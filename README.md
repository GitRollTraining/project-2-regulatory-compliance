# Project B: Regulatory Change Impact & Compliance Actions

Build and run an Agent Skill that helps a Compliance and Operations Manager compare current regulatory and internal evidence, identify supported impacts and unresolved questions, and prepare a draft action package for human review.

## Start

1. Fork this repository and work on your fork's `main` branch.
2. Use the interview link provided by your instructor to understand the manager's workflow, sources, ownership, and approval boundaries.
3. Implement one documented command that fetches the disclosed current sources, creates a snapshot, produces every required artifact, and validates the package.
4. Run the command, review the results, and push the complete repository to `main` without changing or deleting `entire/checkpoints/v1`.

Do not create a separate Session Log. The supported environment records the work automatically.

## Required submission

```text
regulatory-change-impact-brief/
├── SKILL.md
├── scripts/
│   └── <executable implementation>
└── references/
    └── <focused operating references>
deliverables/
├── snapshot.json
├── impact-register.csv
├── compliance-brief.md
└── action-calendar.ics
```

Minimum artifact contract:

- `snapshot.json` identifies the run, as-of time, scope, and status. Its evidence records identify each source, role or authority, locator, retrieval time and result, content type, available version metadata, and captured evidence or a resolvable local reference. Its decision state separates supported facts and impacts, unaffected items, conflicts, unresolved items, proposed actions, approval requirements, and your design decision with rationale.
- `impact-register.csv` has one row per impact or unresolved item with stable IDs, state, evidence references, reason, responsible owner, proposed action when applicable, and approval state.
- `compliance-brief.md` states scope, source status, supported impacts, unresolved items, actions, limitations, and pending Legal and Operations decisions.
- `action-calendar.ics` is a valid draft calendar whose events identify the proposed action, timing, owner or review role, and pending approval state.

Follow the [Agent Skills specification](https://agentskills.io/specification). The `SKILL.md` frontmatter must include `name: regulatory-change-impact-brief` and a useful `description`. Document prerequisites, runtime inputs, the exact command, output paths, validation, and material failure behavior. Validate the package with:

```bash
skills-ref validate ./regulatory-change-impact-brief
```

## Runtime evidence

Each invocation must read the current disclosed remote sources. Do not use bundled answers or a silent cached copy as the primary source.

`deliverables/snapshot.json` is part of the submitted result. Record the run context, every attempted source and retrieval result, the evidence actually used, supported facts and impacts, conflicts, unresolved items, proposed actions, approval requirements, and your material design decisions and rationale. Preserve enough source identity, timing, version or locator information, and captured evidence for another reviewer to trace the package without asking the assessment system to fetch the source again.

You do not need to reconstruct an earlier version of an external website. If authoritative regulatory evidence is unavailable, block formal impact conclusions and produce an explicitly failed or unresolved draft instead.

## Safety boundary

The workflow is read-only. It may prepare local drafts, but it must not expose credentials, alter a source, submit an official response, give final legal advice, activate policy, change an approved deadline, close an incident, or write to a production calendar. Legal and Operations retain their stated decisions.

Before pushing, run the documented command from a clean checkout and confirm that the snapshot, register, brief, and draft calendar agree.
