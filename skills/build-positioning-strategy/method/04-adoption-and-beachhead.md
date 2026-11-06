---
domain: positioning-strategy
module: KB-4
status: tested
sources: [sources/moore-adoption-beachhead-dossier.md]
depends_on: [M1, KB-2, KB-3]
---

# Adoption Stage and Beachhead Selection

## Decision and boundary

KB-4 decides whether a proposed initial group is a
`beachhead_hypothesis`, `standard_segment_hypothesis`, `research_needed`, or
`blocked`. It does not declare a buyer archetype, forecast adoption, select a
segment from reachability, or treat product novelty as discontinuity.

A beachhead is a deliberately focused initial market where a coherent group
shares the problem, alternative, value chain, adoption barriers, and a
reference path. It is not simply a small vertical, a list of titles, or the
lowest-cost audience to reach.

## Required evidence ledger

| Test | `supported` when | `research_needed` when | `blocked` when |
|---|---|---|---|
| Discontinuity | Buyer evidence identifies a material workflow/risk/proof/integration change. | Change burden unknown. | Only seller novelty is offered. |
| Shared situation | Members share trigger, alternative, value scope, and barrier. | Some common traits but insufficient buyer evidence. | Firmographics/reachability are the only commonality. |
| Whole product | Required dependencies and owners are evidenced. | Gaps or ownership unknown. | Critical known gap is ignored. |
| Reference transfer | A credible peer/application/channel link connects successful users to the next buyers. | Reference path untested. | A generic case study is treated as transfer proof. |
| Repeatability | Same solution can be delivered without hidden bespoke work. | Delivery variability unknown. | Proposition depends on unbounded custom work. |
| Expansion path | Next adjacent group and transfer condition are named and evidenced. | Next group or transfer condition is unknown. | Expansion is asserted from reachability alone. |

## Decision aggregation

First evaluate the standard-segment exception. Return
`standard_segment_hypothesis` when discontinuity is explicitly absent and the
group is evidenced beyond reachability. The six beachhead tests are then not
applicable and must be recorded `not_applicable`, not treated as failed.

Otherwise apply the six tests in this order. Return `blocked` if any test is
`blocked`. Return `research_needed` if no test is blocked but discontinuity,
shared situation, whole product, reference transfer, repeatability, or
expansion path is not `supported`. Return `beachhead_hypothesis` only when all
six tests are supported. Reachability alone is `blocked`, not a standard-
segment shortcut.

## Procedure

1. Copy M1 buyer/situation, KB-2 value status, and KB-3 frame without
   upgrading their evidence state.
2. Ask whether there is buyer-evidenced discontinuity. If not, use a standard
   segment decision rather than technology-adoption language.
3. Build a group ledger: trigger, current alternative, scoped value, adoption
   barrier, whole-product components, delivery owner, and reference path.
4. Test coherence. A group fails if its members need materially different
   alternatives, solutions, or proof to adopt.
5. Test the next group and reference-transfer condition. If either is unknown,
   record expansion path `research_needed`.
6. Apply the aggregation rule, list refused assumptions, and name the smallest evidence
   request that could reverse the decision.

## Worked cases

**Beachhead hypothesis:** audit-triggered operations teams share the same
reconciliation alternative and integration requirement. A partner owns the
integration, the company owns implementation, and evidence identifies a peer
network that evaluates similar deployments. The decision is a hypothesis until
the shared condition and reference behavior are verified, not a promise that
the group will adopt.

**Standard segment:** a vertical is easy to target but contains multiple
current alternatives and outcome needs. It may remain a useful acquisition
segment, but it lacks the coherence required for a beachhead claim.

**Blocked:** “our product is new, so pragmatic buyers need a beachhead.” Product
novelty does not show a buyer discontinuity, whole-product gap, or reference
path. Return `blocked` with `NOVELTY_IS_NOT_ADOPTION_EVIDENCE`.

## Handoff

Return the runtime object with evidence states and reversal condition. Later
modules must not claim an adoption stage or a scalable reference base from a
KB-4 hypothesis.
