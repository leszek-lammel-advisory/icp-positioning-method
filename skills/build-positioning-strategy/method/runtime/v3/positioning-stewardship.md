---
domain: positioning-strategy
runtime: positioning-stewardship
version: 3
status: proposed
load:
  - ../../source-claim-gap-matrix-v3.md
  - ../../sources/dunford-obviously-awesome-second-edition-dossier.md
---

# V3 Runtime: Positioning Stewardship

## Entry

Enter after owner approval to hand positioning to a named receiver, at an
owner-approved checkpoint, or when a material product, customer, alternative,
competitive, value, market-style, or pitch-evidence change may affect the
approved snapshot. This runtime is the handoff and change-control contract.

## Non-entry

Do not use stewardship to create the first positioning, resolve an unknown
alternative, write messaging, approve copy, execute a campaign, or silently
edit the canonical positioning source. A calendar checkpoint without change
evidence is a review trigger, not proof that change is required.

## First move

Resolve the current owner-approved snapshot, its steward, approval ID,
effective scope, version, and downstream receivers. Compare the trigger to
that immutable baseline before proposing any action.

## Exact runtime inputs

- current approved positioning snapshot and owner approval ID;
- named positioning steward and decision owner;
- checkpoint or change-trigger record with date, source, and affected scope;
- downstream receiver and intended use for a handoff;
- prior handoff acknowledgements and known derived artifacts;
- requested action: handoff, checkpoint, impact assessment, or reopen.

## Evidence, source, and field rules

OA2-07 and OA2-08 define maintained handoff and stewardship method. They do not
set a company's cadence, steward, materiality threshold, or change decision.
Those require explicit owner records.

Every trigger, impact, ownership field, and receiver acknowledgement is
`known`, `inferred`, `unknown`, or `conflicted`. A weak signal may be recorded
as inferred; it does not mutate the baseline. Conflicting approved records
block handoff until the owner identifies the canonical version.

## Legal outcomes

- `positioning_stands`: one canonical approved snapshot can be handed off, or
  a checkpoint found no material evidence affecting the chain. The terminal
  status is `route_downstream` to the named receiver.
- `reopen_positioning`: material evidence affects an upstream link and an
  owner-approved review should return to the positioning workflow. This routes
  the review; it does not change the snapshot.
- `research_needed`: a potential change is factual but impact cannot yet be
  classified; the exact evidence request is named.
- `owner_review`: material evidence may affect one or more positioning fields,
  cadence/materiality is an owner decision, or the owner must approve a new
  snapshot.

Missing canonical approval, conflicting versions, prohibited use, or a silent
mutation request fail admission in the V3 router before a stewardship decision
record is created.

## Procedure

1. Verify canonical snapshot, approval, steward, scope, and current version.
2. Classify the request as handoff, checkpoint, change trigger, or downstream
   use.
3. For a handoff, record receiver, permitted use, prohibited inference, and
   acknowledgement. The handoff supplies strategy; it does not approve copy.
4. For a trigger, map evidence to the earliest potentially affected field:
   alternative, distinct capability, value, best fit, market style, or
   expression/pitch evidence.
5. Assess materiality without editing the snapshot. Route factual gaps to
   research and decision/change proposals to owner review.
6. Emit one outcome, terminal status, next owner, and version consequence.

## Diagnostic routing codes

Stewardship has no release-level hard-refusal outcome. Admission failures stop
in the V3 router; the codes below explain the proposed routing reason.

- `APPROVED_POSITIONING_SNAPSHOT_REQUIRED`
- `OWNER_APPROVAL_RECORD_REQUIRED`
- `POSITIONING_STEWARD_REQUIRED`
- `CANONICAL_VERSION_CONFLICT`
- `HANDOFF_RECEIVER_UNDEFINED`
- `HANDOFF_USE_UNDEFINED`
- `RECEIVER_ACKNOWLEDGEMENT_REQUIRED`
- `PROHIBITED_DOWNSTREAM_USE`
- `MATERIALITY_NOT_ESTABLISHED`
- `CHANGE_EVIDENCE_INCOMPLETE`
- `OWNER_CHANGE_APPROVAL_REQUIRED`
- `SILENT_POSITIONING_MUTATION_FORBIDDEN`
- `CALENDAR_TRIGGER_NOT_CHANGE_EVIDENCE`
- `COPY_APPROVAL_OUT_OF_SCOPE`
- `UNAUTHORIZED_EXTERNAL_OR_FILE_WRITE`
- `SOURCE_GAP`

## Record shape: `PositioningStewardshipDecision`

```yaml
run_id: string
record_type: PositioningStewardshipDecision
module_version: positioning-stewardship/v3
request_type: handoff|checkpoint|change_trigger|downstream_use
input_refs: {approved_positioning_snapshot_id: string, owner_approval_id: string, trigger_record_ids: [string], prior_handoff_ids: [string]}
scope: {positioning_object: string, customer_lane: string, situation: string, effective_version: string}
ownership:
  steward: {name: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
  decision_owner: {name: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
trigger:
  type: checkpoint|product_change|customer_change|alternative_change|competitive_change|value_change|market_change|pitch_signal|handoff_request
  description: string
  status: known|inferred|unknown|conflicted
  evidence_refs: [string]
impact_map:
  - field: alternative|distinct_capability|value|best_fit_customer|market_style|expression_or_pitch|none
    impact_status: known|inferred|unknown|conflicted
    materiality: material|not_material|unknown|conflicted
    evidence_refs: [string]
    reasoning: string
handoff:
  receiver: string|null
  permitted_use: [string]
  prohibited_use: [string]
  acknowledgement_status: known|inferred|unknown|conflicted
  acknowledgement_ref: string|null
version_consequence: retain_current|research_before_decision|owner_review_before_new_version|handoff_current
outcome: positioning_stands|reopen_positioning|research_needed|owner_review
terminal_status: route_downstream|research_needed|owner_review
refusal_codes: [string]
prohibited_inferences: [string]
next_action: {action: string, owner: string, evidence_needed: [string]}
source_refs: [string] # OA2-07 and/or OA2-08 as actually applied
```

## Completion

Complete when the canonical version is preserved, trigger and impact fields are
typed, one branch and owner are named, and any handoff records permitted and
prohibited use. A new positioning version exists only after a separate explicit
owner approval; stewardship never creates it implicitly.

## Downstream prohibitions

Receivers may use only the approved snapshot for the recorded purpose. They
must not alter positioning, broaden scope, suppress uncertainty, treat handoff
as copy approval, infer change from cadence, or apply a challenged snapshot
after owner review has required a new decision.
