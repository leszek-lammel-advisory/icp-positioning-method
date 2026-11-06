---
domain: positioning-strategy
runtime: positioning-qualified-pitch-validation
module: KB-7
version: 2
status: proposed
depends_on: [V3-readiness, M1, V3-DC, KB-2, V3-BFC, KB-3-v3]
load:
  - ../../versions/kb-7-qualified-pitch-validation-v2.md
  - ../../07-expression-validation.md
  - ../../source-claim-gap-matrix-v3.md
  - ../../sources/dunford-obviously-awesome-second-edition-dossier.md
  - ../../sources/wynter-perception-validation-dossier.md
---

# V3 Runtime: Qualified-Prospect Pitch Validation

## Entry

Enter to interpret a recorded pitch delivered to one or more live prospects
whose qualification records match the owner-approved best-fit customer and
buying situation. Require an immutable approved positioning snapshot and the
exact pitch version.

## Non-entry

Do not enter to run a live pitch, write a pitch, qualify prospects from memory,
interpret an internal role-play as market evidence, or change positioning.
Synthetic fixtures test runtime behavior only. Copy-only, sales-coaching, CRM,
and campaign requests return `route_downstream`.

## First move

Verify qualification and snapshot approval before reading whether the prospect
liked the pitch or the deal moved. If either fails, stop; later reactions
cannot repair invalid admission.

## Exact runtime inputs

- `approved_positioning_snapshot_id` containing resolvable M1, distinct-
  capability, KB-2, best-fit, and KB-3 V3 record refs and owner approval;
- `pitch_version_id`, exact pitch content ref, delivery date, channel, and
  presenter;
- `prospect_qualification_ids` tied to the approved best-fit lane and situation;
- `pitch_evidence_ids` with source identity and direct prospect language;
- structured comprehension, excitement, confusion, question, objection,
  credibility, and deal-event fields;
- sample scope and known exposure or facilitation limits.

## Evidence, source, and field rules

OA2-06 supplies the qualified-pitch method. The Wynter dossier supplies the
audience/comprehension-before-preference boundary. Neither supplies a live
reaction or qualification fact.

Every qualification field, observed response, classification, and attribution
is `known`, `inferred`, `unknown`, or `conflicted`. Direct prospect language is
kept separate from operator interpretation. Deal progress is an observed event;
causal attribution to positioning is normally `unknown` unless separately
evidenced. Several answers from one prospect remain one source.

## Legal outcomes

- `positioning_supported`: valid live evidence produces `signal_direction:
  support` and no material challenge or change request. This is bounded support
  for retaining the snapshot, not proof; the terminal status is `route_downstream`.
- `positioning_revision_hypothesis`: one or more material signals challenge an
  upstream link and the exact affected owner is known; the terminal status is
  `owner_review`, never an automatic change.
- `research_needed`: signal direction is `none` or non-material `mixed` because
  sample, sequence, qualification, or response evidence is incomplete but
  repairable.
- `owner_review`: signal direction is `challenge` or material `mixed`, or any
  positioning change is proposed. The record routes the exact challenged field
  to its earliest owner without mutation.
- `blocked`: evidence is synthetic/internal/memory-only, qualification or
  approval is absent, a causal claim is demanded, or the requester requires an
  automatic positioning change.

## Procedure

1. Resolve the approved snapshot and qualification records.
2. Preserve exact positioning and pitch versions.
3. Record unaided comprehension of audience, problem, alternative,
   capability/difference, value, and market style before preference.
4. Record excitement, confusion, questions, objections, credibility, and deal
   events separately in prospect language.
5. Classify each material item to qualification/research design, M1, V3
   distinct capability, KB-2, V3 best fit, KB-3, expression, or sales execution.
6. Set `signal_direction`, one outcome, terminal status, and the smallest next action. Never
   change the approved snapshot.

## Diagnostic routing codes

These proposed codes explain runtime routing. The release-level hard refusal
for this decision type is `COPY_RESPONSE_AS_POSITIONING_PROOF` in SKILL.md.

- `APPROVED_POSITIONING_SNAPSHOT_REQUIRED`
- `POSITIONING_SNAPSHOT_SCOPE_MISMATCH`
- `QUALIFIED_BEST_FIT_PROSPECT_REQUIRED`
- `QUALIFICATION_EVIDENCE_INCOMPLETE`
- `LIVE_PITCH_RECORD_REQUIRED`
- `SYNTHETIC_NOT_LIVE_SIGNAL`
- `INTERNAL_ROLEPLAY_NOT_PROSPECT_EVIDENCE`
- `MEMORY_ONLY_SUMMARY_NOT_EVIDENCE`
- `COMPREHENSION_BEFORE_PREFERENCE_REQUIRED`
- `REPEATED_SOURCE_NOT_INDEPENDENT_EVIDENCE`
- `DEAL_PROGRESS_CAUSALITY_NOT_ESTABLISHED`
- `SINGLE_SIGNAL_NOT_CONVERGENCE`
- `EARLIEST_OWNER_ROUTE_REQUIRED`
- `POSITIONING_AUTO_CHANGE_FORBIDDEN`
- `OWNER_CHANGE_APPROVAL_REQUIRED`
- `COPY_OR_EXECUTION_ROUTE_DOWNSTREAM`
- `SOURCE_GAP`

## Record shape: `QualifiedPitchValidationDecision`

```yaml
run_id: string
record_type: QualifiedPitchValidationDecision
module_version: KB-7/v2-qualified-pitch
input_refs: {approved_positioning_snapshot_id: string, pitch_version_id: string, prospect_qualification_ids: [string], pitch_evidence_ids: [string]}
scope: {best_fit_lane_id: string, buyer_situation: string, market_or_geography: string, pitch_date_range: string}
approved_snapshot: {owner_approval_id: string, m1_run_id: string, distinct_capability_run_id: string, kb2_run_id: string, best_fit_customer_run_id: string, market_style_run_id: string}
prospects:
  - prospect_source_id: string
    qualification: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
    evidence:
      - evidence_id: string
        stage: comprehension|excitement|confusion|question|objection|credibility|preference|deal_event
        prospect_claim: string
        interpretation: {value: string, status: known|inferred|unknown|conflicted}
        supports_or_challenges: audience|problem|alternative|distinct_capability|value|best_fit|market_style|expression|sales_execution|none
        direction: support|challenge|neutral|unknown
    deal_progress: {event: string, status: known|inferred|unknown|conflicted, causal_attribution: known|inferred|unknown|conflicted, evidence_refs: [string]}
signal_direction: support|challenge|mixed|none
earliest_affected_owner: none|research_design|M1|V3-DC|KB-2|V3-BFC|KB-3|expression|sales_execution
positioning_change_proposed: boolean
outcome: positioning_supported|positioning_revision_hypothesis|research_needed|owner_review|blocked
terminal_status: route_downstream|owner_review|research_needed|blocked
refusal_codes: [string]
assertions_not_established: [universal_positioning_proof, purchase_intent, demand, causal_deal_progress, automatic_positioning_change]
prohibited_inferences: [string]
next_action: {action: string, owner: string, evidence_needed: [string]}
source_refs: [OA2-06, WYN-C1, WYN-C3]
```

## Completion

Complete when each admitted prospect has a qualification state, every signal
has source and owner classification, one direction and one branch are emitted,
and the approved snapshot remains byte-for-byte referenced rather than
rewritten. No run changes positioning or promotes this proposed extension.

## Downstream prohibitions

No downstream receiver may convert support into universal proof, a challenge
into an automatic change, excitement into demand, preference into strategy,
or a deal event into causal validation. Only an explicit owner-reviewed change
record may create a new approved snapshot.
