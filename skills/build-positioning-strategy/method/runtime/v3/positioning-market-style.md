---
domain: positioning-strategy
runtime: positioning-market-style
module: KB-3
version: 3
status: proposed
depends_on: [V3-readiness, M1, V3-DC, KB-2, V3-BFC]
load:
  - ../../versions/kb-3-market-style-v3.md
  - ../../03-market-frame-choice.md
  - ../../source-claim-gap-matrix-v3.md
  - ../../sources/dunford-obviously-awesome-second-edition-dossier.md
  - ../../sources/play-bigger-category-design-dossier.md
---

# V3 Runtime: Market Style

## Entry

Enter when the user asks whether to compete in an established category, focus
on a narrower value-dense subsegment, or explore a new market game. Require a
ready scope and same-scope M1, distinct-capability, KB-2, and best-fit records.

## Non-entry

Do not enter to name a category from scratch, declare market leadership, choose
a KB-4 beachhead, repair missing value, infer current perception, or write
messaging. Founder preference, novelty, crowding, and a memorable label are not
admission evidence.

## First move

Copy the approved or proposed best-fit lane and KB-2 value state, then test the
most familiar established frame first. New-game work is considered only after
evidence shows why existing frames hide or distort the value.

## Exact runtime inputs

- `readiness_run_id` with branch `ready`;
- same-scope `m1_run_id`, `distinct_capability_run_id`, `kb2_run_id`, and
  `best_fit_customer_run_id`;
- V2 KB-3 frame evidence or candidate-frame evidence IDs;
- buyer comprehension and expectation evidence IDs;
- subsegment coherence and exclusion evidence IDs;
- company capacity evidence IDs for product, proof, sales, demand, time, and
  accepted risk;
- owner-decision record, when an actual style has already been approved.

## Evidence, source, and field rules

OA2-05 defines the three styles and their relative burden. Tested KB-3 V2 owns
existing-frame fidelity and new-frame warrant. Neither source supplies the
company's buyer understanding, subsegment coherence, capacity, or decision.

Every expectation, value-fidelity test, subsegment claim, capacity field,
burden, and owner decision is `known`, `inferred`, `unknown`, or `conflicted`
with source IDs. A source gap receives `SOURCE_GAP`; an owner choice can accept
burden but cannot turn unknown external evidence into known evidence.

## Legal branches

Only these branches are legal:

- `head_to_head`: one established category supports comprehension, value
  fidelity, expectation fit, and a credible reason to choose the offer.
- `big_fish_small_pond`: one value-linked subsegment is coherent and bounded,
  with explicit exclusions and credible focus capacity.
- `create_new_game_hypothesis`: existing frames materially fail, and problem
  POV, different solution logic, expectations, and conditioning capacity are
  supported. This never means `category_created`.
- `research_needed`: a discriminating field is unknown and has a named
  evidence request.
- `owner_review`: more than one style is evidence-compatible, actual style
  approval is requested, burden acceptance is missing, or material stakeholder
  conflict remains.
- `blocked`: upstream contradiction, novelty/crowding-only logic, leadership
  claim, ignored expectation conflict, or attempted owner bypass.

The first three branches are evidence-bounded recommendations unless the input
contains a separate explicit owner approval. They never create owner approval.

## Procedure

1. Verify upstream ID resolution, scope parity, and unchanged states.
2. Build one candidate ledger for each legal style.
3. Apply V2 buyer-comprehension, value-fidelity, expectation-fit, and new-frame
   warrant tests.
4. Apply value-linked subsegment coherence and exclusion tests to
   `big_fish_small_pond`; do not substitute reachability or KB-4 logic.
5. Record execution burden, capacity evidence, counterevidence, and reversal
   condition for every candidate.
6. Select one branch and preserve owner approval as a separate field.

## Diagnostic routing codes

These proposed codes explain runtime routing. The release-level hard refusal
for this decision type is `MARKET_STYLE_FROM_NOVELTY_ONLY` in SKILL.md.

- `READINESS_NOT_READY`
- `UPSTREAM_RECORD_MISSING`
- `UPSTREAM_SCOPE_MISMATCH`
- `KB2_VALUE_NOT_ESTABLISHED`
- `BEST_FIT_CUSTOMER_RECORD_REQUIRED`
- `BUYER_COMPREHENSION_NOT_EVIDENCED`
- `EXPECTATION_FIT_NOT_EVIDENCED`
- `KNOWN_FRAME_CONTRADICTION`
- `SUBSEGMENT_NOT_VALUE_LINKED`
- `SUBSEGMENT_COHERENCE_NOT_EVIDENCED`
- `REACHABILITY_ONLY_NOT_MARKET_STYLE`
- `NOVELTY_OR_CROWDING_NOT_WARRANT`
- `NEW_GAME_CAPACITY_NOT_EVIDENCED`
- `CATEGORY_CREATED_CLAIM_FORBIDDEN`
- `MARKET_LEADERSHIP_CLAIM_FORBIDDEN`
- `OWNER_STYLE_APPROVAL_REQUIRED`
- `MATERIAL_STYLE_CONFLICT`
- `SOURCE_GAP`

## Record shape: `MarketStyleDecision`

```yaml
run_id: string
record_type: MarketStyleDecision
module_version: KB-3/v3-market-style
input_refs: {readiness_run_id: string, m1_run_id: string, distinct_capability_run_id: string, kb2_run_id: string, best_fit_customer_run_id: string, frame_evidence_ids: [string], capacity_evidence_ids: [string], owner_decision_id: string|null}
scope: {positioning_object: string, best_fit_lane_id: string, buyer_situation: string, market_or_geography: string}
upstream_states: {alternative: observed, distinct_capability: supported|hypothesis, value: supported|hypothesis|research_needed|blocked, best_fit: best_fit_supported|best_fit_hypothesis|research_needed|blocked}
candidates:
  - style: head_to_head|big_fish_small_pond|create_new_game_hypothesis
    buyer_comprehension: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
    value_fidelity: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
    expectation_fit: {status: known|inferred|unknown|conflicted, evidence_refs: [string], contradictions: [string]}
    subsegment_coherence: {status: known|inferred|unknown|conflicted, evidence_refs: [string], exclusions: [string]}
    conditioning_capacity: {status: known|inferred|unknown|conflicted, evidence_refs: [string], owners: [string]}
    execution_burden: {status: known|inferred|unknown|conflicted, summary: string, evidence_refs: [string]}
    counterevidence_refs: [string]
    reversal_condition: string
recommended_style: head_to_head|big_fish_small_pond|create_new_game_hypothesis|null
owner_decision: {status: known|inferred|unknown|conflicted, decision: string|null, evidence_refs: [string]}
outcome: head_to_head|big_fish_small_pond|create_new_game_hypothesis|research_needed|owner_review|blocked
terminal_status: decision_ready|owner_review|research_needed|blocked
refusal_codes: [string]
assertions_not_established: [category_created, market_leadership, beachhead, demand, adoption, owner_approval]
prohibited_inferences: [string]
next_action: {action: string, owner: string, evidence_needed: [string]}
source_refs: [OA2-05, PB-C1, PB-C2, PB-C3]
```

## Completion

Complete when all three candidates have typed evidence and burden fields, one
legal branch is emitted, and owner approval is explicitly present or absent.
Completion is a proposed runtime result, not a category declaration, V2
mutation, fixture proof, or release claim.

## Downstream prohibitions

KB-7 V2 may test only an explicitly owner-approved positioning snapshot. No
receiver may infer beachhead, market leadership, category existence, purchase
intent, adoption, demand, or copy approval from a market-style recommendation.
