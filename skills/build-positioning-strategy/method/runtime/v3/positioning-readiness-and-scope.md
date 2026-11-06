---
domain: positioning-strategy
runtime: positioning-readiness-and-scope
version: 3
status: proposed
load:
  - ../../source-claim-gap-matrix-v3.md
  - ../../sources/dunford-obviously-awesome-second-edition-dossier.md
---

# V3 Runtime: Positioning Readiness and Scope

## Entry

Enter before a positioning exercise or when a request leaves the positioning
object, customer scope, purpose, champion, or decision authority ambiguous.
This is a cross-cutting admission gate for every V3 positioning route.

## Non-entry

Do not use this runtime to diagnose alternatives, choose capabilities, value,
customers, or market style, validate a pitch, write copy, or approve a
positioning change. If an approved positioning record exists and the request is
copy-only, return `route_downstream`.

## First move

Freeze the proposed scope in one sentence: positioning object/version, target
customer or decision lane, situation, geography or market when material,
exercise purpose, and decision date. Do not collect positioning answers until
the scope itself is reviewable.

## Required inputs

- request ID and exercise purpose;
- product or offer readiness evidence;
- customer-facing use or selling context;
- named positioning object and version;
- proposed customer/segment lane and exclusions;
- champion and cross-functional decision participants;
- decision owner and unresolved scope conflicts;
- source IDs for every field.

## Evidence, source, and field rules

The OA2 dossier supplies the paraphrased preflight method only. It does not
prove readiness or team alignment. Book content beyond the dossier is not
reconstructed; use `SOURCE_GAP` if such a detail becomes load-bearing.

Every field is `known`, `inferred`, `unknown`, or `conflicted`. `Known` requires
a source that can speak for the field. Team preference may establish intended
scope, but it cannot establish a customer or market fact. A conflict is stated
with both claims and source refs; consensus is not inferred from silence.

## Legal branches

- `ready`: object, purpose, scope, champion, decision owner, and material team
  participation are known, with no unresolved scope conflict.
- `research_needed`: a factual readiness or scope gap has a named evidence
  request and does not require owner choice.
- `owner_review`: the missing item is an owner-only scope, priority, team, or
  risk decision, or stakeholders propose materially different objects/lanes.
- `route_downstream`: positioning is already approved and the request is
  solely a downstream expression or campaign task.
- `blocked`: no positioning object exists, the request combines incompatible
  objects while refusing a split, or it demands substantive positioning before
  resolving a material conflict.

## Procedure

1. Record purpose: first positioning, refresh, material-change review, pitch-
   evidence review, or downstream handoff.
2. Verify the object is available and stable enough to position. Roadmap-only
   claims remain separate from current capability.
3. Bound customer and situation scope; list explicit exclusions.
4. Name champion, decision owner, and participants needed to supply product,
   customer, sales, and market evidence.
5. Classify every field and record conflicts without solving them in prose.
6. Apply one legal branch and issue the smallest next action.

## Closed refusal codes

- `POSITIONING_OBJECT_UNDEFINED`
- `POSITIONING_OBJECT_NOT_READY`
- `EXERCISE_PURPOSE_UNDEFINED`
- `SCOPE_UNDEFINED`
- `INCOMPATIBLE_SCOPES_REQUIRE_SPLIT`
- `CHAMPION_NOT_NAMED`
- `DECISION_OWNER_NOT_NAMED`
- `DECISION_TEAM_INCOMPLETE`
- `MATERIAL_SCOPE_CONFLICT`
- `APPROVED_POSITION_ROUTE_DOWNSTREAM`
- `COMPANY_FACTS_NOT_SUPPLIED`
- `SOURCE_GAP`

## Record shape: `PositioningReadinessDecision`

```yaml
run_id: string
record_type: PositioningReadinessDecision
module_version: positioning-readiness/v3
purpose: {value: first_positioning|refresh|material_change_review|pitch_evidence_review|handoff, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
scope:
  positioning_object: {value: string, version: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
  customer_lane: {value: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
  situation: {value: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
  geography_or_market: {value: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
  exclusions: [{value: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}]
readiness:
  product_or_offer: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
  customer_facing_purpose: {status: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
team:
  champion: {name: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
  decision_owner: {name: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}
  participants: [{role: string, name: string, status: known|inferred|unknown|conflicted, evidence_refs: [string]}]
conflicts: [{field: string, claims: [string], evidence_refs: [string]}]
branch: ready|research_needed|owner_review|route_downstream|blocked
refusal_codes: [string]
prohibited_inferences: [string]
next_action: {action: string, owner: string, evidence_needed: [string]}
source_refs: [OA2-01]
```

## Completion

Complete only when the record has one branch and every required field has a
status. `Ready` admits the scoped exercise; it does not support any positioning
claim and does not promote this proposed runtime.

## Downstream prohibitions

Downstream modules must not broaden the scope, substitute an object, infer
team agreement, treat readiness as customer evidence, or use a downstream
artifact to fill an unknown readiness field.
