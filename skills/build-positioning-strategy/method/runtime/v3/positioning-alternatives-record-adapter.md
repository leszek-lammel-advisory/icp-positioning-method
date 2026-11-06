---
domain: positioning-strategy
runtime: positioning-alternatives-record-adapter
version: 3
status: proposed
depends_on: [M1-v2]
load:
  - ../../01-alternatives-and-status-quo.md
  - ../positioning-alternatives-diagnosis.md
  - ../../sources/dunford-relative-value-dossier.md
---

# V3 Runtime: M1 Observed Alternative Record Adapter

## Purpose

Serialize a completed V2 M1 bounded diagnosis as one machine-resolvable record
without changing V2. The adapter does not run M1, infer alternatives, or
upgrade candidate evidence. It is an additive V3 transport contract for routes
that require an observed same-scope alternative by ID.

## Admission

Require a completed M1 bounded diagnosis with one observed baseline,
buyer/situation scope, evidence refs, alternative statuses, switching-force
states, native boundaries, and next action. Candidate-only, unknown, or blocked
M1 outputs are not adapted as positive records.

## Record shape: `M1ObservedAlternativeDecision`

```yaml
record_id: string
record_type: M1ObservedAlternativeDecision
module_version: positioning-alternatives-diagnosis/v2-adapter-v3
input_refs: {m1_run_id: string, evidence_inventory_ids: [string]}
scope: {positioning_object: string, buyer: string, situation: string}
evidence_states:
  - {evidence_id: string, state: known|inferred|unknown|conflicted, source_ref: string}
baseline_alternative: {value: string, state: observed, evidence_refs: [string]}
alternative_map:
  - {name: string, status: observed|candidate|excluded|unknown, evidence_refs: [string], reasoning: string}
switching_forces:
  push: {state: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
  pull: {state: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
  anxiety: {state: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
  habit: {state: known|inferred|unknown|conflicted, evidence_refs: [string], reasoning: string}
decision_mode: bounded_diagnosis
prohibited_inferences: [string]
next_action: {action: string, owner: string, evidence_needed: [string]}
source_refs: [string]
```

## Invariants

- Every observed alternative resolves to direct same-scope evidence.
- Every known switching force has a non-empty evidence list.
- Unknown forces stay unknown and do not block adaptation when the observed
  baseline itself is supported.
- The adapter may be consumed only with exact scope parity and unchanged
  evidence states.
