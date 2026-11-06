# Positioning Runtime Routing

Load M1 first whenever buyer alternatives or current behavior are uncertain.
M1 through KB-7 are tested and runtime-eligible. This does not license loading
the entire domain for every task: load the smallest route that owns the decision
and preserve the upstream evidence states in the handoff.

| Task | Required context | Must not decide |
|---|---|---|
| Real alternative or status quo | M1 | Category, segment, copy. |
| Why this offer matters | M1 + KB-2 | Unsupported outcome or proof claim. |
| Existing category or new frame | M1 + KB-2 + KB-3 | Current buyer perception without evidence. |
| Initial group / adoption risk | M1 + KB-2 + KB-3 + KB-4 | Beachhead from reachability alone. |
| What buyers currently believe | KB-5 + audience evidence | Desired perception as current fact. |
| Why buyers change or stall | M1 + KB-6 | Force strength or conversion without evidence. |
| Validate a message | M1 + KB-2 + KB-3 + KB-7 | Upstream strategy from preference alone. |

Every run records known, inferred, unknown, and conflicted evidence. A module
may narrow or block a decision; it must not silently repair a missing upstream
input with generic market knowledge.
