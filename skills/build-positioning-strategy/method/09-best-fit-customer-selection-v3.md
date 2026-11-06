---
domain: positioning-strategy
module: V3-BFC
status: proposed
version: 3
sources:
  - sources/dunford-obviously-awesome-second-edition-dossier.md
depends_on: [V3-readiness, M1, V3-DC, KB-2]
---

# Best-Fit Customer Selection

## Decision and boundary

This module selects a bounded best-fit customer decision from the customers
for whom an evidenced KB-2 value chain matters most and can be bought and
reached. It explains why each characteristic changes the importance of the
value. It does not produce a broad ICP, rank accounts, forecast demand, or
declare a beachhead.

Best fit and beachhead are different decisions. Best fit asks where the
differentiated value is unusually relevant and commercially usable. KB-4 asks
whether an initial group satisfies discontinuity, whole-product, reference-
transfer, repeatability, and expansion conditions. Reachability is one best-
fit feasibility check; it is never sufficient evidence for either decision.

## Required inputs

| Input | Minimum content | Failure behavior |
|---|---|---|
| Readiness decision | `ready` with one positioning object and bounded scope. | Route to readiness. |
| M1 | Same-scope observed alternative, buyer situation, and evidence refs. | Unknown alternative routes to M1 research. |
| Distinct capability | At least one same-scope capability record that KB-2 admitted. | Missing difference routes to distinct-capability research. |
| KB-2 | Value-chain decision with link states and evidence refs. | `blocked` or `research_needed` value cannot support selection; a hypothesis can support research lanes only. |
| Customer evidence | Records showing situations, value importance, buying conditions, exclusions, and source identity. | Firmographics without causal relevance remain descriptive only. |
| Commercial feasibility | Buying authority/process and a plausible access route, each evidenced separately. | Unknown feasibility produces research, not exclusion by assumption. |

## Field-status protocol

Use `known`, `inferred`, `unknown`, and `conflicted` for every characteristic,
value-relevance link, buying condition, and access condition. An inferred
characteristic must name the known facts it depends on and a reversal
condition. A conflicted field stays conflicted until research or an explicit
scope split resolves it.

## Selection tests

| Test | Required question | Pass condition |
|---|---|---|
| Value acuity | Why is the KB-2 outcome unusually important here? | Same-scope customer evidence links a characteristic or situation to urgency, consequence, frequency, or strategic importance. |
| Alternative consistency | Do these customers face the same admitted alternative in the same situation? | M1 scope and customer evidence agree. |
| Capability/value fit | Does the admitted distinct capability enable the value for this group? | KB-2 preserves at least a hypothesis chain without contradiction. |
| Group coherence | Would materially different characteristics change the alternative, value, proof, or buying path? | One bounded lane shares the causal explanation; otherwise split it. |
| Ability to buy | Is there evidence of authority, budget logic, procurement viability, or an equivalent buying route? | At least one plausible, evidenced route exists; purchase is not claimed. |
| Ability to reach | Is there a lawful, plausible way to identify and contact or serve the group? | A route is evidenced; reachability does not determine value acuity. |
| Exclusion | Who looks similar but does not share the value condition? | At least one evidence-linked exclusion prevents firmographic overbreadth. |

## Procedure

1. Preserve the M1, distinct-capability, and KB-2 scopes and states.
2. Build candidate groups from customer situations and value relevance, not
   from list filters.
3. For each characteristic, write the causal sentence: "this matters because
   it changes ___." Remove characteristics that do not change value acuity,
   buying feasibility, access, or an explicit exclusion.
4. Split groups when alternative, value chain, proof expectation, or buying
   route materially differs.
5. Evaluate buying and reachability after value acuity; do not let easy access
   rescue a weak value link.
6. Return a hypothesis, exact research plan, owner-review question, or block.

## Legal outcomes

- `best_fit_supported`: value acuity, alternative consistency, buying, and
  reachability are supported; no material conflict remains.
- `best_fit_hypothesis`: value acuity and alternative consistency are
  supported; buying or reachability is a bounded inference; the owner must
  review before downstream use.
- `research_needed`: a named evidence gap could change group membership or
  confidence.
- `blocked`: the request demands selection from firmographics or reachability
  alone, uses a blocked KB-2 chain, combines incompatible groups, or labels the
  result a beachhead without KB-4.

## Handoff and prohibitions

The output gives KB-3 V3 a bounded customer hypothesis, value-acuity logic,
exclusions, buying/access states, evidence refs, and unresolved fields. KB-4
may later test the same group only through its own adoption and beachhead
contract.

No receiver may use this output to claim purchase intent, market size,
adoption stage, beachhead viability, repeatability, category leadership, or
message validation.
