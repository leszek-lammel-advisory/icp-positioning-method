---
domain: positioning-strategy
runtime: positioning-best-fit-customer
module: V3-BFC
version: 3
status: proposed
depends_on: [V3-readiness, M1, V3-DC, KB-2]
load:
  - ../../09-best-fit-customer-selection-v3.md
  - ../../source-claim-gap-matrix-v3.md
  - ../../sources/dunford-obviously-awesome-second-edition-dossier.md
---

# V3 Runtime: Best-Fit Customer

## Entry

Enter when the request asks which customers care most about an admitted KB-2
value chain and can plausibly buy and be reached. Require same-scope readiness,
M1, distinct-capability, and KB-2 records.

## Non-entry

Do not use this runtime for a broad ICP, account ranking, TAM estimate,
prospecting list, persona, adoption-stage diagnosis, or beachhead selection.
KB-4 remains the only owner of beachhead and adoption logic.

## First move

Copy the exact KB-2 buyer outcome and evidence state. Then ask which observed
customer characteristic or situation makes that outcome materially more
important. Do not begin with industry, employee count, title, or channel.

## Exact runtime inputs

- `readiness_run_id` with branch `ready`;
- same-scope `m1_run_id` and observed alternative;
- `distinct_capability_run_id` and capability IDs admitted by KB-2;
- `kb2_run_id` with full link ledger and decision;
- `customer_evidence_ids` with source identity and situation;
- `buying_evidence_ids` and `reachability_evidence_ids` kept separate;
- candidate-group request and proposed exclusions, if supplied.

## Evidence, source, and field rules

OA2-04 defines value-linked selection, buyability, and reachability checks. It
does not supply a customer fact. Every group characteristic, causal value link,
buying condition, access route, and exclusion is `known`, `inferred`,
`unknown`, or `conflicted` with evidence refs. A KB-2 hypothesis remains a
hypothesis and can support a research lane only; it cannot support a declared
best-fit choice.

## Legal outcomes

- `best_fit_supported`: value acuity, alternative consistency, buying, and
  access are supported; exclusions are explicit; no material conflict remains.
- `best_fit_hypothesis`: value acuity and alternative consistency are
  supported while buying or access remains a bounded inference; the terminal
  status is `owner_review`.
- `research_needed`: one named factual gap could change membership or status.
- `blocked`: the selection rests on firmographics or reachability alone, uses a
  blocked/research-needed KB-2 chain as established value, merges incompatible
  groups, or claims a beachhead without KB-4.

## Procedure

1. Verify upstream ID resolution, scope parity, and state preservation.
2. Build candidate groups from customer situations and value-acuity evidence.
3. Link every retained characteristic to value importance, buying feasibility,
   access, or an explicit exclusion.
4. Split lanes when alternative, value, proof expectation, or buying path
   materially differs.
5. Evaluate ability to buy and reach after value acuity; keep the two evidence
   classes separate.
6. Record exclusions, conflicts, reversal conditions, one outcome, and one terminal status.

## Diagnostic routing codes

These proposed codes explain runtime routing. The release-level hard refusal
for this decision type is `CUSTOMER_FIT_FROM_FIRMOGRAPHICS_ONLY` in SKILL.md.

- `READINESS_NOT_READY`
- `M1_OBSERVED_ALTERNATIVE_REQUIRED`
- `DISTINCT_CAPABILITY_RECORD_REQUIRED`
- `KB2_VALUE_RECORD_REQUIRED`
- `KB2_VALUE_NOT_ESTABLISHED`
- `UPSTREAM_SCOPE_MISMATCH`
- `FIRMOGRAPHICS_ONLY_NOT_BEST_FIT`
- `REACHABILITY_ONLY_NOT_BEST_FIT`
- `VALUE_ACUITY_NOT_EVIDENCED`
- `BUYING_FEASIBILITY_NOT_EVIDENCED`
- `ACCESS_ROUTE_NOT_EVIDENCED`
- `INCOMPATIBLE_CUSTOMER_LANES_REQUIRE_SPLIT`
- `BEACHHEAD_CLAIM_ROUTE_TO_KB4`
- `OWNER_PRIORITY_DECISION_REQUIRED`
- `SOURCE_GAP`

## Record shape: `BestFitCustomerDecision`

```yaml
run_id: string
record_type: BestFitCustomerDecision
module_version: best-fit-customer/v3
input_refs: {readiness_run_id: string, m1_run_id: string, distinct_capability_run_id: string, kb2_run_id: string, customer_evidence_ids: [string], buying_evidence_ids: [string], reachability_evidence_ids: [string]}
scope: {positioning_object: string, buyer_situation: string, market_or_geography: string}
upstream_snapshot:
  alternative: {claim: string, state: observed, evidence_refs: [string]}
  distinct_capabilities: [{capability_id: string, state: supported|hypothesis, evidence_refs: [string]}]
  value: {claim: string, state: supported|hypothesis|research_needed|blocked, evidence_refs: [string]}
candidate_lanes:
  - lane_id: string
    group_description: string
    characteristics: [{value: string, status: known|inferred|unknown|conflicted, evidence_refs: [string], why_it_matters: string}]
    value_acuity: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
    alternative_consistency: {status: known|inferred|unknown|conflicted, evidence_refs: [string]}
    ability_to_buy: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
    ability_to_reach: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
    exclusions: [{description: string, status: known|inferred|unknown|conflicted, evidence_refs: [string], reason: string}]
    counterevidence_refs: [string]
    reversal_condition: string
selected_lane_id: string|null
outcome: best_fit_supported|best_fit_hypothesis|research_needed|blocked
terminal_status: decision_ready|owner_review|research_needed|blocked
refusal_codes: [string]
assertions_not_established: [purchase_intent, market_size, adoption_stage, beachhead, repeatability, category_leadership]
prohibited_inferences: [string]
next_action: {action: string, owner: string, evidence_needed: [string]}
source_refs: [OA2-04]
```

## Completion

Complete when every candidate lane has causal characteristics, buying/access
states, exclusions, and a reversal condition, and the run ends in one branch.
The output remains a hypothesis or route; it is not a KB-4 decision and does
not promote this proposed runtime.

## Downstream prohibitions

No receiver may infer market size, purchase intent, adoption stage, beachhead,
reference transfer, repeatability, expansion, category leadership, or message
validation. KB-3 V3 must preserve the lane and all evidence states.
