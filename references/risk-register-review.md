# Risk Register Review Criteria

Source basis: DOE O 413.3B; DOE G 413.3-7A (Risk Management Guide); DOE G 413.3-9A;
DOE/SC Independent Project Review Process;
AACE RP 40R-08 (Contingency Estimating – General Principles);
AACE RP 62R-11 (Risk Assessment: Identification and Qualitative Analysis);
AACE RP 57R-09 (Integrated Cost and Schedule Risk Analysis);
GAO Cost Estimating and Assessment Guide (2020);
GAO Schedule Assessment Guide (2016).

DOE G 413.3-7A defines the risk management process this review tests against —
**identify → assess (qualitative, then quantitative) → handle → track residual → monitor →
report** — and frames risks as both **threats and opportunities**, each with an assigned risk
owner. The criteria below check whether the register reflects that process; absence of a
required element is itself a finding.

---

## 1. Risk Statement Quality

Every risk statement must identify three components: **cause → event → effect**.
A statement missing any of these is not a risk statement — it is a label.

**Check for:**
- Statements that name only a category ("supply chain risk") with no specific cause or effect
- Tautologies that apply to every project ("cost overruns may occur if unforeseen conditions arise")
- Statements that describe a certainty rather than an uncertainty ("the HVAC system will be
  difficult to install" — if this is certain, it is a scope item, not a risk)
- Cause and effect that are not linked (stating a cause and a completely unrelated effect)
- Conflation of multiple distinct risks into a single entry (common in procurement entries)

**Well-formed example:**
"Long-lead electrical switchgear has a current market lead time of 52–72 weeks; if the
purchase order is not issued within 30 days of contract award, switchgear delivery will
slip past the scheduled mechanical completion date, delaying the critical path by up to
6 months."

**Poorly-formed example:**
"Schedule delay may occur if technical issues arise during commissioning." — No specific
cause. No specific effect. Cannot be mitigated or modeled. Flag as [WEAK-STATEMENT].

**Per DOE G 413.3-7A:** identification starts from the project's **bounding (enabling)
assumptions** (e.g., "site utilities will be available in sufficient quantities") and produces
both **threats and opportunities**, each with an assigned owner. Also check:
- A register that captures only threats and **omits opportunities** (schedule compression,
  prompt-payment discounts, scope optimization) reflects an incomplete identification step —
  DOE treats opportunities as risks to be handled (Exploit/Share/Enhance).
- Risks not tied to the bounding assumptions they depend on, so a changed assumption would
  silently invalidate them.

---

## 2. Probability and Impact Scoring

**Check for:**
- Scores that are inconsistent with the risk narrative (e.g., a risk described as
  "sole-source vendor with 60-week lead time against a 48-week schedule assumption"
  scored as Low probability)
- Impact scores that do not distinguish cost impact from schedule impact — these can
  differ significantly for the same risk
- Systematic underscoring across the register (average score of "Medium" across a complex
  project at CD-2 is a red flag)
- Scoring criteria that are not documented — if there is no scoring matrix, the scores
  are arbitrary
- Risks where the probability × impact score does not match the stated rating tier
  (e.g., P=3, I=4, Score=12 rated "Low" when the matrix should produce "High")

**Per AACE RP 62R-11:** Scoring criteria (what constitutes a "3" vs. a "4" for probability
and for cost and schedule impact) must be documented and applied consistently. Absence of
a scoring rubric makes the register unauditable.

Per DOE G 413.3-7A qualitative analysis: probabilities and consequences are assigned from
documented **threshold guideline tables**, and each risk receives an overall rating from the
**risk matrix**; triggers and interdependencies are identified at the same time.

---

## 3. Mitigation Strategy Substance

A mitigation strategy must describe a specific action that reduces the probability of the
risk occurring, reduces the impact if it does occur, or both. Surveillance actions are not
mitigations.

**Flag the following as non-mitigations:**
- "Monitor [risk] and report to PMO" — surveillance only; does not reduce probability or impact
- "Maintain contingency reserve" — this is a response to impact, not a mitigation of the risk
- "Coordinate with [party]" with no specified deliverable or outcome
- "Review [document] periodically" — no action taken on the risk driver
- Single-word mitigations: "Escalate," "Track," "Discuss"

**Check for:**
- Mitigations that are already completed (and therefore are not mitigation actions, they
  are accomplished facts — the risk should be rescored to reflect this)
- Mitigations that are technically infeasible at the current project phase
- Mitigations that shift risk rather than reduce it (e.g., transferring to contractor via
  lump sum — this is a valid risk response but should be labeled as transfer, not mitigation)
- Mitigations with no cost or schedule implication accounted for in the baseline
  (e.g., "engage alternate vendor as fallback" — is the qualification cost and time in the schedule?)

**Per DOE G 413.3-7A — handling taxonomy.** Every risk should carry a deliberate, named
handling strategy. For threats: **Accept, Avoid, Transfer, Mitigate**; for opportunities:
**Accept, Exploit, Share, Enhance**. Check that:
- The strategy is named and the action matches it — a risk labeled "Mitigate" whose action
  only watches it is mislabeled; "Accept" must be a documented, deliberate decision, and the
  accepted risk still flows into the cost/schedule contingency analysis.
- The register documents a **probability of mitigation success** for each mitigation — this
  is what justifies the residual score (Section 5). Its absence makes residual scores arbitrary.
- **Handling-action costs are placed correctly.** DOE G 413.3-7A is explicit: if a handling
  action *will* be performed, its cost and schedule belong in the **project baseline as direct
  cost** (with a WBS activity to track it), **not** in contingency or management reserve. Only
  costs incurred *only if* a trigger event occurs belong in contingency/MR. A register that
  funds planned mitigations out of contingency is a finding (and a common one).

---

## 4. Mitigation Ownership

Every risk must have a named individual (not a role, department, or "TBD") responsible
for executing the mitigation strategy.

**Flag:**
- Owner listed as "TBD" at CD-2 or later — unacceptable; ownership must be assigned
- Owner listed as a department or team ("Project Controls," "PMO," "Engineering")
- Owner listed as a role without a named person ("Project Manager," "Procurement Lead")
- Risks with no owner field at all

**Per DOE/SC IPR Process:** At the Performance Baseline gate (CD-2 equivalent), the
project must demonstrate that the management organization is adequately staffed and that
accountability for risk management is assigned. Unowned risks are unmanaged risks.
DOE G 413.3-7A assigns a named **risk owner** to every threat and opportunity at identification.

---

## 5. Residual Risk Assessment

After mitigation, every risk must be re-assessed for residual probability and impact.
If a mitigation is claimed to reduce the risk, the residual score must reflect that
reduction — and the reduction must be defensible given the mitigation action.

**Flag:**
- No residual probability or score documented (mitigation effectiveness unknown)
- Residual probability reduced to near-zero with no substantive mitigation (optimism bias)
- Residual score identical to the pre-mitigation score (mitigation has no effect — why
  is it in the plan?)
- Residual probability lower than can be justified by the mitigation strategy (e.g.,
  "monitor" as the mitigation strategy with residual probability of 1 out of 5)

**Per DOE G 413.3-7A:** the residual score should follow directly from the documented
**probability of mitigation success** (Section 3) — if a mitigation is 50% likely to succeed,
the residual cannot sit near zero. The handling step must also identify **secondary risks** —
new risks introduced *by the mitigation itself* (e.g., "advertise the bid package nationwide
to widen the pool" introduces a schedule-extension secondary risk). A register that shows
residual risks but no secondary risks has likely not worked the handling step through.

---

## 6. Monte Carlo Integration (Risk Hooks)

For a risk register to support quantitative risk analysis (QRA), each risk must be
connected to the cost estimate and/or schedule through Monte Carlo risk hooks — specific
cost line items or schedule activities whose durations or costs are driven by the risk.

**Per AACE RP 57R-09 and GAO Schedule Assessment Guide:** Risks carrying a schedule
impact rating ≥ 2 and/or a cost impact rating ≥ 2 should be integrated into the
Monte Carlo model. Exclusion of material risks understates the P80 range.

**Check for:**
- Risks with schedule impact ≥ 2 and MC Hook = N or blank
- Risks with cost impact ≥ 2 and MC Hook = N or blank
- High or Critical rated risks excluded from the QRA model
- MC Hook column absent entirely (QRA not being performed)
- Risks documented as "included in Monte Carlo" but no QRA summary or output provided

---

## 7. Correlation Assumptions

Risks are not independent events. Supply chain delays affect multiple procurements
simultaneously. Commodity price increases affect both the cost estimate and the
contractor's escalation exposure. Failing to model correlation between related risks
understates the P80 outcome.

**Per AACE RP 57R-09:** The correlation matrix between correlated risks must be
documented. Assuming zero correlation between supply chain, labor availability, and
commodity price risks on a major construction project at the current time is not
defensible. (DOE G 413.3-7A likewise directs that major/key risks be analyzed for their
inter-relationships with other risks and projects.)

**Check for:**
- No correlation matrix or correlation documentation anywhere in the submission
- Statement that "risks are treated as independent" with no basis provided
- Obvious risk clusters (all equipment procurements, all labor risks) not grouped
  or correlated in the model
- Monte Carlo output that looks implausibly narrow given the number of High/Critical risks

---

## 8. Risk Register Completeness

A risk register is incomplete not only when entries are poorly written, but when
identifiable risk categories are entirely absent. An IPR reviewer tests for missing risks
by asking: given this project type, phase, and context, what risks would any experienced
reviewer expect to find?

**Check for absence of risks in these categories for major capital projects:**

| Category | Common Missing Risks |
|----------|---------------------|
| Geotechnical | Subsurface conditions on greenfield/brownfield sites, especially if borings are sparse |
| Technology Readiness | Any novel process, material, or equipment not previously deployed at this scale |
| Cybersecurity / OT | SCADA, BMS, process control systems on industrial or scientific facilities |
| Skilled Labor | Regional labor market, workforce availability at peak construction demand |
| Regulatory / Permitting | Major permits with long lead times (air, water, hazmat, structural) |
| Inflation / Escalation | If estimate is more than 6 months old or commodity exposure is significant |
| Single Points of Failure | Sole-source equipment, single-bidder contracting situations |
| Interface / Integration | Between major packages, contractors, or systems |
| Force Majeure | Weather, seismic (if applicable), wildfire — at least a placeholder |

Flag any category that appears entirely absent as a potential gap in the risk identification process.

---

## 9. Overall Register Completeness and Structure

Beyond individual risk quality, assess the register as a whole:

- **Risk count vs. project complexity:** A $200M+ capital project at CD-2 with fewer than
  15 risks is almost certainly incomplete. A $1B+ project with fewer than 25 is suspicious.
- **Category balance:** A register dominated by one category (e.g., all schedule risks, no
  technical or regulatory risks) suggests a narrow identification process.
- **Register currency:** Check dates on risk assessments. A register that hasn't been
  updated in more than 90 days is stale for a Performance Baseline gate review.
- **Prior review findings:** Has the project addressed risk-related findings from prior
  reviews? If prior findings are referenced, verify they are closed, not just acknowledged.

---

## 10. Monte Carlo Output Quality (if provided)

If a Monte Carlo summary or output is included, assess:

- **Iterations:** 10,000 minimum per AACE RP 57R-09. Fewer iterations produce unreliable
  convergence at the tails.
- **Distribution choices:** Are triangular distributions used everywhere with a suspiciously
  narrow spread? Are pessimistic tails truncated? Normal distributions for durations/costs
  that can't go negative are a red flag.
- **P50 vs. deterministic baseline:** If the P50 outcome is close to the deterministic
  baseline, either the model has very little risk, or correlation has been omitted. Probe.
- **P80 reasonableness:** For a complex capital project at CD-2, a P80 within 10% of the
  deterministic baseline is almost certainly understated. The GAO benchmark for major
  capital projects suggests P80 cost growth of 15–30% is typical at this phase.
- **Schedule vs. cost correlation in the model:** Are cost and schedule risks linked, or
  are they run in separate independent models? A project where a schedule risk adds duration
  but the cost model shows no time-related cost growth has a broken integration.

Per DOE G 413.3-7A, the quantitative analysis establishes the **confidence level** for the
project's cost and schedule and is the basis for deriving DOE **contingency** (held by the
project team) as distinct from contractor **management reserve** — see the contingency
treatment in `cost-estimate-review.md` §5–6.

---

## Note on sources

These criteria are grounded in DOE G 413.3-7A (Risk Management Guide) for the DOE risk
process — identification (threats and opportunities, owners, bounding assumptions),
qualitative and quantitative assessment, the handling taxonomy
(Accept/Avoid/Transfer/Mitigate; opportunities Accept/Exploit/Share/Enhance), residual and
secondary risk, and the contingency-vs-management-reserve distinction (DOE G 413.3-7A §7) —
together with AACE RP 40R-08 / 57R-09 / 62R-11, the GAO guides, and DOE O 413.3B /
G 413.3-9A. Two risk training coursebooks (Project Risk Analysis & Management; Advanced Risk
Management) were reviewed as corroborating material and are not cited as standalone authority.
