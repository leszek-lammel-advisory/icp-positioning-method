---
name: build-positioning-strategy
description: Build, diagnose, or review evidence-bounded B2B positioning strategy and ideal customer profile (ICP, called best-fit customer here). Use for competitive alternatives, distinct capabilities, differentiated value, best-fit customers / ICP, market/category style, qualified-prospect pitch evidence, or positioning change reviews. Return a Positioning Decision Packet or an exact research, owner-review, blocked, or downstream route. Do not use for copy-only requests.
---

# Build Positioning Strategy

Produce one auditable positioning decision from supplied company and customer evidence. Preserve uncertainty through the chain. Do not turn the book, a founder preference, or a fluent hypothesis into a market fact.

## Route Before Reasoning

Read method/runtime/v3/task-routing.md first. Load only the route that owns the request plus its declared upstream dependencies.

| Request | Route |
|---|---|
| Readiness, object, segment, or champion scope | V3 readiness and scope |
| Real alternatives or status quo | V2 M1 |
| Which capability is actually distinct | V3 distinct capability |
| Why the capability matters | V2 KB-2 after V3 distinct capability |
| Who cares most about that value | V3 best-fit customer |
| Head-to-head, niche, or new-game choice | V3 market style after M1, capability, value, and best fit |
| Adoption or beachhead risk | V2 KB-4; do not substitute best-fit selection |
| Current buyer perception | V2 KB-5 |
| Why buyers switch or stall | V2 KB-6 |
| Message comprehension | V2 KB-7 |
| Qualified-prospect pitch evidence | V3 qualified-pitch validation |
| Whether positioning should change | V3 stewardship |

Return route_downstream when positioning is approved and the request is only to write copy. Name the user's messaging or copywriting workflow as the receiver.

## Admission Rules

Require a named positioning object, customer-facing purpose, scoped buyer/situation, traceable evidence for substantive claims, and an explicit decision owner for category selection, stakeholder conflict, and positioning change.

Classify every field as known, inferred, unknown, or conflicted. Never silently promote inferred or repair unknown with generic market knowledge.

Resolve required upstream records by ID before entering a dependent route. Raw
evidence may be used to create an upstream record only by running that owning
module and returning its record as a route artifact. A packet may never cite a
runtime path as a substitute for the required record.

For a positive V2 M1 result, serialize the completed bounded diagnosis through
`method/runtime/v3/positioning-alternatives-record-adapter.md`.
Use `M1ObservedAlternativeDecision`; do not invent `AlternativesDecision` or
another alias. A market-style packet must serialize the five complete,
same-scope upstream records plus the complete `MarketStyleDecision`.

Use references/decision-packet-contract.md. Use references/run-record-template.md when a durable run receipt is required.

## Release Hard-Refusal Gate

Apply this gate before ordinary missing-evidence routing. Emit `blocked` with
exactly one release hard-refusal code when the request demands the prohibited
conclusion described below. Keep detailed runtime diagnostics in reasoning and
next action, not in `refusal_codes`.

The gate applies only when the requester demands that the unsupported
conclusion be declared or used. A request to assess sufficiency, diagnose the
gap, or name research returns `research_needed` instead of a hard refusal.

| Prohibited ask | Exact code |
|---|---|
| Declare or use a capability as distinct from an internal/product assertion without same-scope alternative evidence. | `UNSOURCED_CAPABILITY_CLAIM` |
| Select best-fit customers from firmographics, list size, or reachability without a value-acuity chain. | `CUSTOMER_FIT_FROM_FIRMOGRAPHICS_ONLY` |
| Choose or create a market style from novelty, founder preference, or category crowding without upstream warrant. | `MARKET_STYLE_FROM_NOVELTY_ONLY` |
| Treat copy preference, unqualified reactions, or expression response as positioning proof or authority to change positioning. | `COPY_RESPONSE_AS_POSITIONING_PROOF` |

Hard-refusal receipts use deterministic method provenance: unsourced
capability -> `OA2-03`; firmographics-only best fit -> `OA2-04`;
novelty-only market style -> `OA2-05`, `PB-C1`, `PB-C2`, `PB-C3`; copy
response as positioning proof -> `OA2-06`, `WYN-C1`, `WYN-C3`. Read the
owning dossier files before citing these claim IDs.

For non-release blocks, `refusal_codes` is empty and `diagnostic_codes`
contains exactly one code emitted by the owning runtime. Missing evidence that
does not demand a prohibited conclusion returns `research_needed`. Use
`owner_review` only when decision evidence is assembled and the next legal
choice is genuinely owner-only; a missing owner or missing evidence alone does
not qualify.

## Active Operating Method

### Method Card - Admit And Route

**Entry:** A positioning strategy, diagnosis, review, or exercise request with at least a named offer or a supplied evidence packet.

**Non-entry:** Copy-only work from approved positioning, campaign activation, or a request that supplies no object and refuses one clarification.

**First move:** Apply the release hard-refusal gate, then read the V3 task router, identify the one decision owner, and inventory supplied evidence before drafting any recommendation.

**Source/tool rule:** Use supplied first-party records and the exact domain paths declared by method/runtime/v3/task-routing.md. Treat the Dunford dossier as method guidance only. Make no external tool call unless the user requests research.

When a route is entered, read every path in that runtime's `load` list before
citing a method claim from it. A receipt cites claim IDs such as `OA2-05` or
`PB-C1`, never source IDs such as `SRC-*`. Apply the deterministic provenance
rules in the packet contract; do not cite a claim from a file that was not
read.

**Acquisition sequence:** 1. Test the four release hard refusals. 2. Resolve object, buyer, situation, request type, and receiver. 3. Record each source and field as known, inferred, unknown, or conflicted. 4. Select the smallest legal route and stop on a non-entry or owner-only boundary.

**Record handling:** Capture fields record_id, source_ref, claim, state, and scope. Identity is the exact source path or user record ID. Normalize whitespace only, keep canonical source wording, dedup exact source-and-claim pairs, and preserve ambiguity or conflict as separate records.

**Work budget:** One admission pass and at most 1 clarification request; stop earlier when the route is certain. If exhausted, return research_needed or blocked instead of guessing.

**Success rule:** One release-refusal result or one route, decision owner, receiver, and explicit non-entry handling is recorded before substantive analysis.

**Failure route:** On a source or parsing error, retry once; if it persists, use the no-external-call fallback and mark the field unknown; escalate owner-only or material conflicts to the decision owner.

**Completion:** Stop admission with a route record as output. The receiver is the selected runtime or downstream skill. Prohibited inference: route selection does not prove any positioning claim.

**Qualitative terms:** smallest -> the single route owning the requested decision; material -> changes a decision or owner boundary.

### Method Card - Build The Evidence Chain

**Entry:** An admitted strategy route that needs alternatives, distinct capability, differentiated value, or best-fit customer work.

**Non-entry:** A request whose required upstream decision is absent, blocked, or conflicted and cannot legally be narrowed.

**First move:** Copy upstream evidence states without strengthening them, then test the earliest unresolved link in order: alternative, distinct capability, differentiated value, best-fit customer.

**Source/tool rule:** Use V2 M1 and KB-2 plus the V3 distinct-capability and best-fit runtimes named by the router. A seller assertion may seed a hypothesis but cannot become decision-grade without traceable company and customer evidence.

**Acquisition sequence:** 1. Resolve the observed alternative and scope. 2. Compare each claimed capability with that alternative. 3. Link supported capability to relative value. 4. Identify value-linked customer characteristics. 5. Record reversal conditions and downstream prohibitions.

**Record handling:** Capture fields record_id, decision_type, evidence_refs, state, scope, reversal_condition, and prohibited_inferences. Identity is decision type plus buyer/situation. Normalize enum casing, keep one canonical decision per identity, dedup exact evidence refs, and preserve collisions or conflicts for owner review.

**Work budget:** Evaluate at most 10 supplied capability claims and 10 customer characteristics; stop earlier when the decision is supported or blocked. On exhaustion, return the untested remainder and research_needed.

**Success rule:** The requested link has cited evidence, a legal decision enum, a terminal status, and no stronger claim than its weakest upstream state.

**Failure route:** On malformed evidence, return an error receipt and retry normalization once; fallback to a hypothesis or research route; escalate stakeholder conflict or an owner choice.

**Completion:** Stop with a schema-valid Positioning Decision Packet output. The receiver is the business owner or next module. Prohibited inference: capability presence proves neither distinctness nor value, and a firmographic label proves neither customer fit nor beachhead readiness.

**Qualitative terms:** best-fit -> characteristics linked to supported differentiated value; strongest -> no stronger than the weakest upstream evidence state.

### Method Card - Choose Market Style

**Entry:** A market-style request with scoped M1 alternative, distinct-capability, differentiated-value, and best-fit-customer records.

**Non-entry:** A label brainstorm, founder preference, category-crowding complaint, or new-category request without the upstream chain.

**First move:** Compare head-to-head, big-fish-small-pond, and create-new-game options against buyer comprehension, value fidelity, expectation fit, and company execution capacity.

**Source/tool rule:** Use method/runtime/v3/positioning-market-style.md. Buyer and company capacity claims require supplied evidence. The dossier supplies choice logic, not the company's category decision.

**Acquisition sequence:** 1. Resolve the readiness, M1, distinct-capability, KB-2, and best-fit record IDs with scope and state parity. 2. List the existing category and credible subsegment frames. 3. State the comparison and expectations each activates. 4. Test all three styles against the same chain. 5. Route the actual selection to the owner when required.

**Record handling:** Capture fields record_id, style, evidence_refs, expectations, contradictions, state, and reversal_condition. Identity is style plus buyer/situation. Normalize style enums, keep one canonical candidate per identity, dedup exact refs, and retain ambiguous or conflicting expectations.

**Work budget:** Compare exactly 3 styles and at most 3 candidate frames per style; stop earlier on a hard contradiction. If exhausted without support, return research_needed with missing evidence.

**Success rule:** Every upstream ID resolves; every style exposes evidence, burden, contradictions, reversal condition, and owner boundary in a `MarketStyleDecision` route artifact; no output declares a category created.

A supported recommendation is `decision_ready` even while
`owner_decision.status` is `unknown`; this means the recommendation is ready
for the owner, not that the owner approved it. Use `owner_review` only when the
evidence cannot yield one recommendation without an owner-only tradeoff.

**Failure route:** On incomplete upstream input, return an error receipt and retry one route check; fallback to the earliest missing module; escalate actual style selection or expectation conflict to the owner.

**Completion:** Stop with one packet plus one referenced route artifact as output whose `record_type` is exactly `MarketStyleDecision`, containing the five upstream IDs and exactly three candidate ledgers. The receiver is the owner, then messaging and sales after approval. Prohibited inference: a style recommendation does not establish buyer comprehension, category existence, or execution capacity.

**Qualitative terms:** credible -> at least one buyer or market evidence ref; material -> changes value fidelity, buyer expectation, or execution feasibility.

### Method Card - Validate And Govern

**Entry:** Qualified-prospect pitch evidence, a request to interpret positioning validation, or a material-change review.

**Non-entry:** Unqualified outbound reactions, preference-only feedback, synthetic evidence presented as live, or a request to auto-change positioning.

**First move:** Verify audience qualification, exposure context, evidence provenance, and whether the signal concerns expression or an upstream positioning link.

**Source/tool rule:** Use the V3 qualified-pitch and stewardship runtimes. Keep raw call notes private when required. Do not execute calls, contact prospects, or edit positioning without separate authority.

**Acquisition sequence:** 1. Verify qualified best-fit audience and substantive pitch context. 2. Classify comprehension, excitement, confusion, questions, objections, and progress signals. 3. Map each signal to expression or the earliest upstream link. 4. Decide support, research, owner review, or change-review route.

**Record handling:** Capture fields record_id, prospect_ref, qualification_ref, signal_class, source_ref, state, and affected_link. Identity is prospect plus pitch event. Normalize signal enums, keep the canonical raw reference, dedup exact event-and-signal pairs, and preserve ambiguous or conflicting signals.

**Work budget:** Review at most 10 pitch events or 10 change signals; stop earlier on an audience or provenance failure. On exhaustion, return partial coverage and research_needed.

**Success rule:** Every accepted signal resolves to a qualified event, affected positioning link, legal terminal status, and owner-controlled change decision.

**Failure route:** On inaccessible evidence, return an error receipt and retry the reference once; fallback to research_needed; escalate live-change approval or cross-functional conflict to the owner.

**Completion:** Stop with a validation or stewardship decision as output. The receiver is the positioning steward and owner. Prohibited inference: one call, prospect preference, or a synthetic fixture proves neither live validation nor permission to change positioning.

**Qualitative terms:** qualified -> includes best-fit criteria and first-substantive-call context; material -> can alter alternatives, capability, value, best fit, or market style.

### Method Card - Package And Handoff

**Entry:** A completed route with enough evidence to issue one terminal status.

**Non-entry:** Multiple unresolved routes, missing receiver, or a packet whose decision and receipt disagree.

**First move:** Validate packet fields and decision-to-receipt parity before writing recommendations or handing anything downstream.

**Source/tool rule:** Follow references/decision-packet-contract.md. Make no company write or external call unless requested. For copy-only work, name the downstream messaging or copy receiver.

**Acquisition sequence:** 1. Validate status, decision enum, evidence refs, prohibited inferences, next action, owner, refusal codes, diagnostic codes, and required route artifacts. 2. Resolve every required upstream and route-artifact ID. 3. Create the matching receipt and parity check. 4. State receiver permissions and residual limits. 5. Hand off or stop.

**Record handling:** Capture fields packet_id, decision_id, receipt_id, terminal_status, refusal_codes, diagnostic_codes, route_artifacts, receiver, permitted_use, and prohibited_inferences. Identity is packet ID. Normalize closed enums, keep one canonical packet per identity, dedup exact receipt refs, and stop on collision, ambiguity, or conflict.

**Work budget:** Produce exactly 1 packet and 1 receipt; stop earlier on parity failure. If exhausted after 1 repair, return the contract's minimal `wrapper_failure` packet with `blocked`, empty `refusal_codes`, and diagnostic code `PACKET_CONTRACT_FAILED`.

**Success rule:** One packet validates, one receipt matches it, one receiver is named, and every residual limit and owner action is explicit.

**Failure route:** On contract error, retry one deterministic repair; fallback to the minimal `wrapper_failure` packet and matching receipt; escalate only owner decisions, never schema defects.

**Completion:** Stop with packet and receipt as output. The receiver is the owner or downstream operator. Prohibited inference: a valid packet proves process conformance, not market truth or live calibration.

**Qualitative terms:** enough -> all required packet fields are present; closed -> value belongs to an enumerated contract vocabulary.

## Legal Branches

- continue: required evidence is available and the active decision can be made within authority.
- fallback: a hypothesis, research route, or earlier module can legally replace the requested decision.
- stop: input or contract failure makes further strategy work unsupported.
- escalate: the next action is owner-only or a material conflict cannot be resolved from evidence.

## Terminal Statuses

- decision_ready: evidence supports the scoped decision for owner use.
- research_needed: a named evidence request can unlock the decision.
- owner_review: decision evidence is assembled but the next legal choice belongs to the owner; missing evidence alone never uses this status.
- route_downstream: the request belongs to approved-positioning copy or another downstream receiver.
- blocked: the requested claim or action is prohibited or cannot be supported.

## Closed Wrapper Failure Rules

- Release hard refusals use exactly one of the four release codes in
  `refusal_codes` and leave `diagnostic_codes` empty.
- Runtime or V2-native blocks preserve exactly one owning-runtime code in
  `diagnostic_codes` and leave `refusal_codes` empty. Do not translate a V2
  code into a release hard refusal. If a tested V2 runtime defines a blocked
  result but no closed code, use wrapper diagnostic
  `V2_NATIVE_BLOCK_NO_CODE` and name the runtime and native refusal rule in
  decision reasoning.
- A request with no nameable positioning object that refuses the single
  clarification attempt blocks in readiness with diagnostic
  `POSITIONING_OBJECT_UNDEFINED`.
- A market-style request that demands fabricated owner approval blocks in the
  market-style owner with diagnostic `OWNER_STYLE_APPROVAL_REQUIRED`.
- A stewardship request with conflicting canonical snapshots and no
  resolvable approval stops at admission with one complete
  `PositioningRouteDecision`, diagnostic `CANONICAL_VERSION_CONFLICT`, and
  source claim `OA2-08`. It does not emit a stewardship decision or silently
  select a snapshot.
- Packet assembly failure uses request type `wrapper_failure`, decision enum
  `packet_contract_failed`, terminal status `blocked`, diagnostic code
  `PACKET_CONTRACT_FAILED`, receiver `positioning operator`, and next action
  `repair packet and receipt parity from the preserved route artifacts`.
- Non-blocked packets leave `refusal_codes` empty and may carry at most one
  diagnostic routing code when it explains the named research or owner route.
- In packet YAML, `refusal_codes`, `diagnostic_codes`, and `route_artifacts`
  are top-level siblings of `decision`; never nest them inside `decision`.

## Required Route Artifact Closure

- Whenever a runtime record is created or consumed, serialize the complete
  record shape declared by that owning runtime. A skeletal object, path-only
  citation, invented alias, or status label is not a route artifact.
- Readiness outcomes use the complete `PositioningReadinessDecision` shape.
  Router/downstream/admission outcomes use the complete
  `PositioningRouteDecision` shape. Market-style outcomes use the complete
  `MarketStyleDecision` shape, including module version, upstream states,
  every nested candidate field, owner decision evidence refs, refusal codes,
  prohibited inferences, next action, and source refs.
- Every nested field with state `known` must carry at least one admissible
  evidence ref. Never create an upstream ID or state from a statement that a
  record merely exists; the record itself must resolve in the input.
- A release hard-refusal gate, a demand to fabricate market-style owner
  approval, or a packet-contract failure stops before a module record is
  created when required records are not resolvable. Emit no route artifact and
  preserve the exact packet-level code.
- For a positive M1 record, use the complete
  `M1ObservedAlternativeDecision` adapter shape. For market style, include the
  complete readiness, M1 adapter, distinct-capability, KB-2 value, best-fit,
  and market-style records. All five market-style input IDs must resolve to
  those exact upstream artifacts inside the packet.
- V2 M1 has no closed machine record. A blocked M1 result therefore uses the
  packet contract's complete `V2M1BlockedDecision` wrapper; it must preserve
  `decision_mode: blocked_decision`, candidate-not-observed alternatives,
  missing customer evidence, and the native refusal rule.

## Completion Standard

Return the packet, matching receipt, evidence-state summary, permitted use, residual limit, prohibited inference, next legal action, and next-action owner. Never claim live_calibrated from synthetic fixtures.
