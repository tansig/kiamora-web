# Prompt 00 — First Claude Session

Paste everything below into Claude Code from the repository root.

```text
This is a new personal project on a clean personal Windows laptop. Do not assume
or search for any company code, company configuration, company Claude setup,
external private repositories, imported skills or prior implementation.

Read these files completely before acting:
- START_HERE.md
- CLAUDE.md
- SPEC.md
- PLAN.md
- STATUS.md
- ADMIN_REQUIREMENTS.md
- DATABASE_DESIGN.md
- SECURITY.md
- ENVIRONMENT_VARIABLES.md
- CONTENT_PENDING.md

Do not implement the application yet.

First:
1. Inspect only this repository and the locally installed tool versions.
2. Confirm that the seed documents are internally consistent.
3. Summarise the architecture, scope, security boundary and milestone gates.
4. Identify genuine blocking decisions only; missing customer content is not blocking.
5. Propose the exact package/dependency choices and explain any deviation from the specification.
   The required UI framework is the latest stable Angular 22.x patch; do not substitute React, Astro, Vue or another framework.
6. Produce a file-level implementation plan for Milestones 1 through 6.
7. Review DATABASE_DESIGN.md and SECURITY.md for gaps, especially RLS and Storage policies.
8. Update STATUS.md with the environment findings and proposed next action.
9. Review UI_SPECS.md and every file in mockups/; map each screen to Angular routes and components.

Do not create application code, install dependencies, change Supabase or deploy.
Stop after presenting the plan and list any approvals needed from me.
```
