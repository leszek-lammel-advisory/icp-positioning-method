---
domain: positioning-strategy
module: V3-DC
status: proposed
version: 3
sources:
  - sources/dunford-obviously-awesome-second-edition-dossier.md
depends_on: [V3-readiness, M1]
consumed_by: [KB-2]
---

# Distinct Capability Identification

## Decision and boundary

This module produces comparative capability records for the existing KB-2
capability-record input. A distinct capability is a specific product or
company behavior that supplied evidence shows the same-scope alternative does
not provide in the same way. It is not a benefit, outcome, market category,
customer segment, feature inventory, or claim that the capability matters to a
buyer.

The module is net-new and additive. It does not revise KB-2. KB-2 continues to
own the chain from observed baseline through difference, mechanism, buyer
outcome, and proof.

## Required inputs

| Input | Minimum content | Failure behavior |
|---|---|---|
| Readiness decision | `ready` for a named positioning object and scope. | Route to readiness; do not compare an undefined offer or scope. |
| M1 handoff | Same-scope buyer, situation, and at least one `observed` alternative with evidence refs. | Candidate or unknown alternatives require research; absent or incompatible M1 blocks the comparison. |
| Capability inventory | Atomic product or operating behaviors with source IDs. | Vague labels and adjectives remain unknown. |
| Alternative evidence | Evidence of what each admitted alternative can and cannot do. | Absence of evidence is not evidence of absence. |
| Request scope | Offer/version, buyer, situation, geography or market when material, and decision date. | Ambiguous scopes split or block before comparison. |

## Field-status protocol

Every substantive field uses exactly one status:

- `known`: directly supported by an admitted source for this scope;
- `inferred`: reasoned from cited known fields, with the inference stated;
- `unknown`: no admissible evidence resolves the field;
- `conflicted`: admitted sources make materially incompatible claims.

Fluent wording never upgrades a status. `Conflicted` evidence cannot be
settled by counting sources or by owner preference when the conflict is
factual; the owner may choose scope or fund research, not rewrite the record.

## Comparative tests

Evaluate each atomic capability against each observed alternative.

| Test | Pass condition | Research condition | Refusal condition |
|---|---|---|---|
| Specificity | The record states observable behavior without adjectives. | Behavior or boundary is vague. | A feature pile is submitted as one capability. |
| Possession | Product, operating, delivery, or partner evidence shows the company can perform it in scope. | Evidence is a roadmap or unverified assertion. | Known evidence contradicts possession. |
| Alternative contrast | Evidence shows the admitted alternative lacks, constrains, or performs the behavior materially differently. | Alternative behavior is unknown. | The comparison substitutes a more convenient alternative than M1 observed. |
| Scope parity | Offer version, buyer situation, and comparison conditions match. | Comparability is incomplete. | The claim combines incompatible scopes. |
| Capability/value separation | The statement ends at behavior and comparison. | Value language can be removed without changing the behavior. | A benefit or outcome is presented as proof of distinctness. |

## Procedure

1. Copy the readiness scope and M1 alternatives without strengthening either.
2. Atomize the capability inventory into one observable behavior per row.
3. Verify company possession and alternative behavior separately.
4. Compare only like scopes. Record where evidence covers one alternative but
   not another.
5. Classify each comparative row as `supported`, `hypothesis`,
   `research_needed`, or `blocked`, while retaining field statuses.
6. Aggregate rows to `supported_capability`, `capability_hypothesis`,
   `research_needed`, or `blocked`, then emit one capability record per pair
   and a research request for every unresolved comparison.

## Row and outcome rules

- `supported`: possession and alternative contrast are known, scope matches,
  and no material conflict remains.
- `hypothesis`: possession is known and distinctness is a bounded inference
  from cited evidence, with a falsifiable next check.
- `research_needed`: possession, alternative behavior, or comparability is
  unknown but can be resolved with named evidence.
- `blocked`: the request changes the M1 alternative, combines incompatible
  scopes, demands a contradicted claim, or requires value from capability
  evidence alone.

At module level, supported rows aggregate to `supported_capability`; hypothesis
rows without supported rows aggregate to `capability_hypothesis`. Those
outcomes map to `decision_ready` and `owner_review` respectively.

## Worked pattern

Suppose M1 has observed a manual coordination workflow. Product evidence shows
that approved changes synchronize between two systems. That supports
possession of synchronization behavior. It does not yet prove that the manual
workflow lacks every equivalent control, that users care, or that coordination
improves. Distinctness remains a hypothesis until the alternative comparison
is evidenced. KB-2, not this module, owns mechanism and outcome.

## Handoff to KB-2

Each admitted row supplies KB-2 with a `capability_id`, exact behavior,
comparison alternative, scope, evidence refs, comparative state, field
statuses, and prohibited claims. KB-2 may evaluate row states `supported` and
`hypothesis` rows. It must not treat `research_needed` or `blocked` rows as a
difference, and it must preserve the capability state rather than upgrading it
through an outcome claim.

No downstream module may infer buyer value, best fit, category, adoption,
proof, or copy from a distinct-capability record alone.
