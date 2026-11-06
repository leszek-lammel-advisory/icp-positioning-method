# Positioning Decision Packet Contract

Return one packet and one matching receipt.

## Packet fields

| Field | Contract |
|---|---|
| packet_id | Unique string. |
| decision_id | Unique string shared with the receipt. |
| request_type | readiness, alternatives, distinct_capability, differentiated_value, best_fit_customer, market_style, adoption, perception, switching, expression, pitch_validation, stewardship, downstream_route, or wrapper_failure. |
| scope | positioning_object, buyer, and situation. |
| evidence | Array of id, source_ref, claim, and state. State is known, inferred, unknown, or conflicted. |
| decision.enum | The runtime's closed decision enum. |
| decision.terminal_status | decision_ready, research_needed, owner_review, route_downstream, or blocked. |
| decision.reasoning | Evidence-linked explanation. |
| refusal_codes | Release hard refusals only. Empty unless the packet blocks one prohibited release ask; then exactly one of UNSOURCED_CAPABILITY_CLAIM, CUSTOMER_FIT_FROM_FIRMOGRAPHICS_ONLY, MARKET_STYLE_FROM_NOVELTY_ONLY, or COPY_RESPONSE_AS_POSITIONING_PROOF. |
| diagnostic_codes | Runtime and wrapper routing codes only. Empty for a release hard refusal. Runtime/V2-native blocks carry exactly one owning-runtime code without translation; a tested V2 blocked result with no native closed code carries `V2_NATIVE_BLOCK_NO_CODE` and names its native rule in reasoning. Packet assembly failure carries exactly `PACKET_CONTRACT_FAILED`. A non-blocked research or owner route may carry at most one diagnostic code. |
| route_artifacts | Array of complete module records created or consumed by the route. A dependent decision must expose its required upstream records by ID. Market-style packets include one complete artifact with `record_type: MarketStyleDecision`, five upstream IDs, and exactly three candidate ledgers. |
| prohibited_inferences | Claims the receiver must not make. |
| permitted_use | Exact receiver permission. |
| residual_limit | What remains unproven. |
| receiver | Named role, operator, or downstream route. |
| next_action | One legal action. |
| next_action_owner | Named owner. |
| reversal_condition | Evidence that could change the decision. |

## Receipt fields

| Field | Contract |
|---|---|
| receipt_id | Unique string. |
| packet_id | Exact packet ID. |
| decision_id | Exact decision ID. |
| route_paths | Runtime paths actually loaded. |
| source_claim_ids | Exact method claim IDs applied, in first-use order. Use claim IDs such as `OA2-05`, `DUN-C1`, `PB-C1`, or `WYN-C1`; never source IDs such as `SRC-*`, dossier IDs, URLs, or runtime paths. Empty when no method claim is applied. |
| evidence_ids | Exact packet evidence IDs. |
| terminal_status | Exact packet status. |
| refusal_codes | Exact packet codes. |
| diagnostic_codes | Exact packet diagnostic codes. |
| route_artifact_ids | Exact IDs of packet route artifacts. |
| validator_state | passed, not_run, or failed. |
| maturity_ceiling | draft, structurally_valid, fixture_proven, live_calibrated, production_accepted, revise, deprecated, or blocked. |

Packet and receipt IDs, decision ID, terminal status, refusal codes, diagnostic codes, route-artifact IDs, and evidence IDs must agree. A schema-valid packet is not proof that the market claim is true.

## Deterministic source-claim provenance

Read every path in an entered runtime's `load` list before applying a claim
from it. A claim may appear in `source_claim_ids` only when its owning dossier
or claim matrix was actually read. Runtime paths belong in `route_paths`, not
`source_claim_ids`.

For a packet with route artifacts, `source_claim_ids` is the stable first-use
union of every artifact's `source_refs`, plus an active router claim when it
was applied. Market-style chain closure applies `OA2-02` and uses this order:
readiness, router, M1 adapter, distinct capability, KB-2, best fit, active
market style. Remove duplicates without reordering. For a packet with no route
artifact, use only the claim IDs that support the active gate or route.

| Active gate or route | Claim IDs when applied |
|---|---|
| Readiness or scope | `OA2-01` |
| Dependency routing | `OA2-02` |
| Distinct capability | `OA2-03` |
| Best-fit customer | `OA2-04` |
| Market style | `OA2-05`; add `PB-C1`, `PB-C2`, and `PB-C3` when evaluating or refusing new-game logic |
| Qualified-pitch validation | `OA2-06`; add `WYN-C1` and `WYN-C3` when classifying expression evidence |
| Approved-positioning handoff | `OA2-07` |
| Stewardship or change review | `OA2-08` |
| V2 M1 actual alternatives | `DUN-C1` |
| Market-context comparison | `DUN-C4` |
| Approved-positioning messaging handoff | `OA2-07` |
| Pure downstream routing or packet wrapper failure | `[]` |

Release hard refusals use these exact claim lists: unsourced capability
`[OA2-03]`; firmographics-only best fit `[OA2-04]`; novelty-only market style
`[OA2-05, PB-C1, PB-C2, PB-C3]`; copy response as positioning proof
`[OA2-06, WYN-C1, WYN-C3]`.

This table is a provenance rule, not permission to cite every listed claim.
Only include a listed claim when the reasoning or a serialized route artifact
actually uses it.

`OA2-02` is applied only when the decision depends on preserving or testing the
cross-module dependency chain. Reading the router or selecting a single module
does not, by itself, apply `OA2-02`; do not add it to readiness, downstream,
stewardship-admission, hard-refusal, wrapper-failure, or standalone M1
receipts.

## Canonical YAML placement

The following fields are top-level packet siblings. Preserve this indentation:

```yaml
packet_id: string
decision_id: string
request_type: string
scope: {}
evidence: []
decision:
  enum: string
  terminal_status: string
  reasoning: string
refusal_codes: []
diagnostic_codes: []
route_artifacts: []
prohibited_inferences: []
permitted_use: string
residual_limit: string
receiver: string
next_action: string
next_action_owner: string
reversal_condition: string
```

Never place `refusal_codes`, `diagnostic_codes`, or `route_artifacts` under
`decision`.

## V2 M1 blocked wrapper

When V2 M1 emits its native blocked decision but has no closed machine record,
include exactly this complete route artifact:

```yaml
record_id: string
record_type: V2M1BlockedDecision
runtime_version: positioning-alternatives-diagnosis/v2
decision_mode: blocked_decision
scope: {positioning_object: string, buyer: string, situation: string}
evidence_states:
  - {evidence_id: string, state: known|inferred|unknown|conflicted, source_ref: string}
alternatives:
  - {name: string, status: candidate|unknown|excluded, evidence_refs: [string]}
missing_customer_evidence: [string]
native_refusal_rule: string
diagnostic_code: V2_NATIVE_BLOCK_NO_CODE
prohibited_inferences: [string]
next_action: {action: string, owner: string, evidence_needed: [string]}
source_refs: [string]
```

No alternative in this wrapper may be `observed` without direct buyer,
win/loss, usage, workflow, or sales evidence.
