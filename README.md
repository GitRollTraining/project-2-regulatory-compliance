# Project 2: Regulatory Change Impact Brief

Interview the Compliance and Operations Owner, then build and run an Agent Skill that turns the provided regulatory, incident, calendar, and policy sources into normalized evidence and a human-reviewable compliance impact brief.

## Start

1. Fork this repository and work on your fork's `main` branch.
2. Interview the Gemini stakeholder in English. Explain which source you need and why; links are provided only when relevant.
3. Implement, run, and validate the skill.
4. Push the complete repository to `main` without changing or deleting `entire/checkpoints/v1`.

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
├── normalized/
│   ├── regulatory_updates.csv
│   ├── incidents.csv
│   └── license_calendar.csv
└── report.md
```

Follow the [Agent Skills specification](https://agentskills.io/specification). The `SKILL.md` frontmatter must include `name: regulatory-change-impact-brief` and a useful `description`. Document the runtime, inputs, exact command, outputs, validation, and safe-failure behavior. Validate with:

```bash
skills-ref validate ./regulatory-change-impact-brief
```

The implementation must recognize source roles from schemas rather than fixed filenames or column order, preserve source versions and dates, distinguish final rules from drafts or guidance, connect changes to incidents and deadlines, and surface conflicts or missing evidence for human review. It must not provide final legal advice, submit an official response, activate policy, close an incident, edit a source system, or invent missing facts.

Keep secrets and hidden assessment material out of the repository. Before pushing, run the documented command from a clean checkout and confirm that `report.md` agrees with all normalized CSV files.
