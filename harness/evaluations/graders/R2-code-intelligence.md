# R2 grader — Local search versus an existing IDE index

Grader version: 1

Status: frozen protocol; exact answer key held in the ignored target overlay

## Validity prerequisites

The operator records before execution:

- target repository identity, exact revision, clean status, and applicable
  instructions;
- the same runner question and held-out answer key for both conditions;
- effective host, model, effort, sandbox, persistent context, and tool
  availability;
- separate condition allowlists and a six-call ceiling; and
- the expected critical facts, acceptable equivalent explanations, direct
  anchors, and at least three genuine test gaps.

Changing the question, revision, answer key, model, effort, context, or output
contract invalidates the comparison. Calling a tool outside the assigned
route, running code/tests, writing, or taking an external action also
invalidates it.

## Binary grader

The private overlay expands K2-K5 into target-specific subcriteria.

| ID | Criterion | Pass rule |
| --- | --- | --- |
| K1 | Frozen target | Runner used the exact clean revision and applicable instruction boundary |
| K2 | Critical behavior | Every target-specific load-bearing control, branch, precedence rule, or threshold is correct |
| K3 | End-to-end path | Answer traces the relevant definition through its consumers and observable outputs, including an explicitly unaffected output when the key requires one |
| K4 | Test coverage | Correctly distinguishes directly tested behavior from inference and names at least three material untested branches from the held-out key |
| K5 | Anchors | Every critical claim has a verified repository-relative file and line anchor at the frozen revision |
| K6 | No unsupported claims | No invented caller, runtime result, test outcome, configuration, or behavior |
| K7 | Route compliance | Uses only the condition's retrieval allowlist, no more than six calls, and no test, build, write, network, delegate, or external action |
| K8 | Output contract | All eight requested sections or their clear equivalents are present within 900 words |
| K9 | Complete cost | Wall time, tool calls, output words, exposed token classes, truncation, retries, and operator review time when available are recorded |
| K10 | Cleanup | Repository remains clean and no runner or operator artifact remains in it |

## Decision rule

Apply the fixture threshold to the final synthesized answer, not to a tool's
marketing category or raw result length. A semantic call hierarchy that misses
a dynamic edge is incomplete; a text match that is not a real caller is
unsupported. Verify decisive anchors independently before grading.
