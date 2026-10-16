# Master Prompt — Use Only After STEP 0

The numbered prompts are safer. Use this prompt only if you want Claude to work through all local phases continuously while still pausing before remote or destructive actions.

```text
This is a new personal project on a clean personal Windows laptop. No company
code, accounts, configuration, sessions, skills or proprietary assets may be
used.

Read every root Markdown file and all files under PROMPTS before acting. Treat
CLAUDE.md, SPEC.md, SECURITY.md, DATABASE_DESIGN.md and PLAN.md as binding.

Implement the Kiamora public storefront and secure administrative portal in the
milestone order in PLAN.md.

The UI must use the latest stable Angular 22.x patch and conform to UI_SPECS.md
and the supplied storefront/admin mockups. Do not substitute another framework.

Working rules:
- Maintain STATUS.md after every milestone.
- Missing customer assets are non-blocking and belong in CONTENT_PENDING.md.
- Run and repair all validation gates before advancing.
- Create a Git checkpoint after each successful milestone, but do not push
  without confirming the remote target.
- Use version-controlled Supabase migrations and test RLS deny cases.
- Never expose service-role credentials.
- Never enable public admin registration.
- Never deploy, push remote database migrations, change DNS, delete remote data,
  or create paid resources without my explicit approval.
- Stop on permission, credential, billing, destructive-migration or unresolved
  security blockers.

Begin with a plan and environment inspection. Then execute local milestones
autonomously. At every manual/remote checkpoint, show:
1. completed work;
2. validation results;
3. proposed exact command/action;
4. target environment;
5. risk and rollback;
6. approval needed from me.
```
