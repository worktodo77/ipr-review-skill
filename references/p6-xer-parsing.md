# Parsing a Primavera P6 XER File

This reference explains how to read a Primavera P6 `.xer` export and extract the facts the
schedule review needs (see `schedule-review.md`). The goal is not to reschedule the project
— it is to read the **stored** values the scheduler exported and turn them into traceable
findings (open ends, constraint counts, float, relationship-type mix, etc.).

> **Important:** An XER reports the schedule **as last calculated in P6**. Float, dates, and
> the critical path are stored values from that last calculation — you are reading them, not
> recomputing them. If the file's data date is stale or the logic was changed after the last
> schedule run, the stored values can be inconsistent; note that rather than trusting them
> blindly.

---

## 1. File structure

An XER is a plain-text, **tab-delimited** file. The first line is a header; the body is a
series of table blocks. Each line's first token is a tag:

| Tag | Meaning |
|-----|---------|
| `ERMHDR` | File header — export version, date, currency, source DB. (First line only.) |
| `%T` | Start of a **table**; the second token is the table name (e.g., `TASK`). |
| `%F` | **Field** (column) names for the current table, tab-separated. |
| `%R` | A **record** (row) for the current table, values tab-separated, in `%F` order. |
| `%E` | End of file. |

So a block looks like:

```
%T	TASK
%F	task_id	proj_id	wbs_id	clndr_id	task_code	task_name	task_type	status_code	...
%R	12345	100	2001	5	A1010	Excavate Foundations	TT_Task	TK_NotStart	...
%R	12346	100	2001	5	A1020	Place Mud Mat	TT_Task	TK_NotStart	...
```

**Encoding & gotchas:**
- XER is usually **Windows-1252** (cp1252), not UTF-8. Read with `encoding="cp1252",
  errors="replace"` to avoid crashes on degree signs, em-dashes, etc.
- Values may contain embedded newlines (e.g., notebook topics, calendar data) — but standard
  rows do not; a robust line-based parser handles the common case. For the tables below this
  is not an issue.
- Durations and float are stored in **hours** (fields ending `_hr_cnt`), not days.
- One XER can contain **multiple projects** (e.g., a baseline plus the current schedule).
  Filter by `proj_id` when a table spans projects.

---

## 2. Tables that matter for review

You rarely need every table. These carry the review-relevant data:

| Table | What it gives you | Key fields |
|-------|-------------------|-----------|
| `PROJECT` | Project header, **data date**, finish dates | `proj_id`, `proj_short_name`, `last_recalc_date` (data date), `plan_start_date`, `scd_end_date` (scheduled finish), `fcst_start_date` |
| `PROJWBS` | WBS hierarchy | `wbs_id`, `parent_wbs_id`, `wbs_name`, `proj_node_flag` |
| `TASK` | Activities + stored dates/float/durations/constraints | `task_id`, `task_code` (Activity ID), `task_name`, `task_type`, `status_code`, `wbs_id`, `clndr_id`, `target_drtn_hr_cnt`, `total_float_hr_cnt`, `free_float_hr_cnt`, `cstr_type`, `cstr_date`, `cstr_type2`, `cstr_date2`, `early_start_date`, `late_end_date`, `act_start_date` |
| `TASKPRED` | Logic relationships | `task_id` (the **successor**), `pred_task_id` (the **predecessor**), `pred_type` (FS/SS/FF/SF), `lag_hr_cnt` |
| `CALENDAR` | Hours-per-day for conversions, work pattern | `clndr_id`, `clndr_name`, `day_hr_cnt`, `default_flag` |
| `TASKRSRC` | Resource assignments (resource loading) | `task_id`, `rsrc_id`, `target_qty`, `target_cost` |
| `RSRC` | Resource dictionary | `rsrc_id`, `rsrc_name`, `rsrc_type` |
| `SCHEDOPTIONS` | Scheduling settings (retained logic vs. progress override; critical-activity definition) | scheduling-option fields |

**Field-name cautions:** `TASKPRED.task_id` is the **successor** and `pred_task_id` is the
**predecessor** — this trips people up. `task_code` is the user-facing Activity ID; `task_id`
is P6's internal key used for joins. Constraint and type **codes** (below) are the safest
things to test on; exact ancillary field names can vary slightly by P6 version, so probe the
`%F` line of a table before relying on a column you are unsure about.

**Common code values:**
- `task_type`: `TT_Task` (task-dependent), `TT_Rsrc` (resource-dependent), `TT_Mile` (start
  milestone), `TT_FinMile` (finish milestone), `TT_LOE` (level of effort / hammock).
- `status_code`: `TK_NotStart`, `TK_Active`, `TK_Complete`.
- `pred_type`: `PR_FS`, `PR_SS`, `PR_FF`, `PR_SF`.
- `cstr_type` / `cstr_type2`: `CS_ALAP` (as late as possible), `CS_MSO` (start on), `CS_MEO`
  (finish on), `CS_MSOA`/`CS_MSOB` (start on or after/before), `CS_MEOA`/`CS_MEOB` (finish on
  or after/before), and the **hard** ones `CS_MANDSTART` / `CS_MANDFIN` (mandatory start/
  finish — these **override logic** and can manufacture negative float).

---

## 3. Parser

A self-contained parser returns `{table_name: [rows...]}`, each row a `dict` keyed by field
name:

```python
def parse_xer(path):
    """Parse a P6 .xer into {table_name: list_of_row_dicts}."""
    tables, current, fields = {}, None, None
    with open(path, encoding="cp1252", errors="replace") as fh:
        for raw in fh:
            line = raw.rstrip("\r\n")
            if not line:
                continue
            parts = line.split("\t")
            tag = parts[0]
            if tag == "%T":
                current = parts[1]
                tables[current] = []
                fields = None
            elif tag == "%F":
                fields = parts[1:]
            elif tag == "%R" and fields is not None:
                vals = parts[1:]
                # pad so trailing empty columns still align with their field names
                if len(vals) < len(fields):
                    vals += [""] * (len(fields) - len(vals))
                tables[current].append(dict(zip(fields, vals)))
            elif tag == "%E":
                break
    return tables
```

Helpers for the unit conversion (hours → days, via the activity's calendar):

```python
def calendar_day_hours(tables):
    """clndr_id -> hours/day (defaults to 8 if unspecified)."""
    out = {}
    for c in tables.get("CALENDAR", []):
        try:
            out[c["clndr_id"]] = float(c.get("day_hr_cnt") or 8) or 8.0
        except ValueError:
            out[c["clndr_id"]] = 8.0
    return out

def hours_to_days(hr, day_hr=8.0):
    try:
        return round(float(hr) / day_hr, 2)
    except (TypeError, ValueError):
        return None
```

---

## 4. Computing the review metrics

```python
tables = parse_xer(path)
tasks   = tables.get("TASK", [])
preds   = tables.get("TASKPRED", [])
day_hrs = calendar_day_hours(tables)

def _to_float(x):
    try: return float(x)
    except (TypeError, ValueError): return 0.0

# --- Data date (read it; every date below is relative to this) ---
data_date = (tables.get("PROJECT", [{}])[0]).get("last_recalc_date")

# --- 4a. Open ends (missing predecessor or successor) ---
has_pred = {p["task_id"] for p in preds}        # task_id == successor side
has_succ = {p["pred_task_id"] for p in preds}   # pred_task_id == predecessor side
open_ends = []
for t in tasks:
    if t.get("status_code") == "TK_Complete":
        continue  # completed work legitimately may lack open logic
    tid, ttype = t["task_id"], t.get("task_type")
    missing_pred = tid not in has_pred and ttype != "TT_Mile"     # start milestone may have none
    missing_succ = tid not in has_succ and ttype != "TT_FinMile"  # finish milestone may have none
    if missing_pred or missing_succ:
        open_ends.append((t.get("task_code"), t.get("task_name"),
                          "no pred" if missing_pred else "", "no succ" if missing_succ else ""))

# --- 4b. Relationship-type mix and leads (negative lag) ---
from collections import Counter
rel_mix = Counter(p.get("pred_type") for p in preds)
leads = [p for p in preds if _to_float(p.get("lag_hr_cnt")) < 0]   # leads are a red flag

# --- 4c. Hard / logic-overriding constraints ---
HARD = {"CS_MANDSTART", "CS_MANDFIN"}
constrained = [t for t in tasks
               if t.get("cstr_type") or t.get("cstr_type2")]
hard_constrained = [t for t in tasks
                    if t.get("cstr_type") in HARD or t.get("cstr_type2") in HARD]

# --- 4d. Float (negative float = behind schedule) ---
def tf_days(t):
    return hours_to_days(t.get("total_float_hr_cnt"), day_hrs.get(t.get("clndr_id"), 8.0))
negative_float = [t for t in tasks if (tf_days(t) or 0) < 0]
near_critical  = [t for t in tasks if 0 <= (tf_days(t) or 1e9) <= 10]  # ~2 weeks of float

# --- 4e. LOE / hammock activities (should not drive the critical path) ---
loe = [t for t in tasks if t.get("task_type") == "TT_LOE"]

# --- 4f. Resource loading coverage ---
resourced = {r["task_id"] for r in tables.get("TASKRSRC", [])}
unresourced = [t for t in tasks
               if t["task_id"] not in resourced
               and t.get("task_type") in ("TT_Task", "TT_Rsrc")]
```

**Critical path note:** P6 stores how "critical" is defined in `SCHEDOPTIONS` — either *total
float ≤ a threshold* (often 0) or *longest path*. There is no universal single "is critical"
boolean to trust across versions, so derive criticality from `total_float_hr_cnt` ≤ the
project's threshold and state which definition you used. Report **negative** float prominently
— it always signals the schedule cannot meet a constraint or imposed date.

---

## 5. From parsed facts to findings

Map the extracted numbers onto the `schedule-review.md` criteria categories:

| schedule-review.md category | XER-derived evidence |
|-----------------------------|----------------------|
| Schedule logic integrity | `open_ends` count and list; dangling (single-tie) activities; `rel_mix` (excessive SS/FF or `leads` suggest logic manipulation) |
| Critical path realism | `negative_float`, `near_critical`, `hard_constrained`; whether the path is logic- or constraint-driven |
| Resource loading | `unresourced` count vs. total; `RSRC`/`TASKRSRC` presence and peaks |
| Duration reasonableness | `target_drtn_hr_cnt` → days via calendar; flag very long activities masking detail; check `CALENDAR` assignments |
| Schedule risk integration | risk hooks (compare to risk register); presence/absence of an SRA — usually external to the XER |
| Baseline integrity | `data_date` (`last_recalc_date`); multiple `proj_id`s = baseline(s) present; compare to current |
| WBS & coding | `PROJWBS` hierarchy; alignment of `wbs_id`/`task_code` to the cost-estimate control accounts |

Every finding should cite the **Activity ID** (`task_code`) and/or WBS path so the scheduler
can trace it — exactly as the cost reviewer cites a control account and the risk reviewer
cites a risk ID.

---

## 6. Quick-start checklist for a review run

1. `parse_xer()` the file; confirm it parsed (non-empty `TASK`, `TASKPRED`).
2. Read and report the **data date** and the **scheduled finish** (`scd_end_date`).
3. Note whether **multiple projects** are present (baseline + current).
4. Run 4a–4f; capture counts and the specific offending Activity IDs.
5. Hand the numbers to `schedule-review.md` for interpretation and severity classification.

> If you only have an Excel or PDF schedule export (not an XER), you cannot see stored float,
> relationship types, or constraints reliably — say so, and scope the review to what the
> export actually contains (activity list, durations, dates) rather than inferring logic.
