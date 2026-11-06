---
domain: positioning-strategy
task_type: positioning-demand-switching
module: KB-6
version: 3
status: tested
depends_on: [M1]
load: [../06-demand-side-switching.md, ../sources/moesta-demand-side-dossier.md]
---

# Runtime Workflow: Demand-Side Switching

Read the handbook and Moesta dossier before every run. Require an M1 run with
an observed alternative and a typed buyer-evidence inventory. A missing M1
alternative returns `research_needed`, `MISSING_M1_ALTERNATIVE`, and
`route_to_M1`; it cannot support `before_state`. A request with no buyer
situation that asks for motives, stage, or switching likelihood from
firmographics, title, web visits, or seller assumptions returns `blocked` with
`MOTIVE_INFERENCE_WITHOUT_BUYER_EVIDENCE`.

The output is a `DemandProgressDecision` plus a `DemandProgressReceipt`.
Persist both objects in exactly two closed YAML fences at the receipt path. The
decision may support a force only with its named evidence and permitted
provenance. The receipt must reproduce all six force states and evidence refs,
the stage, the bottleneck, the intervention, and the decision. `supported`
never means inferred from a persona, company, product category, retained tool,
or feature exposure.

## Deterministic boundaries

| Stage | Required direct evidence | Permitted bottleneck | Required intervention |
|---|---|---|---|
| `no_first_thought` | a buyer record says no recognized struggle or search | `no_recognized_struggle` | `research_situation` |
| `passive_looking` | struggling moment and push, plus no committed search | `unclear_desired_progress` | `clarify_progress_and_before_state` |
| `active_looking` | buyer explores alternatives or evaluation criteria | `evaluation_clarity` or `implementation_anxiety` | `map_alternatives_differences_and_proof` or `provide_rollout_risk_proof` respectively |
| `deciding` | buyer evaluates a specific option, trade-off, or named risk | `implementation_anxiety` or `habit_attachment` | `address_named_risk_or_habit` |
| `first_use` / `ongoing_use` | direct use behavior | `delivery_or_outcome` | `support_delivery_or_capture_outcomes` |

For `no_first_thought`, include
`NO_RECOGNIZED_STRUGGLE_NO_VENDOR_COMPARISON` when a comparison or vendor
intervention was requested. For a requested feature deck against a supported
implementation-anxiety bottleneck, include
`REQUESTED_FEATURE_DECK_NOT_MATCHED_TO_EVIDENCED_BOTTLENECK`. `unknown` stage
may not be used to hide a motive inference.

```yaml
DemandProgressDecision:
  fixture_or_run_id: string
  module_version: KB-6/v3
  input_refs: {m1_run_id: string, buyer_evidence_ids: [string]}
  scope: {buyer: string, situation: string}
  evidence_ledger: [{id: string, record_class: buyer_interview|buyer_behavior|m1_alternative|firmographics|seller_assertion|internal_strategy, provenance: buyer|M1|firmographic|seller|internal, fact: string, supports: [force-or-stage]}]
  forces:
    struggling_moment: {state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], claim: string}
    before_state: {state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], claim: string}
    push: {state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], claim: string}
    pull: {state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], claim: string}
    anxiety: {state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], claim: string}
    habit: {state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], claim: string}
  stage: no_first_thought|passive_looking|active_looking|deciding|first_use|ongoing_use|unknown
  stage_evidence_refs: [string]
  bottleneck: no_recognized_struggle|unclear_desired_progress|evaluation_clarity|implementation_anxiety|habit_attachment|delivery_or_outcome|missing_m1_alternative|unknown
  intervention: research_situation|clarify_progress_and_before_state|map_alternatives_differences_and_proof|provide_rollout_risk_proof|address_named_risk_or_habit|support_delivery_or_capture_outcomes|route_to_M1|request_buyer_interview
  decision: intervention_hypothesis|research_needed|blocked
  prohibited_claims: [string]
  disconfirming_observation: string
DemandProgressReceipt:
  receipt_id: string
  module_version: KB-6/v3
  source_dossier_versions: [SRC-MOESTA-DEMAND-SIDE-20260711]
  force_ledger: [{force: string, state: string, evidence_refs: [string]}]
  stage: string
  stage_evidence_refs: [string]
  bottleneck: string
  intervention: string
  decision: string
  refusal_codes: [MOTIVE_INFERENCE_WITHOUT_BUYER_EVIDENCE|MISSING_M1_ALTERNATIVE|NO_RECOGNIZED_STRUGGLE_NO_VENDOR_COMPARISON|REQUESTED_FEATURE_DECK_NOT_MATCHED_TO_EVIDENCED_BOTTLENECK]
  escalation: none|request_buyer_interview|route_to_M1
  persist_to: "runs/<fixture_or_run_id>.md"

```
