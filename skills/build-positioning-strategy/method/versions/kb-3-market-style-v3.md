---
domain: positioning-strategy
module: KB-3
extension: market-style
version: 3
status: proposed
extends: ../03-market-frame-choice.md
sources:
  - ../sources/dunford-obviously-awesome-second-edition-dossier.md
depends_on: [V3-readiness, M1, V3-DC, KB-2, V3-BFC]
---

# KB-3 V3 Extension: Market Style

## Extension boundary

This extension compares three strategic market styles after alternatives,
distinct capability, differentiated value, and best-fit customer have been
bounded. It does not replace tested KB-3 V2 frame choice and does not change a
V2 decision or maturity claim.

The style outcome is a proposed recommendation. The business owner approves the
actual style and execution burden. An agent may narrow the evidence-compatible
choice; it may not declare a category, a leadership position, or a company
commitment.

## Legal outcomes

| Outcome | Required conditions | Main burden | Prohibited interpretation |
|---|---|---|---|
| `head_to_head` | An established category is understood by the best-fit customer, clarifies the KB-2 value, and creates no material expectation conflict. Evidence supports a credible reason to choose the offer within that comparison. | Prove differentiated choice inside familiar expectations. | The company is already a category leader. |
| `big_fish_small_pond` | A narrower subsegment has unusually acute value, coherent alternatives and expectations, and a credible boundary within which the offer can be preferred. | Maintain focus, proof, access, and explicit exclusions. | The subsegment is a KB-4 beachhead or is won because it is small. |
| `create_new_game_hypothesis` | Existing frames materially hide or distort the value; a recognizable problem point of view, different solution logic, specified expectations, and company conditioning capacity are evidenced. | Highest education, product, proof, sales, demand, time, and risk burden. | A new category exists or has owner approval. |
| `research_needed` | One or more decisive buyer, expectation, value-fidelity, subsegment, or capacity fields are unknown. | Collect the smallest evidence that discriminates between styles. | Uncertainty is a recommendation. |
| `owner_review` | Evidence permits more than one style and the remaining choice is business intent, accepted burden, or material stakeholder conflict. | Owner chooses or requests revision with rationale. | Owner preference supplies missing external evidence. |
| `blocked` | The request contradicts upstream evidence, uses novelty/crowding alone, requires a leadership/category claim, or asks the agent to make an owner-only commitment. | Correct scope or upstream record before proceeding. | A stronger label can repair the contradiction. |

## Comparison procedure

1. Preserve every upstream scope and evidence state.
2. Test `head_to_head` first against buyer comprehension, value fidelity, and
   expected capabilities, buyer, and price logic.
3. Test `big_fish_small_pond` only when the best-fit evidence identifies a
   narrower coherent group for reasons tied to value. Reachability alone fails.
4. Test `create_new_game_hypothesis` only when existing-frame failure is
   evidenced. Apply the tested KB-3 V2 new-frame warrant and conditioning-
   capacity tests.
5. Compare burden, reversal conditions, and prohibited claims side by side.
6. Emit one legal outcome. Where the evidence-compatible result still requires
   commitment of focus, time, risk, or organizational effort, emit
   `owner_review` and present the evidence-backed recommendation separately.

## State and source rule

Every candidate field is `known`, `inferred`, `unknown`, or `conflicted` and
cites company evidence. The provisional dossier may define the three styles
and relative burden only. It cannot establish buyer understanding, segment
coherence, company capacity, or the correct style. Load-bearing source content
the dossier does not cover uses `SOURCE_GAP`.

## Handoff

The V3 runtime emits a `MarketStyleDecision` with candidate tests, burden,
recommendation, owner decision state, reversal condition, and downstream
prohibitions. KB-7 V2 pitch validation may test an owner-approved snapshot; it
may not treat a proposed style as approved.
