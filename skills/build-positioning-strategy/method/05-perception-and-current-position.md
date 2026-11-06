---
domain: positioning-strategy
module: KB-5
status: tested
sources:
  - sources/ries-trout-perception-dossier.md
  - sources/wynter-perception-validation-dossier.md
depends_on: [M1, KB-3]
---

# Perception and Current Position

## What this capability decides

Positioning intent answers what the company wants a buyer to understand. Current
perception answers what a defined buyer group already associates with the offer
in a defined buying situation. They can agree, differ, or be unknown. They are
not interchangeable evidence.

This module diagnoses the current interpretation that later positioning work
must contend with. It returns `current_perception_supported`,
`perception_hypothesis`, `conflicted`, `research_needed`, or `blocked`. It does
not choose the desired frame, prove that a message will work, or turn a buyer
description into a market-wide truth.

An offer is not interpreted on a blank canvas. Buyers bring a comparison,
category expectation, and prior language to it. That is why an internal label
can be clear to its author yet fail to describe the interpretation a buyer
actually brings. The practical consequence is simple: record the buyer's words
and comparison before trying to repair the message.

## Keep these records separate

| Record | What it can establish | What it cannot establish |
|---|---|---|
| Unaided buyer description | How this buyer describes the offer before being taught a label. | The view of every buyer or a causal outcome. |
| Buyer comparison | The alternative or category expectation the buyer is using. | That the comparison is shared without repeated relevant evidence. |
| Objection or win/loss record | A reason a buyer rejected, doubted, or preferred an interpretation. | A universal position or a product defect without context. |
| Message response | Whether a particular expression was understood or credible by a matched sample. | The buyer's pre-existing perception or demand. |
| Desired strategy, homepage, sales deck | The seller's chosen expression or intended frame. | Buyer perception. |
| Analyst or seller inference | A candidate interpretation to test. | Evidence of a buyer's mental model. |

The last two rows are useful inputs, but they are coded `desired` or
`inference`, never upgraded to current perception. This prevents the familiar
failure in which "we position ourselves as X" silently becomes "buyers see us
as X."

## Evidence before synthesis

Every evidence item needs five fields: the buyer or source identifier, the
audience, the buying situation, the record class, and the exact claim. Preserve
the source identifier so repeated words from one interview are not counted as
independent confirmation. Preserve the situation so a procurement buyer and an
operator are not averaged into one vague mental position.

Classify each item before combining it:

| State | Meaning | Allowed decision use |
|---|---|---|
| Current | Direct buyer-facing evidence about an existing association or comparison. | May support a bounded pattern. |
| Desired | Internal or seller-selected interpretation. | Comparison target or test stimulus only. |
| Ambiguous | The wording could describe the product, a desired outcome, or a broader category. | Ask a clarifying question; do not code it as a frame. |
| Inference | Analyst interpretation of indirect evidence. | Hypothesis and research design only. |
| Counterevidence | Relevant evidence that materially does not fit the proposed pattern. | Must constrain or split the conclusion. |

The right unit of analysis is a buyer-situation record, not a sentence. "It is
task management" from a project lead during planning can mean something
different from the same words from an operations leader resolving ownership
conflicts. The module may segment such evidence when the situation difference
is evidenced. It may not invent a segment merely to make contradictory records
disappear.

## Decision procedure

### 1. Fix the scope before reading the language

Name the audience, role if relevant, and the buying or use situation. If the
request has no scope, the right output is `research_needed`. A broad statement
such as "the market sees us as..." is not a usable question because it gives no
way to determine which observations are comparable.

### 2. Build an evidence ledger

For each item, record its exact language, record class, provenance, source
identifier, audience/situation fit, and whether it supports, contradicts, or
does not bear on a candidate interpretation. Do not quote only the convenient
buyer language. A loss reason that invokes a different comparison is material
counterevidence.

### 3. Separate interpretation from consequence

"A coordination layer" is an interpretation. "It reduces reconciliation time"
is an outcome claim. The first can be diagnosed with language and comparison
evidence; the second needs KB-2 proof. Do not let a current-perception finding
upgrade an unproven value chain, and do not let a supported value chain prove
that buyers already use the desired interpretation.

### 4. Test convergence and conflict

Call a pattern `supported` only when at least two independent, relevant
buyer-facing records converge on the same interpretation or comparison, the
scope is stated, and no unresolved counterevidence in that same scope changes
the frame. This is a practical evidence floor, not a claim of statistical
representativeness.

One relevant record can form a `perception_hypothesis`; it cannot establish the
current position. No relevant buyer-facing record produces `research_needed`.
When comparable buyer records use incompatible frames, return `conflicted` and
preserve each frame. First investigate whether a real difference in role,
situation, alternative, or lifecycle stage explains the split. If so, rerun the
diagnosis in the evidenced subgroups. If not, do not average the labels into a
new invented category.

### 5. State the smallest conclusion the evidence permits

The output must name the audience and situation, the exact supported or
competing interpretation, the evidence source identifiers, material limits,
and the next test. A supported result is bounded: "Among the interviewed
operations managers handling cross-system handoffs, three independent records
describe the offer as coordination across systems rather than task management."
It is not: "The market sees us as a coordination platform."

## Worked decisions

**Supported, but bounded.** Three independent operations managers in the same
cross-system handoff situation describe the offer as a way to reconcile an
operational view across systems. One explicitly contrasts it with spreadsheet
reconciliation rather than task management. No relevant record conflicts. The
decision is `current_perception_supported` for that audience and situation. It
does not prove that the claim is valuable, persuasive in a campaign, or shared
outside the observed scope.

**Hypothesis, not a pattern.** One recent buyer calls the offer a control layer
after a compliance incident. The language is relevant but singular. The decision
is `perception_hypothesis`; interview comparable buyers before changing the
site or declaring a market position.

**Conflicted, not averaged.** One comparable buyer calls the offer task
management; another says task-management expectations fail because the real
need is authority control. The module returns `conflicted`. It investigates
whether the buyers faced different alternatives or responsibilities. It does
not write "task and authority management" to make both quotes fit.

**Blocked request.** A founder supplies a homepage category and asks the agent
to report how buyers see the offer. With no buyer-facing evidence, the module
returns `research_needed` and refuses `DESIRED_NOT_CURRENT`. If asked to state
the category as an observed buyer fact anyway, it returns `blocked`.

## Failure modes

- Counting several comments from one customer as independent confirmation.
- Treating a message-test preference as a pre-existing mental association.
- Combining records from unrelated roles or situations into a generic position.
- Ignoring a relevant contradictory comparison because the desired label is
  more elegant.
- Treating a category label as either proof of buyer understanding or proof of
  value.
- Letting current perception choose the strategy automatically. KB-3 owns the
  desired frame decision; KB-7 tests an expression of that decision.

## Handoff and research design

Pass downstream a scoped perception statement or a research plan, never an
unqualified slogan. If the pattern is unknown, request recent buyer and
non-buyer interviews, win/loss material, and unaided first descriptions before
showing a proposed label. Ask what the offer is, what it is compared with, what
problem it is expected to solve, and what does not fit. Record role, situation,
and source identifier so future evidence can actually be compared.

KB-7 can test whether a selected expression is understood by a matched audience.
It must not be used to erase a KB-5 conflict or to prove that the upstream
alternative, value chain, or frame is true.

## Source trace

This handbook is original synthesis of the reviewed Ries and Trout public
corpus and Wynter public message-research sources. Ries and Trout supply the
boundary between seller intent and buyer interpretation, plus the role of prior
associations and conflicting meanings. Wynter supplies the audience/situation
and comprehension-versus-preference discipline. Neither source establishes any
company-specific buyer perception.
