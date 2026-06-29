# Schedule Review Criteria

Source basis: GAO Schedule Assessment Guide — Best Practices for Project Schedules
(GAO-16-89G, Dec 2015); AACE RP 78R-13 (Original Baseline Schedule Review); AACE RP 49R-06
(Identifying the Critical Path); AACE RP 91R-16 (Schedule Development); AACE RP 38R-06
(Documenting the Schedule Basis, referenced); DOE G 413.3-9A; DOE/SC Independent Project
Review Process.

The GAO guide is the backbone: a reliable Integrated Master Schedule (IMS) satisfies **ten
best practices** grouped into **four characteristics** — **Comprehensive**,
**Well-constructed**, **Credible**, **Controlled**. The AACE RPs corroborate and sharpen the
specifics: 78R-13 supplies a concrete baseline-review checklist, 49R-06 the methods for
identifying a valid critical path, and 91R-16 the schedule-development inputs/outputs. The
GAO Table 7 mapping:

| Characteristic | Best practices |
|----------------|----------------|
| **Comprehensive**  | 1 Capturing all activities · 3 Assigning resources · 4 Establishing durations |
| **Well-constructed** | 2 Sequencing all activities · 6 Confirming the critical path is valid · 7 Ensuring reasonable total float |
| **Credible** | 5 Horizontal & vertical traceability · 8 Conducting a schedule risk analysis |
| **Controlled** | 9 Updating with actual progress and logic · 10 Maintaining a baseline schedule |

Apply ALL ten. GAO notes that if sequencing (BP 2) has major deficiencies, then a valid
critical path, total float, and horizontal traceability (BP 6, 7, 5) are **not possible**.
Most evidence below is extractable from a P6 XER file — see `references/p6-xer-parsing.md`.
Cite the Activity ID and WBS path in every finding.

> **Calculation-settings pre-check (AACE 78R-13).** Before reviewing dates, confirm the
> schedule actually calculates and the settings are correct: every activity has early and
> late dates with **no open logic loops** (loops are grounds for rejection); out-of-sequence
> progress is set to **retained logic**; the total-float calculation method and the
> critical-path identification setting are known and match the spec; calendars are valid; and
> **no project "must-finish" date is imposed** (constrain the final activity instead). A
> schedule that does not calculate cannot be reviewed.

---

# A. COMPREHENSIVE

## 1. Capturing All Activities (BP 1)

The schedule must reflect **all** WBS scope — owner *and* contractor work, government/
owner-furnished items, long-lead procurement, submittals and owner reviews, integration,
test, and commissioning. Per AACE RP 91R-16, the schedule is developed from the WBS, work
packages, and execution strategy; per 78R-13 the reviewer confirms scope completeness
against the contract plans and specifications.

**Check for / Flag:**
- Activities not mapped to the program/contractor WBS — `[UNMAPPED-SCOPE]`.
- Detail-to-milestone ratio that signals thin planning: GAO notes 1–2 detail activities per
  milestone is very low detail, ~10 is highly detailed. A near-1:1 ratio at CD-2 is a
  milestone list, not an IMS.
- **Activity distribution not roughly even** start-to-finish (78R-13): markedly more detail
  in the first half than the second indicates an **under-developed finish plan** (a
  rolling-wave tail presented as a baseline).
- Missing **contractual milestones** (78R-13: all contract-required milestones must be
  present); substantial/mechanical completion (the LD / care-custody-control point) coded as
  a **milestone**, not a task with duration.
- Conspicuously absent scope for the project type — long-lead equipment, permitting, owner
  reviews, utility/third-party tie-ins, startup/commissioning. Absence is a finding
  (cross-check the risk register and cost-estimate WBS).
- Activities with no descriptive name or **duplicate** names (78R-13: unique, descriptive,
  verb-noun-location titles); activities marked as both summary and milestone; **zero-duration
  task activities** that should be milestones.

---

## 3. Assigning Resources to All Activities (BP 3)

The schedule should reflect the resources (labor, materials, equipment, facilities) needed,
their availability, and any funding/time constraints. Per AACE RP 91R-16, budgeted labor
hours and resource quantities (aligned to the WBS and the cost estimate) are core
schedule-development inputs; resource loading is what links the IMS to the estimate.

**Check for / Flag:**
- Detail activities (`TT_Task`/`TT_Rsrc`) with no resource/cost assignment where the plan
  implies one — `[UNRESOURCED]`.
- Resource histogram peaks exceeding credible regional craft availability at peak (78R-13:
  concurrent similar work exceeding planned daily crews) — cross-check the labor risk.
- Resource/crew assumptions inconsistent with durations (BP 4) and with the cost estimate's
  hours and productivity (`cost-estimate-review.md` §3, §11).
- **Resource-dependent activity types used without justification** (78R-13): an activity is
  not resource-driven merely because resources are assigned; that setting belongs only where
  varying resources is genuinely used to control duration.
- For an EVMS project at CD-3, an IMS that is not resource/cost-loaded cannot be a valid
  performance measurement baseline — `[CRITICAL]` at that gate.

---

## 4. Establishing the Duration of All Activities (BP 4)

Durations should realistically reflect how long work takes, share the cost estimate's basis,
and be **short and meaningful enough for discrete progress measurement**.

**Check for / Flag:**
- Excessively long detail activities that mask detail (GAO; 78R-13 suggests a duration
  histogram and checking the longest durations against any contract limit — typically
  excluding summary activities and long-lead deliveries).
- **Default/auto durations left unchecked** (78R-13): review every activity carrying a
  software default duration for oversights; task activities should have duration > 0.
- Durations with no stated basis (judgment vs. historical vs. resource-driven), or
  inconsistent with the resource plan (BP 3; charge-questions CD-2 schedule Q7).
- **Calendar defects (78R-13 — review calendars before dates):** weekend/non-work definitions
  that do not match the workplan; a 7-day/24-hour calendar used for anything but
  curing-type work (the only calendar with no holidays); inconsistent hours-per-day;
  work calendars missing holidays; calendars that do not extend beyond the completion date
  to absorb delay; activities on the wrong calendar; defined-but-unused calendars; weather
  contingency buried in durations rather than shown via specialty calendars.

---

# B. WELL-CONSTRUCTED

## 2. Sequencing All Activities (BP 2)

Every activity must be logically sequenced with predecessor and successor logic. GAO gives
no single numeric threshold (any missing/inappropriate logic can disrupt the network) but
defines precise measures; 78R-13 adds that the network must be **initial-plan logic only**
(no post-NTP changes) and must calculate cleanly.

**Logic completeness — Check for / Flag:**
- Remaining detail activities/milestones **missing a predecessor** (excl. start milestone) or
  **missing a successor** (excl. finish milestone) — `[OPEN-END]`.
- Activities missing **both** ties (floating); **dangling** logic (no tie to the start, or
  no tie off the finish) — these distort total float.
- **Open logic loops / uncalculated schedule** (78R-13): if early/late dates are missing the
  loops were never cleared — grounds for rejection.
- **Summary activities carrying logic** — GAO and good practice: logic belongs on detail
  activities, not summaries/LOE/hammocks.

**Relationship-type and lag discipline — Check for / Flag:**
- The **majority of relationships should be finish-to-start (FS)**; SS/FF used sparingly and
  justified; **start-to-finish (SF)** effectively none — flag any.
- **Lags** minimized and justified (a lag hides unmodeled work or float; note lag calendars).
  **Leads (negative lags)** discouraged — GAO: often unnecessary, and cause **logic failure
  when the lead exceeds the successor's remaining duration**; replace with SS+positive-lag or
  finer breakdown. Flag every lead `[LEAD]`.
- **Date constraints** minimized and justified. GAO taxonomy:
  - **Soft** (Start/Finish No Earlier Than — SNET/FNET; P6 "… on or after"): prevent early
    dates; an *active* one (constraint date == scheduled date) is holding the activity.
  - **Hard** (Start/Finish No Later Than — SNLT/FNLT; Must Start/Finish On — MSON/MFON; P6
    mandatory or "… on/on or before"): **override logic**, fix the date, make the activity
    critical, and can manufacture **negative float**. Unjustified hard constraints at CD-2 are
    `[CONSTRAINT-OVERRIDE]` and usually SIGNIFICANT.
- **No imposed project must-finish date** (78R-13): constrain the final activity instead, so
  post-completion activities are not forced and float calculates correctly.
- High path-convergence (an activity with many predecessors) flags a merge-point risk area.

**Well-formed:** "AC-1420 *Set Reactor* — pred AC-1410 *Erect Steel* (FS); succ AC-1430
*Connect Piping* (FS, 0 lag). No constraint."
**Poorly-formed:** "AC-1420 *Set Reactor* — no predecessor; Must-Finish-On 15-Mar-2027." —
`[OPEN-END]` + `[CONSTRAINT-OVERRIDE]`.

---

## 6. Confirming That the Critical Path Is Valid (BP 6)

The schedule must have a valid **critical path = the longest continuous path of driving logic**
from the data date to the finish milestone (GAO; AACE RP 49R-06). 49R-06 defines four common
identification methods and — importantly — when each is trustworthy:

1. **Lowest total float** — activities with the lowest TF; simple, but **fragments when
   constraints, multiple calendars, lag calendars, interruptible, summary, or open-ended
   activities are present**, because connected critical activities then carry *different*
   float values.
2. **Negative total float** — anything behind an imposed date; useful for flagging, not for
   defining the true driving path.
3. **Longest path** — the driving-logic path traced back from the activities whose early
   finish equals the project's latest early finish. **49R-06 recommends Longest Path for
   projects that use multiple calendars and constraints** — i.e., most real projects.
4. **Longest path value** — assigns each activity a degree-of-longest-path value (like float
   describes criticality).

**Check for / Flag:**
- **Critical path identified by lowest total float on a multi-calendar / constrained schedule**
  — likely fragmented and misleading; the review should expect **Longest Path** here
  (`[CP-METHOD-MISMATCH]`), and confirm the software's CP setting matches the spec.
- The critical path is **not continuous** to the finish milestone — GAO names the usual
  causes (hard constraints, multiple/inconsistent calendars, out-of-sequence progress,
  leads/lags), all of which 49R-06 confirms break a float-based path.
- The CP is **constraint-driven** rather than logic-driven (`[CONSTRAINT-DRIVEN-CP]`), or runs
  through administrative/LOE activities rather than genuine project-driving scope.
- **Manual trace test:** slip a near-finish driving activity and confirm the finish milestone
  moves by the same amount; if not, the logic to the finish is broken.
- Near-critical paths not identified (see BP 7).

---

## 7. Ensuring Reasonable Total Float (BP 7)

Total float should accurately reflect flexibility; critical-path activities carry the least.

**Check for / Flag:**
- **Negative total float in a baseline** — GAO: the schedule can't meet a date as planned;
  78R-13 is stricter still — negative float means the baseline does not meet contractual
  requirements and **should disqualify the submittal**. Always report prominently; trace it
  to its hard constraint (BP 2).
- **Unreasonably high total float** — GAO: indicates schedule **logic might be missing or
  invalid** (e.g., a missing successor). Don't read high float as comfort; trace it.
- **Near-critical paths not identified.** 78R-13 gives a concrete definition: near-critical =
  **total float ≤ half an update reporting period**. Specs often cap the percentage of
  critical/near-critical activities; surface these paths because minor slips make them
  critical.
- Confirm the **total-float calculation method** (early-start−late-start vs.
  early-finish−late-finish); they differ for interruptible and summary activities (78R-13).

---

# C. CREDIBLE

## 5. Verifying Horizontal and Vertical Traceability (BP 5)

- **Horizontal traceability:** the schedule links the products/outcomes of related, sequenced
  activities — the "hand-offs" between disciplines, contracts, and systems are present and in
  the right order. Test a few cross-team hand-offs (engineering release → procurement →
  fabrication → delivery → install) and confirm logic carries the date through. 78R-13's
  submittal-review-deliver and major-material-delivery checks are concrete hand-offs to test
  (each delivery should logically precede the first activity that needs the material).
- **Vertical traceability:** detail rolls up to and agrees with intermediate and
  master/milestone dates. Per AACE RP 91R-16, contracted-party (subcontractor) schedules
  integrated as submittals must reconcile into the master.

**Check for / Flag:**
- Hand-offs between major contracts/vendors/systems missing from the logic (interface delay
  exposure) — cross-check interface/integration risks in the register.
- Detail dates that do not roll up to the reported milestone dates (`[VERTICAL-BREAK]`).
- Subcontractor scope treated as a black box rather than integrated — at CD-3, SIGNIFICANT.

---

## 8. Conducting a Schedule Risk Analysis (BP 8)

An SRA starts from a valid CPM schedule (BP 1–7 must hold first) and runs a statistical
simulation to predict the **confidence level** of meeting the completion date, size the
**schedule contingency/reserve**, and prioritize driving risks (GAO; AACE RP 91R-16 lists
simulation/optimization among schedule-development methods).

**Check for / Flag:**
- **No SRA at CD-2/CD-3** — a baseline completion date with no probabilistic basis is not
  defensible (`[NO-SRA]`).
- Committed/baseline finish set at a low confidence level. DOE practice commonly targets a
  high confidence (≈ **P80**); a baseline at the deterministic (≈ P0–P50) date with no reserve
  understates risk (align with charge-questions CD-2 schedule Q6).
- Token duration-uncertainty ranges (±5% on everything) or omission of the known
  high-uncertainty activities; register risks not mapped to schedule activities (no risk
  "hooks").
- Correlation between related activities/risks ignored → implausibly narrow P80 (same failure
  mode as the cost QRA — `risk-register-review.md`).
- SRA not integrated with cost risk where time-related costs matter (AACE RP 57R-09;
  `cost-estimate-review.md` §11).
- SRA run on a schedule that fails BP 2/6/7 — note when upstream logic defects undermine the
  SRA's validity.

---

# D. CONTROLLED

## 9. Updating the Schedule Using Actual Progress and Logic (BP 9)

**Check for / Flag:**
- **Stale status / data date** (`last_recalc_date` old relative to the review). For an
  *original baseline*, 78R-13 expects the **data date = project start = notice to proceed
  (NTP)**, with no activities statused as started except pre-NTP work.
- **Actual dates in a baseline** (78R-13): a baseline is the plan at bid and should carry no
  actuals (except pre-NTP); actuals belong in the first update. Otherwise poorly performing
  work gets absorbed into the baseline instead of the as-built history.
- **Invalid status dates** — actuals in the future (beyond the data date) or remaining work in
  the past; signs the schedule was not properly recalculated.
- **Out-of-sequence progress** unresolved — confirm the setting is **retained logic**
  (78R-13) and that logic was corrected rather than overridden to "make dates."
- No indication that schedulers maintaining the IMS are trained in CPM (charge-questions: team
  capability). For update reviews specifically, AACE RP 53R-06 (Schedule Update Review) is the
  companion to 78R-13.

---

## 10. Maintaining a Baseline Schedule (BP 10)

**Check for / Flag:**
- **No baseline under configuration management** — performance cannot be measured without a
  change-controlled target schedule. At CD-2 the baseline is the point of the gate.
- Baseline not clearly identified as such (78R-13: title/version should say "Baseline");
  variances (current vs. baseline) not analyzed, or downstream impacts not assessed.
- **No schedule basis document / narrative** — GAO requires it; AACE RP 38R-06 (Documenting
  the Schedule Basis) defines it: explain the approach, define custom fields, state ground
  rules and assumptions, and **justify constraints, lags, long durations, calendars, and
  other unusual features**. Its absence means every constraint/lag flagged above is
  unexplained by definition (`[NO-BASIS-DOC]`).
- **Factors that should fail a baseline (78R-13):** the plan does not meet the contract, is
  unachievable, does not represent the contractor's actual plan, or contains fatal technical
  errors (e.g., negative float, open loops). Weigh the cost of rejecting vs. accepting a
  flawed baseline.

---

## Phase calibration and integration

- **Scale scrutiny to the gate.** Use the schedule charge questions for the phase in
  `references/charge-questions.md`. CD-0/CD-1 may accept a milestone or logic-light schedule;
  **CD-2** applies the full ten best practices at the highest bar; CD-3 requires an
  executable, resource-loaded performance-measurement baseline.
- **Integrate across work products.** The IMS WBS should reconcile to the cost-estimate
  control accounts (`cost-estimate-review.md` §11); the spend curve should match the schedule;
  schedule risks should be the register's risks (`risk-register-review.md`). Inconsistent
  stories across the three documents are themselves a finding.
- **Prior-review closure.** Lead with whether prior findings are closed with evidence;
  reopened/unaddressed prior findings are automatically SIGNIFICANT or CRITICAL.

---

## Extracting the evidence

Most BP 1, 2, 6, 7, 9 measures (activity counts, open ends, dangling logic, relationship-type
mix, leads/lags, hard constraints, total float, data date, baseline presence) can be computed
directly from a Primavera P6 **XER** export — see `references/p6-xer-parsing.md` for the parser
and metric definitions. Cite the Activity ID (`task_code`) and WBS path in every finding.

---

## Note on sources

These criteria are grounded in the GAO Schedule Assessment Guide (GAO-16-89G) — its ten best
practices, four characteristics (Table 7), and standardized data measures (Table 11) — and in
the AACE schedule RPs: **78R-13** (Original Baseline Schedule Review) for the baseline-review
checklist, calculation settings, and disapproval factors; **49R-06** (Identifying the Critical
Path) for valid critical-path methods and the Longest-Path recommendation under
multiple calendars/constraints; and **91R-16** (Schedule Development) for development inputs and
outputs — plus DOE G 413.3-9A and DOE/SC IPR practice. AACE RP 38R-06 (Documenting the Schedule
Basis) and RP 53R-06 (Schedule Update Review) are referenced for the basis document and update
reviews. For schedule risk integration with cost, AACE RP 57R-09 applies (its uploaded copy is
a DRM placeholder; the SRA criteria reflect standard practice).
