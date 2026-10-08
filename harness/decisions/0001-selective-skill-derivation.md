## ADR: Selective skill derivation with neutral contracts and host-native projections

Status: Accepted

Date: 2026-09-03

Accepted: 2026-09-03

Amended 2026-09-25: catalog and distribution wording generalized for sharing;
the decision is unchanged. The author also runs one complete public plugin
bundle user-wide as a personal trial; that trial is not a catalog adoption
under this decision and stays subject to the keep/change/retire review in the
[evaluation protocol](../evaluations/README.md).

Context: The personal agentic-development program needs reusable procedures
and specialist roles across several coding hosts and software domains. Public
skill collections contain useful mechanisms, but they overlap an existing
catalog and often encode assumptions about issue trackers, commits, automatic
fan-out, tool permissions, or one host's lifecycle. Installing whole bundles
would create duplicate triggers, unclear ownership, upstream drift, and a
second distribution path. Writing separate personal copies for every host
would create the same divergence in a different place.

Decision: Keep the canonical procedure or role contract agent-neutral. Adopt
only a source mechanism that beats the existing baseline on a frozen local
evaluation. Classify the local use as an exact mirror, a derivative, or an
independently written implementation; retain the applicable license, copyright,
pinned upstream reference, source paths, and a summary of local changes. Put
shared skills and roles in one owned catalog with a single distribution route,
and keep host-specific model, effort, isolation, tool, and lifecycle settings
in tested projections. Project guidance and domain authorities remain closest
to the code. Upstream updates are reviewed and re-evaluated rather than applied
automatically.

Alternatives:

- Install complete upstream bundles. This is fast to try, but duplicates
  existing procedures and imports their triggers, side effects, and update
  policy.
- Maintain editable copies independently in each host. This is easy to start,
  but makes ownership, attribution, behavior parity, and removal difficult.
- Reimplement every procedure without consulting upstream work. This avoids
  derivative maintenance, but discards useful prior art and can obscure where
  a mechanism came from.
- Standardize on one host's native format as the canonical source. This reduces
  initial adapter work, but leaks that host's model names, tools, and lifecycle
  into every other surface.

Consequences: Intake is slower and the retained catalog should be smaller.
Each adopted item needs an overlap review, license decision, behavioral fixture,
owner, update route, and retirement condition. Host adapters and fresh-session
tests remain necessary; textual similarity alone does not establish behavior
parity. No automatic upstream update or new installer path is introduced. The
acceptance authorizes this architecture and the evaluation work, not the
promotion of any particular skill. Each generic contract still has to pass the
same frozen evaluation as its Codex projection without weakening permission or
side-effect boundaries before that contract becomes a default.
