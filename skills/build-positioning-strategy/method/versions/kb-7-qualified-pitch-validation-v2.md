---
domain: positioning-strategy
module: KB-7
extension: qualified-prospect-pitch-validation
version: 2
status: proposed
extends: ../07-expression-validation.md
sources:
  - ../sources/dunford-obviously-awesome-second-edition-dossier.md
  - ../sources/wynter-perception-validation-dossier.md
depends_on: [V3-readiness, M1, V3-DC, KB-2, V3-BFC, KB-3-v3]
---

# KB-7 V2 Extension: Qualified-Prospect Pitch Validation

## Extension boundary

This extension interprets a structured sales-pitch record from live,
qualified, best-fit prospects against an immutable, owner-approved positioning
snapshot. It extends tested KB-7 V1 expression validation; it does not replace
the V1 comprehension sequence or change V1 maturity.

A qualified-prospect reaction is evidence. It may support, challenge, or fail
to resolve the positioning. It never edits the positioning, upgrades an
upstream state, proves market demand, or attributes causality to deal progress.
Every proposed positioning change terminates at `owner_review`.

## Admission

Require:

- an owner-approved positioning snapshot with resolvable M1, distinct-
  capability, KB-2, best-fit, and market-style records;
- the exact pitch version and delivery context;
- a qualification record showing why each respondent fits the approved
  best-fit scope and buying situation;
- a live pitch record that separates prospect words, operator notes,
  comprehension, excitement, confusion, questions, objections, and observed
  deal event;
- source identity, date, and evidence refs.

Synthetic fixtures, internal role-play, unqualified contacts, and memory-only
call summaries cannot produce a live positioning signal.

## Evidence sequence

1. Verify qualification before interpreting the reaction.
2. Preserve the pitch and positioning versions; do not summarize either into a
   stronger claim.
3. Record unaided comprehension of audience, problem, alternative,
   capability/difference, value, and market style.
4. Record excitement, confusion, questions, credibility concerns, and
   objections as separate signals in the prospect's language.
5. Record deal progress as an observed event with plausible alternative
   explanations. It is not proof that positioning caused the event.
6. Classify each item to the earliest owner: qualification/research design,
   M1, distinct capability, KB-2, best fit, KB-3, expression, or sales
   execution.

## Signal interpretation

| Signal direction | Minimum basis | Meaning | Forbidden conclusion |
|---|---|---|---|
| `support` | Qualified live prospects understand the approved chain and provide no material contradiction in scope. | Bounded support for retaining the snapshot. | The positioning is universally proven or caused progress. |
| `challenge` | A qualified live prospect provides a specific, evidence-linked contradiction to an approved field. | Owner review is warranted at the earliest affected layer. | The prospect automatically rewrites the position. |
| `mixed` | Qualified evidence supports and challenges material fields, or varies by coherent lane. | Split scope or gather discriminating evidence before owner choice. | Average the conflict into a positive verdict. |
| `none` | Qualification, sequence, sample, or response content cannot support a positioning inference. | Research or design repair is needed. | Silence or a deal event is validation. |

One prospect can reveal a material contradiction; one prospect cannot establish
convergence. Repeated answers from one source remain one source. Sample size is
reported, not converted into a universal numeric threshold by this prose
contract.

## Legal outcomes

- `positioning_supported` with `route_downstream` when qualified live evidence
  supports the approved snapshot without material challenge.
- `positioning_revision_hypothesis` with `owner_review` when evidence challenges
  a specific upstream link and identifies the earliest owner.
- `research_needed` when qualification, sequence, or response evidence can be
  repaired through a named request.
- `owner_review` when evidence is materially mixed or the owner must choose the
  scope of a change review.
- `blocked` when the request treats copy response, synthetic evidence, or an
  unqualified reaction as positioning proof, or demands an automatic change.

## Owner-review rule

When evidence suggests a change, emit `positioning_revision_hypothesis` with
terminal status `owner_review` and the exact challenged
field, supporting and counterevidence, affected upstream owner, scope, and
reversal condition. The owner may accept research, preserve the current
position, narrow the scope, or authorize a new positioning run. The runtime
does not mutate the approved snapshot.

## Downstream prohibitions

Pitch evidence must not:

- auto-change alternatives, capability, value, best fit, or market style;
- turn comprehension, excitement, preference, objection, or progress into
  purchase intent or causal proof;
- authorize new copy, CRM changes, campaign activation, or sales coaching;
- treat synthetic or internal responses as live qualified-prospect evidence;
- bypass the earliest upstream owner with an expression rewrite.
