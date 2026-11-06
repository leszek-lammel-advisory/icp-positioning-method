---
domain: positioning-strategy
module: KB-7
status: tested
sources: [sources/wynter-perception-validation-dossier.md]
depends_on: [M1, KB-2, KB-3]
---

# Expression Validation

## Decision and boundary

KB-7 tests whether a specific expression faithfully communicates an already
declared positioning hypothesis to a defined, relevant audience in a defined
situation. Its output is `expression_supported`, `expression_revise`,
`upstream_research_needed`, or `blocked`.

It is not a positioning generator or a strategy vote. A respondent preferring
one expression does not establish the buyer's actual alternative, prove the
value chain, or select a market frame. Those remain M1, KB-2, and KB-3
decisions with their original evidence states. KB-7 may preserve an upstream
hypothesis as the test target, but may never strengthen it.

The question is deliberately narrow: "Can matched respondents, unaided,
identify who this is for, the problem, the comparison, and the difference?"
Only after that question has been answered may a test ask for preference or
credibility. Preference is a downstream expression signal, not market demand,
adoption intent, or proof of an upstream claim.

## Admission and sequence

Every run declares an audience, situation, exact expression variant, and an
upstream snapshot containing one M1 alternative, one KB-2 value statement,
and one KB-3 frame. The snapshot can contain a hypothesis or research-needed
state. It is a test target, not a claim upgraded by this module.

Run the following sequence without skipping a gate:

1. Screen for the intended audience and situation. An internal stakeholder,
   a generic respondent, or a prospect outside the stated situation is not a
   matched respondent.
2. Ask unaided comprehension: who is the expression for, what problem does it
   name, what does the buyer do otherwise, and what is different here?
3. Ask what proof or credibility concern remains. Record this separately from
   comprehension so a respondent's skepticism is not rewritten as a wording
   problem.
4. Only then collect preference, if preference is useful to the expression
   decision. A preference result without the completed prior gates is blocked.
5. Classify the earliest defect and route it. Do not revise words while an
   earlier positioning boundary is contradicted.

## Evidence ledger

Each response records its source ID, provenance, audience-match status, stage,
structured result, and exact claim. A response can support only the field it
was asked about. Internal preference has `internal` provenance and cannot
support audience match, comprehension, preference among buyers, or an
upstream conclusion. Synthetic fixtures are method tests only and never
describe a real company, customer, or market.

| Field | Pass condition | Failure means | It cannot establish |
|---|---|---|---|
| Audience match | Respondent is in the stated buyer and situation. | Test design is invalid for this scope. | A segment exists or will buy. |
| Audience and problem recognition | Unprompted answer identifies the intended audience and problem. | Wording or audience diagnosis is incomplete. | Demand or category fit. |
| Comparison clarity | Unprompted answer identifies the supplied alternative or comparison. | Return to M1 if the named alternative is contradicted. | A new buyer alternative. |
| Difference comprehension | Respondent can state the supplied difference. | Expression can be revised only after earlier fields pass. | Value or outcome proof. |
| Credibility / proof | Respondent names a proof gap or finds the claim credible. | Route an outcome or proof contradiction to KB-2. | A measured buyer outcome. |
| Frame fit | Respondent's interpretation is compatible with the supplied frame. | Route a frame contradiction to KB-3. | A new frame or category. |
| Preference | A matched, comprehending respondent prefers an expression. | A copy comparison only. | Alternative, value, frame, demand, or adoption. |

## Earliest-boundary routing

Choose one primary failure. If more than one issue appears, stop at the
earliest upstream one rather than stacking copy edits on top of it.

| Primary failure | Required route | Forbidden shortcut |
|---|---|---|
| No matched audience | `research_design` | Treating generic or internal preference as buyer validation. |
| Incomplete comprehension before preference | `research_design` | Reading a preference winner as a positioning winner. |
| Named alternative contradicted | M1 | Substituting a different alternative in copy. |
| Value mechanism, outcome, or proof contradicted | KB-2 | Adding a stronger benefit claim or proof language. |
| Supplied frame contradicted | KB-3 | Naming a new category from the response. |
| All earlier concepts are understood but the difference is unclear | expression layer | Declaring the value chain false. |

Frame routing is later than alternative and value routing. A frame failure may
be sent to KB-3 only when this test did not also contradict the M1 alternative
or KB-2 value target. A proof gap belongs to KB-2 because expression cannot
invent proof.

## Decision aggregation

Return `blocked` for an internal-only test, a mismatched audience, or a
preference question asked before the required unaided-comprehension fields.
Return `upstream_research_needed` when a matched, completed test contradicts
the supplied alternative, value/proof, or frame, with the exact owner above.
Return `expression_revise` only when matched respondents understand audience,
problem, and comparison but fail to understand the stated difference without
contradicting an earlier layer. Return `expression_supported` only when the
matched audience clears every comprehension field. It means the expression is
understood at the recorded scope. It never upgrades the upstream snapshot or
establishes demand.

## Worked patterns

**Expression revision:** matched synthetic respondents identify the intended
buyer, problem, and current workflow, but cannot say what changes. Route to
the expression layer with a narrower articulation test. Do not claim the
underlying value is false.

**Alternative contradiction:** matched synthetic respondents understand the
words but consistently state that the named current workflow is not theirs.
Route to M1. The expression may be clear while the M1 alternative is still
wrong for this scope.

**Proof contradiction:** matched synthetic respondents understand the stated
difference but say the claimed outcome is not credible without evidence.
Route to KB-2's proof link. Do not add statistics, customer claims, or a
stronger headline.

**Blocked preference:** internal stakeholders prefer variant B. With no
matched respondents and no unaided-comprehension result, return `blocked`.
This is a design preference, not expression validation.

## Handoff and receipt

Persist exactly one `ExpressionValidationDecision` and one
`ExpressionValidationReceipt` at the self-referential fixture or run path.
The receipt mirrors the upstream snapshot, audience match, comprehension
statuses, preference status, primary failure, route, and decision. It records
the Wynter dossier, sample limit, refusal codes, and the explicit list of
claims that KB-7 did not establish: alternative, differentiated value, and
market frame. Downstream users may use a supported expression only at the
recorded audience and situation scope.
