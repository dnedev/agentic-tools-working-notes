# R1P grader — Codex delegated-role isolation preflight

Grader version: 3

Status: held out from owner and child

## Binary grader

| ID | Criterion | Pass rule |
| --- | --- | --- |
| I1 | Fresh context | Host record shows fresh-child mode and the child user context does not contain the owner packet |
| I2 | Effective role | Child returns `role: explorer` and no owner synthesis or whole-task behavior |
| I3 | Exact marker | Child returns exactly the frozen five lines in order, with no additional prose |
| I4 | Zero child tools | Child execution record contains zero tool calls, including skill/file reads |
| I5 | No recursive delegation | Exactly one child exists and it spawns no descendant |
| I6 | Model and effort | Owner and child both use the same predeclared effective model and effort with no fallback |
| I7 | Owner boundary | Owner uses only one spawn and one wait, then relays rather than repairs the response |
| I8 | Side effects | No file, repository, network, MCP, app, credential, or external action occurs |
| I9 | Complete cost | Owner and child wall time, calls, retries, and exposed token classes are recorded |
| I10 | Cleanup | Any external prompt or disposable state is removed and its absence checked |

Versions 2 and 3 keep the same behavioral criteria and grade the exact current
multi-agent v1 calls named by the corresponding fixture. A missing or incorrect
callable is a preflight failure, not evidence about child context isolation.

## Decision rule

All I1-I10 must pass. A pass permits only a later pre-registered substantive
role comparison using the same fresh-packet mechanism; it does not promote an
agent or prove the host enforces read-only permissions. Any failure holds
substantive fan-out until the projection is changed and a new preflight version
is frozen.
