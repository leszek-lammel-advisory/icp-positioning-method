# ICP and Positioning Method

An evidence-first method for B2B positioning and ideal customer profile (ICP)
work, packaged as a skill for Claude Code and Claude. It is also readable as a
plain handbook if you want to run it by hand.

Most positioning work starts with a tagline or a category and works backwards.
This method goes the other way. It starts from what your buyers would do if
you did not exist, and only moves forward when the evidence supports each
step:

```
real alternative -> distinct capability -> differentiated value
  -> best-fit customer (ICP) -> market style -> pitch validation
```

Every link limits the next one. If the alternative is imagined, the value is
invented. If the value is only asserted, the ICP is wishful. If you pick a
category first, everything after it is theatre.

The method will tell you "we do not know yet" when that is the honest answer,
and it will name the exact evidence that would change the decision.

## Who it is for

- B2B founders doing positioning for the first time or after a pivot.
- Marketing, GTM, and RevOps leads who need an ICP that is more than a
  firmographic filter.
- Agencies and consultants who run positioning workshops for clients and want
  an auditable trail from evidence to decision.

## What "ICP" means here

In this method the ICP is the **best-fit customer**: the customers who care
most about your differentiated value, can buy, and can be reached. Every
characteristic in the ICP has to explain *why* the value matters more to that
group. Industry, headcount, and title alone are refused as an ICP
(`CUSTOMER_FIT_FROM_FIRMOGRAPHICS_ONLY`), because a list filter says nothing
about why someone would buy.

Best fit is also kept separate from a beachhead. "Who values this most" and
"which first group can create references for the next one" are different
questions with different evidence.

## What is in the repo

```
skills/build-positioning-strategy/
  SKILL.md                     entry point: routing, refusal gate, method cards
  references/                  output contract and run record template
  method/
    00-domain-overview.md      the chain and the module map
    01-09 *.md                 handbooks, one per decision
    runtime/                   step-by-step workflows with output shapes
    runtime/v3/                router, readiness, capability, ICP, market style,
                               pitch validation, stewardship
    versions/                  extensions to KB-3 and KB-7
    sources/                   short paraphrased source dossiers
    source-claim-gap-matrix-v3.md
  agents/openai.yaml           display metadata for agent hosts that read it
templates/
  evidence-card.md             fill this in before you start
```

### Module map

| Module | Question it answers | Handbook | Workflow |
|---|---|---|---|
| Readiness (V3) | Are we ready, and what exactly are we positioning, for whom? | n/a | `runtime/v3/positioning-readiness-and-scope.md` |
| M1 | What does the buyer really do instead? | `01-alternatives-and-status-quo.md` | `runtime/positioning-alternatives-diagnosis.md` |
| V3-DC | What can we do that the real alternative cannot? | `08-distinct-capability-identification-v3.md` | `runtime/v3/positioning-distinct-capability.md` |
| KB-2 | Why does that difference matter to the buyer? | `02-differentiated-value.md` | `runtime/positioning-differentiated-value.md` |
| V3-BFC | Who cares most about that value (the ICP)? | `09-best-fit-customer-selection-v3.md` | `runtime/v3/positioning-best-fit-customer.md` |
| KB-3 | Which market frame or style makes the value obvious? | `03-market-frame-choice.md`, `versions/kb-3-market-style-v3.md` | `runtime/positioning-market-frame-choice.md`, `runtime/v3/positioning-market-style.md` |
| KB-4 | Is there a real beachhead, or just a reachable segment? | `04-adoption-and-beachhead.md` | `runtime/positioning-adoption-beachhead.md` |
| KB-5 | What do buyers believe about us today? | `05-perception-and-current-position.md` | `runtime/positioning-perception-diagnosis.md` |
| KB-6 | Why do buyers switch or stall? | `06-demand-side-switching.md` | `runtime/positioning-demand-switching.md` |
| KB-7 | Does this wording communicate the position? Does a qualified pitch support it? | `07-expression-validation.md`, `versions/kb-7-qualified-pitch-validation-v2.md` | `runtime/positioning-expression-validation.md`, `runtime/v3/positioning-qualified-pitch-validation.md` |
| Stewardship (V3) | Should the approved positioning change? | n/a | `runtime/v3/positioning-stewardship.md` |

"V2" modules are the original, tested set. "V3" modules were added later and
are marked `proposed`: they follow the same rules but have not yet been
calibrated on as many live cases.

## How to use it

### With Claude Code

1. Copy the skill folder into your project or your personal skills folder:

   ```bash
   # project-level
   mkdir -p .claude/skills
   cp -R skills/build-positioning-strategy .claude/skills/

   # or personal, available in every project
   mkdir -p ~/.claude/skills
   cp -R skills/build-positioning-strategy ~/.claude/skills/
   ```

2. Fill in `templates/evidence-card.md` (or paste your raw notes, call
   transcripts, win/loss notes, and product docs).
3. Run `/build-positioning-strategy` or just ask for positioning or ICP work,
   and point it at your evidence.

All paths inside the skill are relative to the skill folder, so keep the
folder structure intact.

### With Claude (claude.ai or the desktop app)

Zip the `skills/build-positioning-strategy` folder and upload it as a custom
skill (in Settings, under Capabilities, where skills are enabled for your
account). Then start a chat, attach your evidence, and ask for the decision
you need.

### By hand

Read `method/00-domain-overview.md`, then the handbook for the decision you
need (start with `01-alternatives-and-status-quo.md` if you are unsure). Each
handbook has a procedure, worked examples, and failure modes. Use
`templates/evidence-card.md` to collect inputs and the matching `runtime/`
file as a checklist for the output.

## Example flow

A fictional company, **Northwind Ledger**, sells software that keeps approved
vendor changes in sync between a purchasing tool and an accounting system.
The founder asks: "Who is our ICP, and how should we position?"

1. **Readiness.** The skill fixes the scope: Northwind Ledger v2, finance
   operations teams in mid-market companies, month-end close. It also records
   who owns the decision before any analysis starts.
2. **Alternatives (M1).** From six customer interviews, the observed
   alternative is a shared spreadsheet plus a weekly reconciliation meeting.
   The founder's list of three competitor vendors is recorded as `candidate`,
   because no buyer mentioned them.
3. **Distinct capability.** "Approved vendor changes sync to both systems
   within minutes" is compared against the spreadsheet. Possession is shown in
   a demo; the contrast is supported by interview notes. Result:
   `supported_capability`.
4. **Differentiated value (KB-2).** Baseline and difference are supported.
   "Fewer payment errors at close" is plausible but only one customer reported
   it. Result: `hypothesis`, with a request for before/after error counts.
5. **ICP (best-fit customer).** Interviews show the value is most acute for
   teams with several purchasing entities and a recent audit finding. The
   skill keeps those two characteristics because each changes why the value
   matters, and excludes single-entity companies even though they look
   similar. Because the value from step 4 is still a hypothesis, this is a
   research lane, not a declared ICP. Result: `best_fit_hypothesis`, terminal
   status `owner_review`, plus the evidence that would confirm it.
6. **Market style.** Not yet run. The value chain is still a hypothesis, so
   the skill names the evidence needed before a category or style choice.

Every step returns a short decision packet: the decision, the evidence it
used, what it refused to assume, what nobody may infer from it, and the next
action and owner.

## Ground rules the skill enforces

- It never invents company, customer, competitor, or market facts. Missing
  evidence becomes a research request.
- Every field is `known`, `inferred`, `unknown`, or `conflicted`, and no later
  step may upgrade an earlier state.
- Four requests are refused outright: claiming a capability is distinct
  without evidence about the alternative, picking an ICP from firmographics or
  list size, choosing a new category from novelty or crowding, and treating
  copy preference as proof of positioning.
- Choices that belong to the business (category, accepted risk, positioning
  changes) go to the named owner. The skill recommends; it does not approve.
- It does not write copy. Once positioning is approved, hand it to your
  messaging or copywriting process.

## Sources

The method is an original synthesis. The source dossiers in
`method/sources/` paraphrase a small number of claims from public work by
April Dunford (including *Obviously Awesome*, second edition), Bob Moesta,
Geoffrey Moore, Play Bigger, Al Ries and Jack Trout, and Wynter. They are
pointers, not substitutes: read the originals. None of these authors endorse
or are affiliated with this repo.

## License

MIT. See `LICENSE`.

Built by Leszek Lammel at Lammel Advisory.
