---
domain: positioning-strategy
task_type: positioning-expression-validation
module: KB-7
version: 1
status: tested
depends_on: [M1, KB-2, KB-3]
load:
  - ../07-expression-validation.md
  - ../sources/wynter-perception-validation-dossier.md
---

# Runtime Workflow: Expression Validation

## Admission

Load one declared expression variant, a defined audience and situation, and
an immutable upstream snapshot from M1, KB-2, and KB-3. The snapshot may be a
hypothesis but must retain its original state and evidence references. If an
input is absent, record it as absent and do not reconstruct an alternative,
value, or frame from the expression or respondent answers.

Do not start with an internal comparison, a generic panel, or a preference
vote. Those may inform drafting taste but cannot emit a KB-7 validation
decision. Every respondent record must identify whether it matches the stated
audience and situation.

## Procedure

1. Screen respondents against the declared audience and situation. If no
   matched respondent exists, return `blocked` and request relevant research.
2. Ask unaided questions in this order: intended audience, problem, current
   alternative/comparison, and offered difference. Capture each answer as a
   separate structured evidence item.
3. Ask for proof or credibility concerns, and then frame fit if the test is
   testing the supplied frame's interpretation. Keep those outcomes separate
   from word comprehension.
4. Collect preference only after every required comprehension field has been
   completed. A preference asked earlier is a blocked sequence, even when it
   has a winner.
5. Determine the earliest failure: audience design, M1 alternative,
   KB-2 value/proof, KB-3 frame, or expression. Do not revise copy until the
   result is an expression-layer failure.
6. Emit the paired decision and receipt. List alternative, differentiated
   value, and market frame as not established by the test in both artifacts.

## Required output: `ExpressionValidationDecision`

```yaml
fixture_or_run_id: string
module_version: KB-7/v1
input_refs: {m1_run_id: string, kb2_run_id: string, kb3_run_id: string, expression_variant_ids: [string], respondent_evidence_ids: [string]}
scope: {audience: string, situation: string}
upstream_hypothesis:
  alternative: {claim: string, state: observed|candidate|excluded|unknown, evidence_refs: [string]}
  differentiated_value: {claim: string, state: supported|hypothesis|research_needed|blocked, evidence_refs: [string]}
  market_frame: {claim: string, state: supported|hypothesis|research_needed|blocked, evidence_refs: [string]}
expression_variant: {id: string, text: string}
evidence_ledger: [{id: string, source_id: string, provenance: respondent|internal, audience_match: matched|not_matched|not_assessed, stage: audience_screen|unaided_comprehension|credibility_probe|preference, supports: [audience_match|audience_recognition|problem_relevance|comparison_clarity|difference_comprehension|credibility|frame_fit|preference], result: correct|incorrect|neutral|preferred|not_preferred|not_answered, claim: string}]
audience_match: {status: matched|not_matched|not_assessed, evidence_ids: [string]}
comprehension:
  audience_recognition: {status: pass|fail|not_tested, evidence_ids: [string]}
  problem_relevance: {status: pass|fail|not_tested, evidence_ids: [string]}
  comparison_clarity: {status: pass|fail|not_tested, evidence_ids: [string]}
  difference_comprehension: {status: pass|fail|not_tested, evidence_ids: [string]}
  credibility: {status: pass|fail|not_tested, evidence_ids: [string]}
  frame_fit: {status: pass|fail|not_tested, evidence_ids: [string]}
preference: {status: not_collected|collected, evidence_ids: [string], winner: string|null}
primary_failure: none|expression|audience|alternative|value_or_proof|frame|sequence
decision: expression_supported|expression_revise|upstream_research_needed|blocked
route: expression_layer|research_design|M1|KB-2|KB-3
assertions_not_established: [alternative, differentiated_value, market_frame]
next_evidence_request: string
```

## Required receipt: `ExpressionValidationReceipt`

```yaml
receipt_id: KB7-R-<fixture_or_run_id>
module_version: KB-7/v1
source_dossier_versions: [SRC-WYNTER-PERCEPTION-VALIDATION-20260711]
respondent_scope_limit: string
upstream_hypothesis: {alternative: object, differentiated_value: object, market_frame: object}
audience_match: matched|not_matched|not_assessed
comprehension_status: {audience_recognition: pass|fail|not_tested, problem_relevance: pass|fail|not_tested, comparison_clarity: pass|fail|not_tested, difference_comprehension: pass|fail|not_tested, credibility: pass|fail|not_tested, frame_fit: pass|fail|not_tested}
preference_status: not_collected|collected
primary_failure: none|expression|audience|alternative|value_or_proof|frame|sequence
decision: expression_supported|expression_revise|upstream_research_needed|blocked
route: expression_layer|research_design|M1|KB-2|KB-3
refusal_codes: [string]
assertions_not_established: [alternative, differentiated_value, market_frame]
persist_to: "runs/<fixture_or_run_id>.md"
```

## Hard refusals

- `INTERNAL_PREFERENCE_NOT_BUYER_VALIDATION`: internal preference is not buyer
  expression evidence.
- `MATCHED_AUDIENCE_REQUIRED`: an unmatched respondent cannot validate the
  stated scope.
- `COMPREHENSION_BEFORE_PREFERENCE_REQUIRED`: no preference conclusion before
  unaided comprehension is completed.
- `PREFERENCE_CANNOT_ESTABLISH_UPSTREAM`: preference cannot establish an
  alternative, differentiated value, or market frame.
- `ALTERNATIVE_CONTRADICTION_ROUTE_TO_M1`,
  `VALUE_OR_PROOF_CONTRADICTION_ROUTE_TO_KB2`, and
  `FRAME_CONTRADICTION_ROUTE_TO_KB3`: route to the earliest owner and do not
  write a replacement claim.
