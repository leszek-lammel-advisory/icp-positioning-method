---
domain: positioning-strategy
task_type: positioning-differentiated-value
module: KB-2
status: tested
version: 2
depends_on: [M1]
load:
  - ../02-differentiated-value.md
  - ../sources/dunford-relative-value-dossier.md
---

# Runtime Workflow: Differentiated Value

## Admission check

Run only with an M1 handoff containing a single `observed` baseline alternative
for the same buyer and situation. If the M1 handoff exists but its alternatives
are only `candidate`, `excluded`, or `unknown`, emit `research_needed` with
`refusal_code: M1_BASELINE_NOT_OBSERVED` and route to M1. If the M1 handoff is
absent or its buyer/situation is incompatible, emit `blocked` with the same
code. Do not invent a baseline from category knowledge or a feature list.

## Execution

1. Copy the M1 run ID, module version, baseline text, buyer/situation, and
   evidence refs without strengthening them.
2. Record one capability difference and its product evidence refs.
3. Record the causal mechanism and buyer outcome separately. Assign each a
   canonical state using the KB-2 matrix.
4. Classify proof as `product_demo`, `seller_assertion`, `customer_testimony`,
   `usage_observation`, `outcome_measurement`, `study`, or `absent`.
5. Apply the decision order: contradiction/required unsupported performance
   claim -> `blocked`; insufficient baseline/difference/context ->
   `research_needed`; intact but unproven mechanism/outcome -> `hypothesis`;
   all supported -> `supported`.
6. Add a prohibition for every non-supported link. State the smallest evidence
   request that could change the decision.

## Required output: `KB2ValueDecision`

```yaml
fixture_or_run_id: string
module_version: "KB-2/v2"
input_refs:
  m1_run_id: string
  capability_record_ids: [string]
  evidence_inventory_ids: [string]
scope:
  buyer: string
  situation: string
links:
  baseline: {claim: string, state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], reasoning: string, prohibited_downstream_claims: [string]}
  difference: {claim: string, state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], reasoning: string, prohibited_downstream_claims: [string]}
  mechanism: {claim: string, state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], reasoning: string, prohibited_downstream_claims: [string]}
  outcome: {claim: string, state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], reasoning: string, prohibited_downstream_claims: [string]}
  proof: {claim: string, state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], reasoning: string, proof_class: string, prohibited_downstream_claims: [string]}
decision: supported|hypothesis|research_needed|blocked
refused_assumptions: [string]
prohibited_downstream_claims: [string]
next_evidence_request: string
```

## Required receipt: `KB2ValueReceipt`

```yaml
receipt_id: "KB2-R-<fixture_or_run_id>"
module_version: "KB-2/v2"
source_dossier_versions: ["SRC-DUNFORD-RELATIVE-VALUE-20260711"]
input_refs: {m1_run_id: string, capability_record_ids: [string], evidence_inventory_ids: [string]}
link_evidence_ledger:
  - {link: baseline|difference|mechanism|outcome|proof, state: supported|hypothesis|research_needed|blocked, evidence_refs: [string], prohibited_downstream_claims: [string]}
decision: supported|hypothesis|research_needed|blocked
refusal_codes: [string]
escalation: "none | route_to_M1 | request_customer_evidence | request_product_evidence"
persist_to: "runs/<run_id>.md"
```

## Refusals

Refuse feature-only value claims, baseline substitution, demo-to-outcome
inference, performance claims without appropriately scoped outcome evidence,
and a request to convert a hypothesis into copy. The wording "buyers retained
the workflow" does not reveal *why* they retained it.
