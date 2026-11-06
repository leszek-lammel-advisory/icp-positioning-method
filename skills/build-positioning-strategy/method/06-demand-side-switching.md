---
domain: positioning-strategy
module: KB-6
status: tested
sources: [sources/moesta-demand-side-dossier.md]
depends_on: [M1]
---

# Demand-Side Switching and Buyer Progress

## Decision and boundary

KB-6 decides a buyer-progress diagnosis and the smallest evidence-bound
intervention: `intervention_hypothesis`, `research_needed`, or `blocked`. It
does not predict purchase, assign a numeric force score, infer motives from
firmographics, or replace M1's alternative evidence.

## Required force ledger

| Field | Supported only when | Prohibited shortcut |
|---|---|---|
| Struggling moment | A buyer/account record identifies an event or inadequacy in a named situation. | Generic persona pain. |
| Before state | Current behavior or alternative is observed in M1. | Product-category inference. |
| Push | Evidence states what is unsustainable about the current situation. | Assuming a manual workflow is painful. |
| Pull | Evidence states desired progress or attraction. | Treating feature availability as pull. |
| Anxiety | Buyer evidence names concern about changing, risk, or implementation. | Inferring fear from retention. |
| Habit | Buyer evidence identifies attachment, routine, or cost of giving up current behavior. | Calling every incumbent use habit. |

## Procedure

1. Validate the M1 buyer, situation, and observed alternative. A missing M1
   alternative routes to `research_needed` and `route_to_M1`; it never permits
   a completed before-state or an alternative comparison. A request made from
   firmographics, title, visits, or seller assumptions routes to `blocked`.
2. Build the force ledger with evidence refs and state for each field.
3. Locate the progress state from observed behavior: `no_first_thought`,
   `passive_looking`, `active_looking`, `deciding`, `first_use`,
   `ongoing_use`, or `unknown`.
4. Name one bottleneck. Choose only an intervention that addresses the
   evidenced bottleneck: research the situation, progress clarification,
   alternative criteria, named risk proof, delivery support, or outcome
   capture. A buyer with no recognized struggle must not receive a vendor
   comparison; a buyer with implementation anxiety must not receive feature
   volume as a substitute for transition evidence.
5. State the observable result that would support or disprove the diagnosis.

## Stage-to-intervention rules

| Stage | Minimum evidence | Typical bottleneck | Allowed intervention |
|---|---|---|---|
| no_first_thought | No recognized struggle | no problem space | research the situation; do not compare vendors |
| passive_looking | problem noticed, no committed search | relevance or desired progress | clarify before-state and progress |
| active_looking | alternatives/criteria being explored | evaluation clarity | map alternatives, differences, and proof |
| deciding | specific option/trade-off/risk evaluated | anxiety or habit | address the named risk with relevant evidence |
| first_use/ongoing_use | use behavior exists | delivery or sustained outcome | capture outcomes and contradictions |

`no_first_thought` is a research boundary, not a demand-generation verdict.
The runtime may ask about the situation but must refuse a vendor comparison.
`passive_looking` requires a directly observed struggle and no committed
search. `active_looking` requires observed exploration of alternatives or
criteria. `deciding` requires a direct option, trade-off, or named risk under
evaluation. The runtime must preserve `unknown` when behavior does not support
one of those stages.

## Worked cases

**Bounded intervention:** a buyer reports missed handoffs after a reorg and
has not looked for tools. Push and struggling moment are supported; pull,
anxiety, and habit are unknown. Stage: `passive_looking`. Decision:
`intervention_hypothesis` to ask for desired progress and before-state language,
not to send a competitor grid.

**Wrong intervention:** a buyer asks whether implementation will disrupt a
critical process. The agent responds with more feature volume. The evidence
points to anxiety, so feature volume does not address the bottleneck.

**Blocked:** a request asks to score an account's switching likelihood from
title, company size, and web visits. No buyer situation or force evidence
exists. Return `blocked` with `MOTIVE_INFERENCE_WITHOUT_BUYER_EVIDENCE`.

## Handoff

Return the runtime object. An intervention hypothesis is not validated copy or
demand. It may inform research or expression experiments, whose outcomes must
be recorded separately.
