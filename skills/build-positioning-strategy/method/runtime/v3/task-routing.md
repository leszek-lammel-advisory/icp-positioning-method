---
domain: positioning-strategy
runtime: task-routing
version: 3
status: proposed
load:
  - ../../source-claim-gap-matrix-v3.md
  - positioning-alternatives-record-adapter.md
---

# V3 Runtime: Task Routing

## Entry

Enter when a request asks for positioning diagnosis, exercise design, distinct
capability, differentiated value, best-fit customer, market style,
qualified-prospect pitch interpretation, or positioning stewardship. The
router chooses the smallest route that owns the requested decision and retains
all upstream states.

## Non-entry

Do not run a positioning decision for approved-position copywriting,
campaign activation, account ranking, CRM work, live pitch
execution, or company research with no positioning question. Return
`route_downstream` and name the receiver. Do not treat a copy request as
authorization to reopen strategy.

## First move

Classify the requested decision and verify whether the named positioning object
and scope have a resolvable V3 readiness record. Readiness is a cross-cutting
admission gate, not a stage that can be inferred from downstream artifacts.

## Route table

| Request | Smallest legal route | Required prior records | Must not decide |
|---|---|---|---|
| Exercise readiness or scope | V3 readiness | Supplied scope and team evidence | Positioning substance. |
| Real alternative or status quo | V3 readiness -> M1 V2 | Readiness `ready` | Capability, value, customer, style, or copy. |
| Distinct capability | Readiness -> M1 -> V3 distinct capability | Observed same-scope M1 alternative | Buyer value from feature evidence. |
| Differentiated value | Readiness -> M1 -> V3 distinct capability -> KB-2 V2 | KB-2 capability records from V3 | Best fit, style, or outcome proof beyond KB-2. |
| Best-fit customer | Readiness -> M1 -> V3 distinct capability -> KB-2 -> V3 best fit | Same-scope upstream records | KB-4 beachhead or adoption decision. |
| Market style | Prior chain -> KB-3 V3 | Best-fit hypothesis and V2 frame evidence | Owner approval or category declaration. |
| Qualified-prospect pitch evidence | Approved snapshot -> KB-7 V2 | Qualification and live pitch records | Automatic positioning change. |
| Handoff, checkpoint, or material change | V3 stewardship | Approved snapshot or named change trigger | Silent mutation or channel copy. |
| Approved-position copy | downstream receiver | Approved positioning ref | Re-run positioning without a change trigger. |

## Evidence and source rules

- Method sources may define tests only; company facts require company evidence.
- The provisional OA2 dossier is `use_with_caveat`. Use `SOURCE_GAP` when a
  decision depends on source content the dossier does not paraphrase.
- A record is admissible only when its ID, version, scope, status, and evidence
  refs resolve. Missing records remain missing.
- A positive V2 M1 bounded diagnosis is transported only as a complete
  `M1ObservedAlternativeDecision` through the V3 adapter. The adapter does not
  alter V2 or make a candidate alternative observed.
- A dependent packet serializes every complete record it consumes. Market
  style requires the complete readiness, M1 adapter, distinct-capability,
  KB-2 value, and best-fit records plus the complete market-style record.
- Preserve `known`, `inferred`, `unknown`, and `conflicted` fields. Never turn
  an inferred or conflicted upstream field into known during routing.
- Load the smallest route. Do not load the whole domain as a substitute for
  selecting an owner.

## Legal branches

- `run_positioning`: one route and its required records are identified.
- `research_needed`: evidence acquisition can resolve the missing route input.
- `owner_review`: the next action is an owner-only scope, style, priority, or
  change decision.
- `route_downstream`: the request belongs to a named non-positioning receiver.
- `blocked`: the request requires invention, bypasses a blocked upstream
  record, or asks the router to make an owner-only commitment.

## Closed refusal codes

Only these codes are legal:

- `ROUTE_SCOPE_UNDEFINED`
- `READINESS_RECORD_REQUIRED`
- `UPSTREAM_RECORD_MISSING`
- `UPSTREAM_SCOPE_MISMATCH`
- `UPSTREAM_STATE_CANNOT_BE_UPGRADED`
- `COMPANY_FACTS_NOT_SUPPLIED`
- `OWNER_DECISION_REQUIRED`
- `COPY_ONLY_ROUTE_DOWNSTREAM`
- `UNAUTHORIZED_EXTERNAL_OR_FILE_WRITE`
- `SOURCE_GAP`

## Record shape: `PositioningRouteDecision`

```yaml
request_id: string
record_type: PositioningRouteDecision
runtime_version: positioning-routing/v3
request_summary: string
decision_scope:
  positioning_object: string
  buyer_or_market: string
  situation: string
  field_statuses: {positioning_object: known|inferred|unknown|conflicted, buyer_or_market: known|inferred|unknown|conflicted, situation: known|inferred|unknown|conflicted}
classified_task: readiness|alternatives|distinct_capability|differentiated_value|best_fit_customer|market_style|qualified_pitch_validation|stewardship|downstream
selected_route: [string]
required_record_refs: [string]
missing_or_conflicted_inputs: [string]
branch: run_positioning|research_needed|owner_review|route_downstream|blocked
receiver: string
refusal_codes: [string]
prohibited_inferences: [string]
next_action: {action: string, owner: string, evidence_needed: [string]}
source_refs: [string]
```

## Completion

Complete when exactly one branch, one receiver, one smallest route, and one
next action are recorded. Routing does not complete any positioning module and
does not change maturity or runtime eligibility.

## Downstream prohibitions

No receiver may use a route decision as evidence that the company is ready,
an upstream claim is true, a market style is approved, a prospect is
qualified, or copy is authorized. Every substantive decision requires its own
runtime record.
