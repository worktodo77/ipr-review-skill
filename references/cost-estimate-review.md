# Cost Estimate Review Criteria

Source basis: AACE RP 17R-97 (Cost Estimate Classification System);
AACE RP 31R-03 (Reviewing, Validating, and Documenting the Estimate);
AACE RP 34R-05 (Basis of Estimate);
AACE RP 40R-08 (Contingency Estimating – General Principles);
AACE RP 57R-09 (Integrated Cost and Schedule Risk Analysis);
GAO Cost Estimating and Assessment Guide (GAO-09-3SP);
DOE G 413.3-9A; DOE/SC Independent Project Review Process.

A real cost-estimate reviewer does three things in sequence (per AACE RP 31R-03):
**review** the estimate (qualitative — does it meet requirements, cover the full scope,
follow required methods, and present in the expected format), **validate** it (quantitative
— benchmark it against independent metrics, history, and a check estimate), and confirm it
is **documented** (the Basis of Estimate is complete and every cost is traceable). The
criteria below are organized to support that sequence. Apply ALL of them — absence of a
required element is itself a finding.

---

## 1. Estimate Classification and Maturity

Per AACE RP 17R-97, the **maturity level of project definition deliverables** is the sole
primary determinant of estimate class. The estimate's claimed class must be supported by
the actual maturity of the design and planning deliverables — not asserted, and not driven
by the percentage of design "complete" alone.

**The 17R-97 classification matrix (use the actual figures):**

| Class | Maturity (% of definition) | Typical end usage | Methodology | Accuracy range index [a] |
|-------|----------------------------|-------------------|-------------|--------------------------|
| Class 5 | 0% to 2%    | Screening / feasibility   | Stochastic (factors/models) or judgment | 4 to 20 |
| Class 4 | 1% to 15%   | Concept study / feasibility | Primarily stochastic | 3 to 12 |
| Class 3 | 10% to 40%  | Budget authorization or control | Mixed, primarily stochastic | 2 to 6 |
| Class 2 | 30% to 75%  | Control or bid/tender | Primarily deterministic | 1 to 3 |
| Class 1 | 65% to 100% | Check estimate or bid/tender | Deterministic | 1 |

[a] Accuracy is expressed as an index relative to a Class 1 estimate. If a Class 1 range is
±10/−5%, an index of 10 implies roughly +100/−50% at an 80% confidence interval. The range
is project-specific; the table gives the expected band, not a guarantee.

**Gate alignment (using the skill's CD mapping):** CD-0 → Class 5; CD-1 → Class 4; CD-2
(Performance Baseline) → Class 3 maturing to Class 2. A Performance Baseline built on a
Class 4/5 estimate is not defensible.

**Check for / Flag:**
- **Class–maturity mismatch:** estimate labeled Class 3 (or "AACE Class 2") while the
  supporting deliverables (P&IDs, equipment lists, site investigation, quantity takeoffs)
  are at a concept level. Flag as `[CLASS-OVERSTATED]` — this is the single most common and
  most consequential cost-estimate finding at a baseline gate.
- **No stated class at all** — the estimate does not declare its AACE class or confidence
  basis, so its accuracy cannot be judged against expectation.
- **Methodology inconsistent with claimed class:** a "Class 2" estimate built almost
  entirely from stochastic factors and allowances (the methodology of a Class 4), or a
  "Class 5" priced from detailed deterministic takeoffs (effort not credible at that phase).
- **Accuracy range narrower than the class supports:** a Class 3 estimate presented with a
  ±10% range implies Class 1 precision the deliverables cannot support. Optimistic narrowing
  of the range is a form of optimism bias — Section 10.

---

## 2. Scope Coverage and Completeness

The estimate must cover the **entire** project scope. Per AACE RP 31R-03, confirming the
estimate "covers the entire project scope" and is "free from errors and omissions" is a core
purpose of the review. Per GAO, a high-quality estimate is **comprehensive** — it includes
all life-cycle costs, has enough detail (a WBS with a dictionary), and documents all
assumptions and exclusions.

**Check for / Flag:**
- WBS does not align with the project scope basis document or the schedule WBS — costs and
  activities cannot be reconciled (see Section 11).
- Identifiable scope present in the design deliverables but absent from the estimate.
- Allowances used in place of estimates for undefined scope **without a documented basis**
  for the allowance percentage or amount.
- Whole cost categories missing. For major capital projects, test for the presence of:

| Category | Commonly under-scoped or omitted |
|----------|----------------------------------|
| Construction indirects | General conditions, temporary facilities, supervision, scaffolding, craft per-diem |
| Owner's costs | PMO/PM staff, owner's engineering, legal/permitting fees, insurance, financing |
| Commissioning & start-up | Systems completion, vendor reps, operator training, first-fill/consumables |
| Site & enabling works | Demolition, hazmat abatement, utilities relocation, off-site infrastructure |
| Escalation | Treated as $0 or omitted on a multi-year spend (Section 4) |
| Spares & special tools | Capital spares, OEM-recommended spares |
| Sales/use tax & duties | On equipment and materials, where applicable |

Flag any conspicuously absent category as a potential scope gap, not merely a number to add.

---

## 3. Quantity Development and Pricing Basis

**Quantities — check for:**
- Quantity basis not stated (measured takeoff vs. parametric/factored vs. assumed). At
  Class 3 and better, major commodity quantities (concrete, steel, pipe, cable, earthwork)
  should be measured, not factored.
- Round-number quantities that signal assumption rather than takeoff (e.g., "10,000 LF of
  pipe" across an entire plant) at a maturity where measurement is expected.
- Quantity growth allowances missing where the design is incomplete (design-development
  growth on quantities is real and should be explicit, not buried in contingency).

**Pricing — check for:**
- Unit rates with no stated **source and date**. A unit rate from a 3-year-old database,
  un-escalated, is a finding.
- Vendor quotes that are stale, scope-incomplete, or budgetary ("for information only")
  treated as firm pricing. Check quote age, validity period, and scope coverage.
- **Sole-source / single-bid pricing** treated as competitive market pricing without an
  adjustment or a risk entry. Flag and cross-check against the risk register.
- Labor pricing inconsistent with the schedule's productivity and crew assumptions
  (Section 11) — wage rates, burden, and productivity factors should reconcile to the IMS.

**Reviewer technique (per 31R-03, Pareto principle):** roughly 80% of the cost comes from
~20% of the line items. Drill into the high-value items: have the basis for the quantity and
the unit rate shown explicitly. If the answers to drill-down questions are "evasive or
unclear" (31R-03's phrase), a broader problem with estimate quality is likely.

---

## 4. Escalation

**Check for:**
- Escalation methodology not stated (index-based vs. compounded rate vs. lump sum).
- Escalation **index source and publication date** not documented, or a single blended rate
  applied to dissimilar commodities (structural steel, copper, switchgear, and labor do not
  escalate at the same rate).
- Escalation applied to the wrong time basis — it must be applied to the **time-phased spend
  curve** (to the midpoint of expenditure for each element), not to the base-year total as a
  flat add. Applying escalation only to the contract-award date understates it.
- Escalation set to $0 or omitted on a multi-year project. Even in low-inflation periods this
  requires a stated, defensible assumption.
- "Hyper-escalation" or known market premiums (e.g., constrained electrical equipment
  markets) not distinguished from baseline escalation where the exposure is material
  (31R-03 specifically calls out distinguishing hyper-escalation for management).

Per AACE RP 40R-08, escalation and currency are treated as **separate** risk/cost
provisions from contingency — confirm escalation is not double-counted inside contingency
or silently omitted from both.

---

## 5. Contingency Derivation

Per AACE RP 40R-08, contingency is a risk fund covering cost (and schedule) uncertainty
**within the defined project scope**, established as part of the overall risk-management
process. It is **not** an allowance for major scope changes, and per 40R-08 it is treated
separately from escalation, currency, and other primarily financial risks (and from
management reserve — Section 6).

**The contingency must have a stated method.** Per 40R-08 the common methods are:
- **Predetermined / percentage** (judgment; e.g., a flat % of base estimate)
- **Expected value** (probability × impact summed across identified risks)
- **Parametric** (regression models driven by system maturity and complexity)
- **Range estimating / simulation** (Monte Carlo on cost — and, integrated with schedule,
  per AACE RP 57R-09)

**Check for / Flag:**
- **Flat-percentage contingency at CD-2.** A single "15%" with no risk basis is a Class
  4/5-grade method presented at a baseline gate. Flag `[CONTINGENCY-NOT-RISK-BASED]`. At
  CD-2 the contingency should be derived from the quantitative risk analysis (QRA).
- **Contingency not traceable to the risk register.** If the register's material risks
  (see `risk-register-review.md`) are not the drivers of the contingency figure, the two
  documents are telling different stories. Reconcile them.
- **No stated confidence level.** Risk-based contingency should be tied to a target
  probability (commonly the P50–P80 band; DOE baselines commonly target the upper end,
  ~P80/P85, at CD-2). "Contingency = P80 minus the deterministic point estimate" is the
  defensible construction.
- **Contingency that only adds to the point estimate, never models underrun** — a one-sided
  distribution that ignores the possibility of an underrun is usually a modeling artifact.
- **Contingency held at a single program level** with no visibility into which control
  accounts or risks drive it (acceptable to hold centrally, but the derivation must be
  transparent).

**Well-formed example:** "Contingency of $42M (P80) is derived from a 10,000-iteration Monte
Carlo cost-risk model integrating the 23 quantified risks in the register; the P50 is $1.31B
and the P80 is $1.35B against a deterministic base of $1.308B; the dominant drivers are
switchgear lead-time and site labor productivity (tornado attached)."

**Poorly-formed example:** "Contingency: 15% of construction cost." — No method, no risk
linkage, no confidence level. Flag `[CONTINGENCY-NOT-RISK-BASED]`.

---

## 6. Management Reserve and Other Risk Funds

**Check for:**
- **Management reserve (MR) conflated with contingency.** MR covers in-scope "unknown
  unknowns" and is controlled by management above the project; contingency covers the
  quantified/known risk exposure and is controlled by the project. They must be sized and
  reported separately.
- MR sized arbitrarily (a round percentage) with no rationale relative to the residual
  uncertainty at this phase.
- Escalation reserve and foreign-exchange (FX) provisions not separated from contingency
  where exposure is material (per 40R-08, these are distinct from contingency).
- Total risk funding (contingency + MR + escalation reserve) not rolled up anywhere, so the
  reader cannot see the full risk-adjusted cost.

---

## 7. Indirect and Owner Costs

Indirects and owner costs are the most frequently under-estimated portions of a capital
estimate. Review them specifically rather than accepting a percentage roll-up.

**Check for:**
- Construction indirects (field supervision, temporary facilities and utilities, general
  conditions, small tools/consumables, scaffolding) applied as a thin blanket percentage
  inconsistent with the execution strategy and schedule duration.
- Owner's costs (project management, owner's engineering, design management, permitting and
  legal, insurance, commissioning oversight, owner-furnished equipment) missing or
  understated — these commonly run a substantial fraction of installed cost and are
  routinely thin.
- Start-up and commissioning costs (vendor reps, operator training, first fills,
  performance testing, temporary operations) absent or buried.
- Time-related indirects (extended general conditions, escalated overheads) not linked to
  the schedule — if the schedule grows, these costs grow (Section 11).

---

## 8. Basis of Estimate (BOE) Narrative

Per AACE RP 31R-03 and RP 34R-05, the BOE is the central document of the estimate. It must
let an independent estimator understand and, for the major elements, reconstruct the
estimate. A well-organized BOE describes four bases:

- **Design basis** — scope, the specific drawings/specs/deliverables used (listed by
  number and revision), and exclusions.
- **Planning basis** — execution strategy, contracting/packaging plan, schedule milestones,
  shift and labor assumptions.
- **Cost basis** — pricing sources, unit-rate basis, allowances, factors, wage rates, FX,
  and escalation basis.
- **Risk basis** — contingency method, the risks considered, and the probabilistic outcome.

**Check for / Flag:**
- BOE missing entirely, or present but not covering all four bases. At CD-2 a missing BOE is
  `[CRITICAL]` — the estimate is unauditable.
- **Assumptions, inclusions, and exclusions not explicitly stated.** Per GAO, ground rules
  and assumptions must be documented; undocumented assumptions are where estimates quietly
  fail. Exclusions must be listed and must reconcile with the scope basis and the schedule.
- **Traceability broken** (31R-03): not every cost on the estimate summary can be traced to
  estimate detail and backup. Spot-check several summary lines down to their detail.
- **No reconciliation to the prior estimate.** A new estimate gains credibility by explaining
  the delta from the last one. Reconciliation should show, by element, the previous value,
  current value, variance $, and variance % (31R-03 / ASTM E1804 format). Large unexplained
  movements are a finding.

**Well-formed BOE assumption:** "Structural steel priced at $4,250/ton installed, based on
three competitive fabricator budget quotes dated March 2026 (validity 60 days), escalated to
the Q3-2027 erection midpoint at 4.1%/yr per [index]; excludes architecturally exposed steel,
which is carried as an allowance pending design."

**Poorly-formed BOE assumption:** "Steel priced per in-house database." — No source date, no
escalation basis, no scope definition, not traceable. Flag `[BOE-UNTRACEABLE]`.

---

## 9. Validation and Benchmarking

Per AACE RP 31R-03, validation is the **quantitative** half of the review: the estimate is
benchmarked against independent metrics and, where warranted, a check estimate. Per GAO
(Step 7), the point estimate should be **compared to an independent cost estimate** and
**cross-checked** on the major cost drivers.

**Check for / Flag:**
- No estimate-metrics/benchmark report (e.g., $/SF, $/kW, engineering hours/total, labor
  %/total, $/installed ton) comparing this estimate to similar completed projects.
- Benchmark ratios that sit well outside the range for the project type with **no
  explanation** (31R-03: "if there is a large discrepancy, it must be explainable").
- No independent check estimate or cross-check on the cost drivers at a baseline gate.
- Benchmark sources weaker than they should be — 31R-03's preference order is third-party
  published data (best) > company historical actuals (acceptable) > prior detailed estimates
  (least preferred).
- Validation performed only by the team that prepared the estimate, with no independent or
  "cold-eyes" review where the gate warrants it.

---

## 10. Estimate Quality — GAO Four Characteristics and Optimism Bias

GAO assesses a high-quality estimate against four characteristics. Use them as a closing
quality lens and map findings to whichever characteristic they undermine:

- **Comprehensive** — full scope and life cycle, adequate detail (WBS + dictionary),
  assumptions and exclusions documented (Sections 2, 8).
- **Well-documented** — BOE complete, sources captured, every cost traceable, results
  reconciled and reproducible (Sections 8, 9).
- **Accurate** — unbiased, based on current and relevant data, free of math/double-count
  errors, adjusted for inflation, reconciled to prior estimates (Sections 3, 4, 8).
- **Credible** — sensitivity analysis performed, risk/uncertainty analysis performed,
  cross-checked, and compared to an independent estimate (Sections 5, 9, 11).

**Optimism bias is the reviewer's standing hypothesis.** GAO's body of work finds capital
cost estimates are more often understated than overstated. Probe specifically for:
- A point estimate at or below the P30 of any risk analysis that exists.
- "Best-case" productivity, lead-time, and pricing assumptions stacked across the estimate.
- Contingency and escalation both thin (the two provisions that absorb optimism).
- A narrowed accuracy range inconsistent with the estimate class (Section 1).

---

## 11. Integration with Schedule and Risk Register

A cost estimate cannot be judged in isolation. Per 31R-03 the estimate must be "integrated
with the schedule," and per AACE RP 57R-09 cost and schedule risk are analyzed together.

**Check for / Flag:**
- Estimate WBS / control accounts do not map to the schedule WBS — cost and time cannot be
  reconciled or status-reported together.
- Time-phased spend curve (cash flow) inconsistent with the IMS — escalation and time-related
  indirects are derived from the spend curve, so a mismatch propagates into both.
- Time-related cost risks (extended overhead, prolonged escalation) appear in the cost model
  but the driving duration risk is absent from the schedule risk analysis, or vice versa —
  a broken cost/schedule risk integration (57R-09).
- Contingency not reconciled to the risk register's quantified risks (Section 5).
- Escalation rate/curve inconsistent with the schedule's expenditure timing (Section 4).

---

## 12. Currency, Document Control, and Prior-Review Closure

- **Currency:** vendor quotes, indices, and labor rates should be current. Pricing more than
  ~6 months old on a volatile commodity, or an estimate not refreshed against the current
  design revision, is stale for a baseline gate.
- **Document control:** the estimate and BOE should carry revision dates/version numbers
  identifying them as the documents of record, consistent with the design revision they price.
- **Prior-review closure:** if the estimate was reviewed before, lead with whether prior
  findings are **closed with evidence** (a corrected number/BOE), not merely acknowledged.
  Reopened or unaddressed prior cost findings are automatically SIGNIFICANT or CRITICAL.

---

## Note on sources

The criteria above are grounded in the uploaded sources (AACE 17R-97, 31R-03, 40R-08, and the
GAO Cost Estimating and Assessment Guide GAO-09-3SP) plus standard AACE practice. AACE RP
34R-05 (Basis of Estimate) is cited as the dedicated BOE reference; its content here is drawn
from 31R-03's BOE coverage and general practice. RP 57R-09 (Integrated Cost and Schedule Risk
Analysis) is cited for cost/schedule risk integration; the uploaded copy is a DRM placeholder,
so its criteria here reflect standard 57R-09 practice. If the 34R-05 and 57R-09 full texts are
added later, Sections 5, 8, and 11 can be tightened to those documents' specific clause language.
