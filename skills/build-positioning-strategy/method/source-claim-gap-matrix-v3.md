---
domain: positioning-strategy
artifact: source-claim-gap-matrix
version: 3
status: proposed
source_dossier: sources/dunford-obviously-awesome-second-edition-dossier.md
---

# V3 Source-Claim Gap Matrix

## Purpose

This matrix limits what the provisional second-edition dossier may contribute
to V3. It maps method claims to the new prose contracts, names the evidence a
company decision still requires, and prevents missing source spans from being
silently reconstructed. It does not modify or supersede any tested V2
handbook, runtime, fixture, or release claim.

## Admission rule

All `OA2-*` claims are `use_with_caveat`. They can define a method or decision
boundary. They cannot establish a product capability, competitive difference,
customer, market, prospect qualification, category, or positioning change.
Every company-specific field must retain one of `known`, `inferred`, `unknown`,
or `conflicted` and cite separate evidence.

If a decision depends on book content that the dossier does not paraphrase,
record `SOURCE_GAP`. Adjacent claims, the tested V2 corpus, and general
positioning knowledge may not be used to pretend the missing content was
read.

## Claim matrix

| Claim | V3 use | Primary destination | Company evidence still required | Prohibited inference | Residual gap |
|---|---|---|---|---|---|
| `OA2-01` | Readiness and scope checks before a positioning exercise. | `runtime/v3/positioning-readiness-and-scope.md` | Product readiness, exercise purpose, positioning object, scope, champion, and decision-team records. | Passing a checklist proves the positioning is correct. | Preflight details beyond the paraphrased checks remain `SOURCE_GAP`. |
| `OA2-02` | Dependency order from alternatives through market style. | `runtime/v3/task-routing.md` | Resolvable upstream decision records for the same scope. | A downstream artifact can repair or upgrade an upstream state. | Paraphrased chain only; further elaboration is not reconstructed. |
| `OA2-03` | Identify comparative capabilities before KB-2 evaluates value. | `08-distinct-capability-identification-v3.md`; `runtime/v3/positioning-distinct-capability.md` | Product or operating evidence and same-scope alternative evidence. | Feature presence proves distinctness or buyer value. | The source defines the test, not any company's capability set. |
| `OA2-04` | Select a value-linked best-fit customer hypothesis. | `09-best-fit-customer-selection-v3.md`; `runtime/v3/positioning-best-fit-customer.md` | KB-2 value record, customer evidence, buying feasibility, and reachability evidence. | Firmographics, list availability, or reachability alone prove best fit or a beachhead. | KB-4 remains the adoption/beachhead owner. |
| `OA2-05` | Compare three market styles and their execution burden. | `versions/kb-3-market-style-v3.md`; `runtime/v3/positioning-market-style.md` | Buyer comprehension, expectation fit, value fidelity, subsegment coherence, and capacity evidence. | A style recommendation declares a category or commits the company. | Actual style and accepted burden remain owner decisions. |
| `OA2-06` | Interpret structured pitch evidence from qualified best-fit prospects. | `versions/kb-7-qualified-pitch-validation-v2.md`; `runtime/v3/positioning-qualified-pitch-validation.md` | Qualification record, live pitch record, approved positioning snapshot, and observed response evidence. | One call, preference, synthetic response, or deal event automatically changes positioning. | Synthetic fixtures can prove method behavior only, never live validation. |
| `OA2-07` | Hand approved positioning to a maintained messaging source. | `runtime/v3/positioning-stewardship.md` | Owner-approved positioning record, receiver, version, and handoff acknowledgement. | The positioning domain writes or approves channel copy. | Message-source format and downstream copy approval remain outside this domain. |
| `OA2-08` | Assign stewardship and reopen on material change. | `runtime/v3/positioning-stewardship.md` | Named steward, owner-approved cadence, change evidence, and affected decision IDs. | A calendar date or weak signal forces a positioning rewrite. | Cadence and materiality thresholds are company decisions. |

## Cross-claim gaps

| Gap ID | Gap | Required behavior |
|---|---|---|
| `GAP-V3-01` | The dossier is a short paraphrase of the book, not the book. | Keep every V3 artifact `proposed`; record `SOURCE_GAP` when missing text is load-bearing. |
| `GAP-V3-02` | No company facts are supplied. | Return research, owner review, or a block instead of a filled positioning answer. |
| `GAP-V3-03` | The V3 branch contract has synthetic fixture proof but no live company or qualified-prospect calibration. | Permit `fixture_proven` for the machine contract only; do not claim live calibration, canonical status, or market truth. |
| `GAP-V3-04` | V2 and V3 use different additional layers. | Preserve tested V2 contracts; bridge through their declared inputs rather than editing or reinterpreting them. |
| `GAP-V3-05` | Live qualified-pitch evidence is not present in the source. | Treat synthetic and historical examples as method inputs only; live-signal claims require live records. |

## Promotion boundary

These prose files specify proposed behavior. During development they were
checked against synthetic fixture records and validators (not shipped in this
package), which establish branch-contract proof at `fixture_proven` only. They do not establish live-calibrated runtime behavior,
canonical promotion, market truth, or V2 mutation. Independent skill proof and
owner approval remain separate gates.
