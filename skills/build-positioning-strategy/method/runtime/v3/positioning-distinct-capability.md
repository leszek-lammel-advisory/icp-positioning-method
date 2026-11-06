---
domain: positioning-strategy
runtime: positioning-distinct-capability
module: V3-DC
version: 3
status: proposed
depends_on: [V3-readiness, M1]
load:
  - ../../08-distinct-capability-identification-v3.md
  - ../../source-claim-gap-matrix-v3.md
  - ../../sources/dunford-obviously-awesome-second-edition-dossier.md
---

# V3 Runtime: Distinct Capability

## Entry

Enter when the user asks what the product or company can do differently from a
real alternative, or when KB-2 needs a capability record. Require one `ready`
readiness record and one same-scope M1 record with an `observed` alternative.

## Non-entry

Do not enter for a feature inventory, benefit statement, value proposition,
best-fit customer, market style, ROI claim, proof claim, or copy request. Route
those tasks to their owner after capability comparison is complete.

## First move

Resolve the readiness and M1 IDs, then place one atomic capability behavior
beside one observed alternative behavior. Do not begin with adjectives or
customer outcomes.

## Exact runtime inputs

- `readiness_run_id` with branch `ready`;
- `m1_run_id`, buyer, situation, observed alternative, and evidence refs;
- `capability_inventory_ids` with current object/version and atomic behaviors;
- `alternative_evidence_ids` for the same comparison scope;
- request ID and requested capability lane.

## Evidence, source, and field rules

Product or operating evidence can establish possession. Alternative evidence
must establish the comparison; silence, a vendor page omission, or internal
belief does not establish absence. OA2-03 defines the method and cannot supply
either fact. Load-bearing source content the dossier does not cover receives `SOURCE_GAP`.

Every behavior, scope field, possession finding, and alternative comparison is
`known`, `inferred`, `unknown`, or `conflicted`. Comparative state is separate:
`supported`, `hypothesis`, `research_needed`, or `blocked`.

## Legal outcomes

- `supported_capability`: at least one row is `supported`, every admitted row
  has direct comparison evidence, and the terminal status is `decision_ready`.
- `capability_hypothesis`: at least one row is a bounded `hypothesis`, no row
  is presented as supported, and the terminal status is `owner_review`.
- `research_needed`: missing possession, alternative behavior, or scope parity
  can be resolved through named evidence.
- `blocked`: the request substitutes the M1 alternative, combines incompatible
  scopes, demands a contradicted comparison, or treats benefit as capability.

## Procedure

1. Copy upstream scope and alternative without strengthening them.
2. Split inventories into atomic observable behaviors.
3. Test company possession and alternative behavior independently.
4. Apply specificity, contrast, scope-parity, and capability/value-separation
   tests from the handbook.
5. Record one row per capability-alternative pair, including contrary evidence.
6. Emit the outcome, terminal status, and a KB-2 handoff containing only admitted rows.

## Diagnostic routing codes

These proposed codes explain runtime routing. The release-level hard refusal
for this decision type is `UNSOURCED_CAPABILITY_CLAIM` in SKILL.md.

- `READINESS_NOT_READY`
- `M1_OBSERVED_ALTERNATIVE_REQUIRED`
- `UPSTREAM_SCOPE_MISMATCH`
- `CAPABILITY_NOT_ATOMIC`
- `CAPABILITY_POSSESSION_NOT_EVIDENCED`
- `ALTERNATIVE_BEHAVIOR_NOT_EVIDENCED`
- `ABSENCE_OF_EVIDENCE_NOT_DISTINCTNESS`
- `ALTERNATIVE_SUBSTITUTION_FORBIDDEN`
- `INCOMPATIBLE_COMPARISON_SCOPE`
- `BENEFIT_IS_NOT_CAPABILITY`
- `KNOWN_COMPARISON_CONTRADICTION`
- `OWNER_SCOPE_DECISION_REQUIRED`
- `SOURCE_GAP`

## Record shape: `DistinctCapabilityDecision`

```yaml
run_id: string
record_type: DistinctCapabilityDecision
module_version: distinct-capability/v3
input_refs: {readiness_run_id: string, m1_run_id: string, capability_inventory_ids: [string], alternative_evidence_ids: [string]}
scope: {positioning_object: string, object_version: string, buyer: string, situation: string}
baseline_alternative: {value: string, m1_state: observed, field_status: known|inferred|unknown|conflicted, evidence_refs: [string]}
capability_records:
  - capability_id: string
    behavior: {value: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
    company_possession: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
    alternative_behavior: {value: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
    scope_parity: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
    comparative_claim: string
    comparative_state: supported|hypothesis|research_needed|blocked
    counterevidence_refs: [string]
    prohibited_downstream_claims: [string]
    next_evidence_request: string
outcome: supported_capability|capability_hypothesis|research_needed|blocked
terminal_status: decision_ready|owner_review|research_needed|blocked
kb2_handoff_capability_ids: [string]
refusal_codes: [string]
prohibited_inferences: [string]
next_action: {action: string, owner: string, evidence_needed: [string]}
source_refs: [OA2-03]
```

## Completion

Complete when every submitted capability has one comparative state, one
evidence path, and one prohibition where not supported. The output is a
proposed producer record; it does not prove KB-2 value or V3 fixture maturity.

## Downstream prohibitions

KB-2 must preserve comparative state. No downstream receiver may infer buyer
importance, mechanism, outcome, proof, best fit, market style, adoption,
leadership, or copy from this record alone.
