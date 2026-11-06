---
domain: positioning-strategy
module: KB-2
status: tested
sources:
  - sources/dunford-relative-value-dossier.md
depends_on: [M1]
---

# Differentiated Value Relative to the Alternative

## Purpose and boundary

KB-2 decides the evidential status of one proposed value chain. It does not
write a value proposition, choose a category, select a segment, estimate ROI,
or turn a hypothesis into headline copy. Its output is an auditable bridge
between a tested M1 alternative diagnosis and later positioning decisions.

Value is not a feature or an adjective. It is a buyer-relevant outcome enabled
by a meaningful difference relative to a buyer's evidenced alternative. The
chain is:

`baseline alternative -> difference -> mechanism -> buyer outcome -> proof`

Every arrow is a separate claim. A capability demonstration establishes only
the difference. It does not establish the mechanism, outcome, adoption, or
economic impact.

## Required inputs

| Input | Minimum content | Failure behavior |
|---|---|---|
| M1 handoff | run ID, M1 version, one `observed` baseline, evidence refs, situation | `research_needed` if an M1 handoff has only `candidate`, `excluded`, or `unknown` alternatives; `blocked` if M1 is absent or the buyer/situation is incompatible. An `excluded` alternative may not be used as a baseline. |
| Capability record | capability ID, exact behavior, product/demo evidence refs | `research_needed` if the difference itself is unknown. |
| Evidence inventory | customer, usage, outcome, and proof records with IDs | Missing records remain missing - no inferred proof. |
| Claim request | one proposed buyer outcome, named buyer/situation | Split feature piles into one chain per claim. |

## Link ledger and canonical vocabulary

For each link record `state`, `evidence_refs`, and `reasoning`. The only valid
states are `supported`, `hypothesis`, `research_needed`, and `blocked`.

| Link | `supported` | `hypothesis` | `research_needed` | `blocked` |
|---|---|---|---|---|
| Baseline | M1 marks one buyer alternative observed in the same situation. | Never valid. | M1 has only `candidate`, `excluded`, or `unknown` alternatives. | No M1 handoff or incompatible buyer/situation. |
| Difference | Product or operating difference is evidenced relative to that baseline. | Credible seller claim but no product evidence. | Capability is vague or comparison is incomplete. | Difference changes the baseline or contradicts evidence. |
| Mechanism | Customer/use evidence directly connects the difference to a work/risk/control change. | Causal path is plausible but not directly observed. | No causal account or buyer context. | Claimed mechanism contradicts supplied evidence. |
| Outcome | Buyer testimony, measured use, or an appropriately scoped study supports the outcome in the same or demonstrably comparable situation. | Outcome is plausible from a supported baseline and difference but untested. | Buyer importance or result is unknown. | Requested outcome contradicts evidence or is an unsupported quantified performance claim. |
| Proof | Evidence class is named and supports the level of claim. | Evidence supports an earlier link only. | No proof inventory or method. | A demo or seller assertion is offered as outcome proof. |

The chain decision is calculated in this order:

1. Return `blocked` if baseline is blocked, an asserted link contradicts its
   evidence, or a requester requires an outcome/performance claim whose proof
   class cannot support it.
2. Return `research_needed` if baseline is not supported, difference is not
   supported, or mechanism/outcome lacks the minimum evidence to form a bounded
   hypothesis.
3. Return `hypothesis` if baseline and difference are supported, no link is
   blocked, and mechanism or outcome is not directly evidenced.
4. Return `supported` only if all five links are supported. A supported chain
   still states its scope and cannot be generalized to an unobserved segment.

## Procedure

1. **Verify comparability.** Confirm that the M1 baseline, proposed buyer, and
   claimed situation match. Do not borrow a baseline from another segment.
2. **State the difference without an adjective.** Write what the product or
   operating model does differently from the baseline, with its evidence ID.
3. **Construct a falsifiable mechanism.** Describe the intermediate work or
   risk change. If the link cannot be observed or queried, label it
   `research_needed`, not "obvious."
4. **Classify the buyer outcome.** Record the narrow outcome the evidence can
   support. Product screenshots prove capability. Direct testimony can support
   a reported experience. Measured before/after evidence may support a scoped
   result. None automatically proves an ROI claim.
5. **Calculate and refuse.** Apply the matrix, state every refused assumption,
   and specify the smallest next evidence request that could change the
   decision.

## Worked case

M1 observed that one operations team uses a shared spreadsheet and weekly
meeting to reconcile ownership. A demo shows approved changes synchronize
across systems. The baseline and difference are supported. "Fewer handoffs
are lost" is a mechanism hypothesis, not a fact, unless customer or usage
evidence shows it. "Dependable coordination" is likewise a buyer-outcome
hypothesis. The correct decision is `hypothesis` with a test: ask users to
compare missed or delayed handoffs before and after use, and ask whether this
outcome affects their choice to change the workflow.

## Failure modes

**Feature pile:** “automation, dashboards, integrations, and AI make finance
faster.” No baseline, causal link, buyer outcome, or proof class is specified.

**Proof laundering:** “customers save hours” because a one-click export is
shown in a demo. The proof supports a capability, not the claimed result.

**Alternative drift:** M1 observed a spreadsheet workflow, but the agent
compares the offer to an enterprise analytics vendor because that makes the
feature list look better. The chain is invalid because its baseline changed.

**No-baseline improvisation:** A founder asks for value language before any
customer alternative is known. The only admissible output is `research_needed`
or `blocked`, plus the M1 evidence request.

## Output and handoff contract

Return the `KB2ValueDecision` object in the runtime verbatim. A later module
may use only a `supported` chain as established value. It may inspect a
`hypothesis` to design research, but must not express it as a customer truth.
Every non-supported link carries prohibited downstream claims and the next
evidence request.
