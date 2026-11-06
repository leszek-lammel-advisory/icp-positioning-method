---
domain: positioning-strategy
task_type: positioning-adoption-beachhead
module: KB-4
version: 2
status: tested
depends_on: [M1, KB-2, KB-3]
load: [../04-adoption-and-beachhead.md, ../sources/moore-adoption-beachhead-dossier.md]
---

# Runtime Workflow: Adoption and Beachhead

Require M1, KB-2, and KB-3 runs plus a group evidence inventory. Missing
upstream decisions produce `research_needed`, never an invented segment. Apply
the six-test ledger in the handbook. Use `blocked` for novelty-only logic,
known ignored whole-product gaps, or reachability-only beachheads.

Apply the six-test aggregation rule in the handbook. A beachhead hypothesis
requires every test including expansion path to be `supported`; otherwise it is
`research_needed` unless a test is blocked. The only early exception is a
`standard_segment_hypothesis`: buyer evidence must explicitly establish no
discontinuity and establish group coherence beyond reachability. Record that
evidence in `standard_segment_basis`; do not call reachability-only evidence a
standard segment.

```yaml
BeachheadDecision:
  fixture_or_run_id: string
  module_version: KB-4/v2
  input_refs: {m1_run_id: string, kb2_run_id: string, kb3_run_id: string, group_evidence_ids: [string]}
  scope: {buyer_group: string, application: string}
  tests:
    discontinuity: {state: supported|hypothesis|research_needed|blocked|not_applicable, evidence_refs: [string], reasoning: string}
    shared_situation: {state: supported|hypothesis|research_needed|blocked|not_applicable, evidence_refs: [string], reasoning: string}
    whole_product: {state: supported|hypothesis|research_needed|blocked|not_applicable, evidence_refs: [string], gaps: [string], owners: [string]}
    reference_transfer: {state: supported|hypothesis|research_needed|blocked|not_applicable, evidence_refs: [string], next_group: string}
    repeatability: {state: supported|hypothesis|research_needed|blocked|not_applicable, evidence_refs: [string], reasoning: string}
    expansion_path: {state: supported|hypothesis|research_needed|blocked|not_applicable, evidence_refs: [string], next_group: string, transfer_condition: string}
  decision: beachhead_hypothesis|standard_segment_hypothesis|research_needed|blocked
  standard_segment_basis: {explicit_discontinuity_absent: boolean, coherence_evidence_refs: [string], coherence_reasoning: string} # required only for standard_segment_hypothesis
  refused_assumptions: [string]
  reversal_condition: string
  next_evidence_request: string
BeachheadReceipt:
  receipt_id: string
  source_dossier_versions: [SRC-MOORE-ADOPTION-BEACHHEAD-20260711]
  test_ledger: [{test: string, state: string, evidence_refs: [string]}]
  decision: string
  refusal_codes: [MISSING_UPSTREAM_INPUT|NOVELTY_IS_NOT_ADOPTION_EVIDENCE|REACHABILITY_ONLY_NOT_BEACHHEAD|KNOWN_WHOLE_PRODUCT_GAP_IGNORED|REFERENCE_TRANSFER_NOT_PROVEN|UNBOUNDED_BESPOKE_DELIVERY]
  escalation: none|request_group_research|request_delivery_evidence|route_upstream
  persist_to: "runs/<fixture_or_run_id>.md"
```
