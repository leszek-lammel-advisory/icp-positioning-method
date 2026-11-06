---
domain: positioning-strategy
task_type: positioning-market-frame-choice
module: KB-3
version: 2
status: tested
depends_on: [M1, KB-2]
load:
  - ../03-market-frame-choice.md
  - ../sources/dunford-relative-value-dossier.md
  - ../sources/play-bigger-category-design-dossier.md
---

# Runtime Workflow: Market Frame Choice

## Admission and refusal

Require M1 buyer/situation and a KB-2 ledger. If either is absent, return
`research_needed` with `MISSING_UPSTREAM_INPUT`. Refuse `blocked` requests that
cite only founder preference, novelty, or category crowding with
`NOVELTY_OR_CROWDING_NOT_WARRANT`. Do not infer buyer
comprehension, current perception, adoption, or outcome proof from a label.

## Steps

1. Build one candidate-frame ledger for each existing frame and, only if
   warranted, one proposed new frame.
2. Attach provenance to every field. Label buyer language, inference, and
   seller assertion separately.
3. Apply the four handbook tests. Mark unknown fields `research_needed` rather
   than resolving them in prose.
4. Decide `existing_frame` only when comprehension, value fidelity, and
   expectation fit are supported with no material contradiction.
5. Decide `category_creation_hypothesis` only when new-frame warrant,
   conditioning capacity, and all expectation fields are supported. Any unknown
   capability, buyer, or price expectation returns `research_needed`. Never
   output `category_created`.
6. Record the exact reversal condition and downstream prohibitions.

## Required output: `KB3FrameDecision`

```yaml
fixture_or_run_id: string
module_version: "KB-3/v2"
input_refs: {m1_run_id: string, kb2_run_id: string, frame_evidence_ids: [string], capacity_evidence_ids: [string]}
scope: {buyer: string, situation: string}
candidates:
  - frame: string
    type: existing|new
    state: supported|hypothesis|research_needed|blocked
    evidence: [{id: string, type: buyer_language|buyer_research|product_evidence|company_plan|seller_assertion|inference, claim: string}]
    comparison_activated: string
    expectations:
      capabilities: {value: string, state: supported|hypothesis|research_needed|blocked, evidence: [{id: string, type: string, claim: string}]}
      buyer: {value: string, state: supported|hypothesis|research_needed|blocked, evidence: [{id: string, type: string, claim: string}]}
      price_logic: {value: string, state: supported|hypothesis|research_needed|blocked, evidence: [{id: string, type: string, claim: string}]}
    value_fidelity: supported|hypothesis|research_needed|blocked
    contradictions: [string]
    reversal_condition: string
decision: existing_frame|category_creation_hypothesis|research_needed|blocked
reasoning: string
refused_assumptions: [string]
prohibited_downstream_claims: [string]
next_evidence_request: string
```

## Required receipt

```yaml
receipt_id: "KB3-R-<fixture_or_run_id>"
module_version: "KB-3/v2"
source_dossier_versions: [SRC-DUNFORD-RELATIVE-VALUE-20260711, SRC-PLAY-BIGGER-CATEGORY-DESIGN-20260711]
input_refs: {m1_run_id: string, kb2_run_id: string, frame_evidence_ids: [string], capacity_evidence_ids: [string]}
candidate_states: [{frame: string, state: supported|hypothesis|research_needed|blocked, evidence: [{id: string, type: string, claim: string}]}]
decision: existing_frame|category_creation_hypothesis|research_needed|blocked
refusal_codes: [MISSING_UPSTREAM_INPUT|NOVELTY_OR_CROWDING_NOT_WARRANT|EXPECTATION_FIT_NOT_EVIDENCED|KNOWN_FRAME_CONTRADICTION]
escalation: "none | request_buyer_research | request_company_capacity_evidence | route_to_M1_or_KB2"
persist_to: "runs/<fixture_or_run_id>.md"
```
