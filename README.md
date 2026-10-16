# Kiamora Website and Administrative Portal

This repository will contain Kiamora's public bespoke-jewellery storefront and secure administrative portal.

## Architecture

```text
Browser
  -> Cloudflare Workers / Astro SSR
       -> Supabase Auth
       -> Supabase PostgreSQL
       -> Supabase Storage
       -> WhatsApp click-to-chat
```

## Documentation map

- `START_HERE.md` — exact execution order.
- `STEP_0_MANUAL_SETUP.md` — accounts, tools and manual configuration.
- `STEP_0_1_CUSTOMER_INFORMATION_REQUEST.md` — customer asset request.
- `CLAUDE.md` — standing Claude Code instructions.
- `SPEC.md` — functional and technical scope.
- `PLAN.md` — implementation milestones and gates.
- `ADMIN_REQUIREMENTS.md` — portal screens and behaviour.
- `DATABASE_DESIGN.md` — schema and data rules.
- `SECURITY.md` — authentication, RLS, storage and security tests.
- `ENVIRONMENT_VARIABLES.md` — local and deployment configuration.
- `DEPLOYMENT_GUIDE.md` — Cloudflare and Supabase release process.
- `CONTENT_PENDING.md` — missing business content.
- `PROJECT_VALUES.md` — commit-safe project identifiers and public values.
- `REFERENCE_LINKS.md` — official product documentation.
- `STATUS.md` — living implementation status.
- `PROMPTS/` — ready-to-paste Claude prompts.

## Local commands after implementation

```powershell
npm install
npm run dev
npm run typecheck
npm run lint
npm run test
npm run test:e2e
npm run build
npm run preview
```

Claude must create and document any missing scripts during Milestone 1.

## Source of truth

If instructions conflict, use this order:

1. Latest explicit user instruction
2. `SPEC.md`
3. `SECURITY.md`
4. `DATABASE_DESIGN.md`
5. `PLAN.md`
6. Other documentation
