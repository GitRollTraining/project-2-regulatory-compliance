# Project B: Regulatory Change Impact & Compliance Actions

Build and run an Agent Skill that helps a Compliance and Operations Manager compare current regulatory and internal evidence, identify supported impacts and unresolved questions, and prepare a draft action package for human review.

## Start

1. Fork this repository and work on your fork's `main` branch.
2. Open the [Project B stakeholder interview](https://work-sim-alpha.catalyte.ai/s/project-b-regulatory-compliance) to understand the manager's workflow, sources, ownership, and approval boundaries.
3. Implement one documented command that fetches the disclosed current sources, writes each required workflow snapshot when that stage completes, produces every final artifact, and validates the package.
4. Run the command, review the results, and push the complete repository to `main` without changing or deleting `entire/checkpoints/v1`.

Do not create a separate Session Log. The supported environment records the work automatically.

## Required submission

```text
snapshot.schema.json  # provided contract; keep unchanged
regulatory-change-impact-brief/
├── SKILL.md
├── scripts/
│   └── <executable implementation>
└── references/
    └── <focused operating references>
deliverables/
├── snapshots/
│   ├── 01-scope.json
│   ├── 02-source-capture.json
│   ├── 03-authority-and-timing.json
│   ├── 04-evidence-reconciliation.json
│   ├── 05-impact-analysis.json
│   ├── 06-actions-and-approvals.json
│   └── 07-publication-validation.json
├── impact-register.csv
├── compliance-brief.md
└── action-calendar.ics
```

## Required snapshot chain

Every stage file must conform to [`snapshot.schema.json`](snapshot.schema.json). All seven use one `run_id`. From stage 2 onward, `predecessor` identifies and hashes the immediately preceding file. Each stage names the upstream record IDs it consumed and the record IDs it produced.

| Stage | Required state |
|---|---|
| 01 | as-of time, review type, systems, audiences, approval gates |
| 02 | every source attempt and retrieval result |
| 03 | binding rules, timing, labelled guidance, authority blockers |
| 04 | system facts, policy controls, incidents, conflicts, evidence gaps |
| 05 | impacts, unaffected records, conflicts, unresolved items |
| 06 | actions, escalations, owners, approvals, learner decisions |
| 07 | final artifact paths and hashes, validation and publication status |

Run status is `complete`, `partial`, `blocked`, or `failed`. Retrieval status is `retrieved`, `unavailable`, `invalid`, `unverified`, or `stale`. Impact state is `supported-impact`, `supported-no-impact`, `conflicting`, or `unresolved`. Do not invent records to demonstrate a state, and do not let a missing or conflicting record disappear downstream without a traceable reason.

## Decision behavior

The seven files are an ordered audit trail, but the business workflow is not always a happy path:

- unavailable binding evidence blocks formal impact conclusions and remains visible downstream;
- for another unavailable required source, choose and document either a whole-run block or a safely bounded partial result, then apply that policy consistently;
- insufficient or conflicting applicability evidence stays unresolved with an owner and required next evidence;
- a correctable validation failure returns to the earliest affected stage and reruns downstream work;
- Legal interpretation and Operations activation, dates, and closure remain pending human decisions.

## Final artifacts

- `impact-register.csv` has one row per impact or unresolved item with stable IDs, state, evidence references, reason, responsible owner, proposed action when applicable, and approval state.
- `compliance-brief.md` states scope, source status, supported impacts, unresolved items, actions, limitations, and pending Legal and Operations decisions.
- `action-calendar.ics` is a valid draft calendar whose events identify the proposed action, timing, owner or review role, and pending approval state.

Follow the [Agent Skills specification](https://agentskills.io/specification). The `SKILL.md` frontmatter must include `name: regulatory-change-impact-brief` and a useful `description`. Document prerequisites, runtime inputs, the exact command, output paths, validation, and material failure behavior. Validate the package with:

```bash
skills-ref validate ./regulatory-change-impact-brief
```

## Runtime evidence

Each invocation must read the current disclosed remote sources. Do not use bundled answers or a silent cached copy as the primary source.

The seven snapshots are part of the submitted result. Write them during the workflow, not retrospectively after the final report. Preserve enough source identity, timing, version or locator information, predecessor hashes, and stable record IDs for another reviewer to follow the complete document-to-decision path without refetching the source.

You do not need to reconstruct an earlier version of an external website. If authoritative regulatory evidence is unavailable, block formal impact conclusions and produce an explicitly failed or unresolved draft instead.

## Safety boundary

The workflow is read-only. It may prepare local drafts, but it must not expose credentials, alter a source, submit an official response, give final legal advice, activate policy, change an approved deadline, close an incident, or write to a production calendar. Legal and Operations retain their stated decisions.

Before pushing, run the documented command from a clean checkout and confirm that every snapshot passes the schema, the lineage is intact, and the register, brief, and draft calendar agree with stages 06–07.
