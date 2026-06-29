# IPR Review Skill

An AI assistant **skill** that performs an **Independent Project Review (IPR)–style
self-assessment** of project-controls work products — **risk registers**, **integrated master
schedules** (Primavera P6), and **cost estimates** — and returns structured, cited findings in
the format of a DOE/SC IPR closeout report.

It is designed to give a project-controls practitioner the kind of honest, specific, standards-
grounded feedback an independent review committee would give — *before* a formal review.

> ⚠️ **This is an experimental pilot. Outputs are AI-generated and must not be relied upon.**
> It is **not** a formal Independent Project Review and **not** professional engineering, legal,
> or financial advice. See **[Disclaimer & Limitation of Liability](#disclaimer--limitation-of-liability)**
> and **[DISCLAIMER.md](DISCLAIMER.md)** before using it.

---

## What it does

Given one or more uploaded work products, the skill:

1. **Intakes** the context — work-product type, project phase / decision gate, project description,
   and any prior-review history.
2. **Reads the data** — Excel risk registers and cost books, Primavera **P6 `.xer`** schedule
   exports, and PDF/Word narratives.
3. **Applies a review protocol** grounded in published standards (see [Standards](#standards-referenced)).
4. **Produces an IPR-style report** — charge-question responses, an issue summary, and
   classified **Findings / Comments / Recommendations** (`CRITICAL` / `SIGNIFICANT` / `MINOR` /
   `STRENGTH`), each traceable to a specific risk ID, schedule activity, or cost account, plus an
   overall readiness verdict.

It reviews three work products:

| Work product | What it checks (examples) |
|---|---|
| **Risk register** | risk-statement quality (cause→event→effect), probability/impact scoring, mitigation substance & ownership, residual & secondary risk, Monte-Carlo integration, correlation, completeness |
| **Schedule (IMS)** | logic integrity (open ends, dangling logic, relationship mix, leads), constraint discipline, critical-path validity & method, total float, resourcing, calendars, baseline & status |
| **Cost estimate** | AACE class vs. maturity, scope/WBS coverage, quantities & pricing, escalation, contingency derivation, management reserve, BOE traceability, validation/benchmarking, cross-WP integration |

Scrutiny scales with the gate (conceptual → baseline → construction start → completion).

---

## How it works

```
SKILL.md                      ← the agent's operating instructions (intake → read → protocol → report)
references/
  charge-questions.md         ← phase-specific charge questions (CD-0 … CD-4 and private-sector equivalents)
  risk-register-review.md     ← risk register review criteria
  schedule-review.md          ← schedule (IMS) review criteria
  cost-estimate-review.md     ← cost estimate review criteria
  p6-xer-parsing.md           ← how to parse a Primavera P6 .xer and compute schedule metrics
```

The agent reads `SKILL.md`, then the reference file(s) for the work product(s) under review.

---

## Installation & use

This is a skill for AI coding/agent assistants that support the *skills* convention (a `SKILL.md`
plus `references/`). To use it:

1. **Clone** this repository (or drop the folder into your assistant's skills directory).
   ```bash
   git clone https://github.com/worktodo77/ipr-review-skill.git
   ```
2. **Invoke it** by asking your assistant to review a work product and attaching the file, e.g.:
   - *"Review my risk register before the gate review."*
   - *"Run an IPR check on this P6 schedule (.xer)."*
   - *"Stress-test this cost estimate for CD-2."*
3. The assistant follows `SKILL.md`, applies the relevant criteria, and returns the IPR-style report.

You can also use the `references/*.md` files directly as a **human checklist** for a manual
peer review, independent of any AI tool.

**Accepted inputs:** Excel (`.xlsx`), Primavera P6 (`.xer`), PDF, and Word. A description of a
work product is *not* sufficient — the review needs the actual data.

---

## Status & testing

This is an **early pilot**. During development it was exercised against sample project-controls
work products to confirm it parses inputs and produces criteria-based findings in the expected
format. It has **not been independently or formally validated**, no accuracy or performance claims
are made, and every output **must be independently verified by a qualified professional** (see the
[Disclaimer](#disclaimer--limitation-of-liability)).

## Standards referenced

The review criteria are **the skill authors' own distillations** of widely used public standards and
recommended practices, including U.S. DOE Order 413.3B and Guides 413.3-7A (Risk Management) and
413.3-9A (Project Review); AACE® International Recommended Practices (e.g., 17R-97, 31R-03, 40R-08,
49R-06, 57R-09, 62R-11, 78R-13, 91R-16); and the U.S. GAO Cost Estimating & Assessment Guide and
Schedule Assessment Guide.

**This repository does not contain or redistribute those copyrighted source documents.** AACE®,
Primavera®, and all other marks are the property of their respective owners; this project is **not
affiliated with, sponsored by, or endorsed by** DOE, AACE International, the GAO, Oracle, or any
standards body.

---

## Limitations

- **Experimental / AI-generated.** Outputs can be incomplete, mistaken, or miscalibrated and **must
  be independently verified by a qualified professional.**
- **Not a formal IPR.** It does not constitute a DOE Independent Project Review, regulatory approval,
  or any assurance of gate passage.
- **Reviews exported files, not live tools.** Schedule metrics are read from the **stored values** in
  a `.xer` (it does not re-run the scheduling engine); EVMS execution, live tool settings, and basis
  narratives outside the files are out of scope.
- **Quality depends on inputs.** Findings are only as good as the data provided; absent context is
  flagged as "confirm/verify," not asserted as fact.
- **Coverage ≠ execution.** A criterion being in the reference files does not guarantee the agent
  computes it on every run.
- **No data leaves with the skill.** The repo ships criteria only — no project data, no source standards.

---

## Disclaimer & Limitation of Liability

**THIS IS A PILOT / EXPERIMENTAL TOOL. ITS OUTPUTS ARE NOT TO BE RELIED UPON.**

The IPR Review Skill and all of its outputs are provided **"AS IS" and "AS AVAILABLE," without
warranties of any kind**, express or implied, including (without limitation) merchantability, fitness
for a particular purpose, accuracy, completeness, and non-infringement.

Outputs are **automatically generated** and may be **incorrect, incomplete, or misleading**. They do
**not** constitute a formal Independent Project Review and are **not** professional engineering, cost-
estimating, scheduling, legal, financial, or other professional advice, and **no professional or
fiduciary relationship is created** by use of this tool. Nothing here should be used as the basis for
any project, funding, safety, contractual, or other decision. **Always obtain independent verification
from a qualified professional before acting on any output.**

**You assume all risk** arising from use of this tool and its outputs. To the maximum extent permitted
by law, the authors, contributors, and copyright holders **shall not be liable** for any direct,
indirect, incidental, special, consequential, exemplary, or punitive damages, or any loss of profits,
data, goodwill, or other losses, arising out of or relating to the tool or its outputs, **even if
advised of the possibility of such damages**, and regardless of the legal theory.

**You agree to indemnify and hold harmless** the authors, contributors, and copyright holders from any
claims, damages, liabilities, costs, or expenses (including reasonable legal fees) arising from your
use of the tool or its outputs.

See **[DISCLAIMER.md](DISCLAIMER.md)** for the full text. 
---

## License

Released under the **MIT License** — see [LICENSE](LICENSE). The MIT License itself includes an
"AS IS," no-warranty, no-liability provision; the disclaimer above supplements it.

## Contributing & support

Pilot. Issues and contributions welcome, but the project is provided without any commitment of support,
maintenance, or fitness for any purpose.
