---
domain: positioning-strategy
module: KB-3
status: tested
sources:
  - sources/dunford-relative-value-dossier.md
  - sources/play-bigger-category-design-dossier.md
depends_on: [M1, KB-2]
---

# Existing Market Frame or Category Creation

## Decision and boundary

KB-3 decides whether the available evidence supports an **existing frame**, a
**category-creation hypothesis**, **research needed**, or **blocked**. A market
frame is a buyer interpretation aid: it activates a comparison, expected
capabilities, buyer role, and often price logic. It is not a branding exercise
and it cannot repair missing value proof.

Choose an existing frame when it helps the supported buyer understand the
M1/KB-2 situation without creating material false expectations. Consider a
new frame only when the existing frame obscures a material problem or solution
logic *and* the company can sustain teaching a different point of view.

## Required inputs

| Input | Minimum content | Missing-evidence behavior |
|---|---|---|
| M1 | observed alternative, buyer, situation, refs | `research_needed` or `blocked` if absent. |
| KB-2 | value decision, link ledger, scope | A hypothesis stays a hypothesis under every frame. |
| Frame evidence | buyer language, market comparisons, or research record | Do not assume a buyer understands the label. |
| Company capacity | product/sales/proof/demand owners, activities, time/risk | New category cannot pass without it. |

## Candidate-frame ledger

For every frame record: `frame`, `type`, `evidence_refs`, `comparison it
activates`, `expected capabilities/buyer/price logic`, `value clarity`,
`contradictions`, `reversal condition`, and `state`.

| Test | Existing frame passes when | Category creation passes when | Failure behavior |
|---|---|---|---|
| Buyer comprehension | Evidence shows the intended buyer understands the comparison. | Evidence shows the underlying new problem is recognizable or testable in buyer language. | `research_needed`. |
| Value fidelity | It clarifies, rather than hides, the scoped KB-2 chain. | It identifies a materially different solution logic, not a synonym. | `blocked` if contradiction is known. |
| Expectation fit | Expected capabilities, buyer, and price logic do not materially conflict with the offer. | New expectations are specified and can be fulfilled. | `research_needed` if expectations are unknown. |
| Conditioning capacity | Not required beyond ordinary execution. | Named product, proof, sales, and market activities have owners and accepted time/risk. | `research_needed` if capacity is unproven; `blocked` if request rests on novelty/crowding. |

## Procedure

1. Copy the M1 buyer situation and KB-2 decision without strengthening either.
2. List the smallest plausible existing frames. Do not include a frame merely
   because a founder likes it or an analyst uses it.
3. For each frame, identify the comparison and expectations it invites. Mark
   an expectation as unknown if it is not evidenced.
4. Test value fidelity and contradiction. A frame that promises the wrong
   product behavior is not "differentiated" - it is misleading.
5. Consider a new frame only after recording what the existing frame hides.
   Require a buyer-evidenced problem POV, distinct solution logic, and a
   conditioning plan with named evidence.
6. Return one decision, its confidence, evidence ledger, refused assumptions,
   and the one condition that could reverse it.

## Worked decisions

**Existing frame:** buyers already call the problem coordination; a
coordination frame makes the observed spreadsheet workflow and supported
synchronization difference clear; no product expectation conflicts. Decision:
`existing_frame`, scoped to that buyer/situation. It does not turn the
hypothesized buyer outcome into proof.

**Category creation hypothesis:** the existing frame reliably causes buyers to
expect task management, while repeated interviews describe a different
authoritative-state problem. The product's solution logic is distinct and the
company can show owned education, product, proof, sales, and demand work.
Decision: `category_creation_hypothesis`, followed by perception research, not
a declaration that the category exists.

**Blocked:** a founder wants a new label solely because incumbent vendors are
strong. No hidden buyer problem, distinct logic, or conditioning capacity is
evidenced. Decision: `blocked`, refusal code `NOVELTY_OR_CROWDING_NOT_WARRANT`.

## Failure modes

- Treating a crowded category as a reason to invent one.
- Using an elegant label as evidence that buyers will understand it.
- Letting a new frame upgrade a KB-2 value hypothesis into an outcome claim.
- Selecting a frame before the buyer alternative is known.

## Handoff

Return `KB3FrameDecision` as defined in the runtime. KB-4 may use the decision
to assess adoption and beachhead conditions. KB-5 must still test current
perception; KB-7 must still test expression.
