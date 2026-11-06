---
domain: positioning-strategy
task_type: positioning-perception-diagnosis
module: KB-5
version: 2
status: tested
depends-on: [M1, KB-3]
load: [../05-perception-and-current-position.md, ../sources/ries-trout-perception-dossier.md, ../sources/wynter-perception-validation-dossier.md]
---

# Runtime Workflow: Perception Diagnosis

Require a defined audience and buying situation plus audience-facing evidence.
Internal strategy, homepage copy, and a desired frame are coded `desired`, not
current perception. If no relevant audience evidence exists, return
`research_needed` with `NO_AUDIENCE_PERCEPTION_EVIDENCE`. If a request demands
that desired material be reported as an observed buyer fact, return `blocked`
with `DESIRED_NOT_CURRENT`.

1. Record each item as unaided description, comparison, objection, win/loss
reason, message response, desired strategy, or ambiguous. Only a pre-exposure
buyer interview or win/loss record may support current perception. A message
response tests an expression and is never current-perception evidence.
2. Preserve collection method, pre-exposure status, audience, situation,
provenance, and a respondent or source ID per item. Several statements from
one source are never independent confirmation.
3. Synthesize only comparable audience/situation groups. A pattern is
`supported` only when at least two independent relevant records converge and no
unresolved counterevidence in that scope changes the frame; a single record
stays a hypothesis.
4. Return `conflicted` only when comparable buyer claims name both competing
frames and explicitly state their incompatibility; do not average them. Never
state desired perception as current fact.

```yaml
PerceptionDecision:
  fixture_or_run_id: string
  module_version: KB-5/v2
  input_refs: {m1_run_id: string, kb3_run_id: string, audience_evidence_ids: [string]}
  scope: {audience: string, situation: string, evidence_ids: [direct_buyer_evidence_id]}
  evidence_ledger: [{id: string, source_id: string, audience: string, situation: string, class: unaided_description|comparison|objection|win_loss|message_response|desired_strategy|ambiguous, collection_method: buyer_interview|win_loss_record|message_test|internal_artifact|ambiguous, pre_exposure: boolean, provenance: buyer|seller|internal|inference, state: current|desired|ambiguous|inference|counterevidence, frame: string, incompatible_with: string|null, incompatible_with_evidence_ids: [string], claim: string}]
  pattern: {claim: string, state: supported|hypothesis|research_needed|conflicted, evidence_ids: [string], counterevidence_ids: [string]}
  decision: current_perception_supported|perception_hypothesis|conflicted|research_needed|blocked
  refused_generalizations: [string]
  next_test: string
PerceptionReceipt:
  receipt_id: string
  source_dossier_versions: [SRC-RIES-TROUT-PERCEPTION-20260711, SRC-WYNTER-PERCEPTION-VALIDATION-20260711]
  sample_limits: string
  decision: current_perception_supported|perception_hypothesis|conflicted|research_needed|blocked
  refusal_codes: [NO_AUDIENCE_PERCEPTION_EVIDENCE|DESIRED_NOT_CURRENT|INCOMPARABLE_AUDIENCE|SINGLE_RECORD_NOT_PATTERN|UNRESOLVED_FRAME_CONFLICT]
  persist_to: "runs/<fixture_or_run_id>.md"
```
