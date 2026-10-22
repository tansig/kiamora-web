# Kiamora Website + Admin Portal — Start Here

This pack is the source of truth for building Kiamora on a clean personal Windows laptop with Claude Code CLI.

## Intended outcome

- Premium public bespoke-jewellery storefront.
- Secure `/admin` portal.
- Admin-managed products, categories, images, homepage content and business settings.
- Supabase PostgreSQL, Auth and Storage.
- Angular 22.x using standalone components and hybrid rendering.
- Cloudflare Workers deployment.
- WhatsApp as the primary customer-conversion channel.
- No company code, company configuration or company-owned AI skills.

## Do this in order

1. Complete every item marked **YOU** in `STEP_0_MANUAL_SETUP.md`.
2. Configure and verify personal GLM access using `GLM_5_3_FLASH_SETUP.md`.
3. Send `STEP_0_1_CUSTOMER_INFORMATION_REQUEST.md` to the business/customer.
4. Create and clone the empty GitHub repository.
5. Extract this pack into the repository root. `CLAUDE.md` must be at the root.
6. Copy `.env.example` to `.env` and fill only the public Supabase values after the project exists.
7. Commit the seed pack before Claude changes anything.
8. Open the repository in VS Code.
9. Run `claude` from the repository root and confirm `/status` still shows the personal Z.AI endpoint.
10. Paste `PROMPTS/00_FIRST_SESSION.md`.
11. Continue with the numbered prompts only after reviewing the prior phase.

## Important division of work

### YOU perform manually

- Create accounts and enable two-factor authentication.
- Configure the personal Z.AI Coding Plan credential outside the repository.
- Save recovery codes and passwords.
- Create the GitHub repository.
- Create the Supabase organisation/project and first admin identity.
- Authorise Cloudflare and connect the production domain when ready.
- Supply secrets through dashboards or local `.env` files.
- Approve database migrations and production deployments.
- Review product prices, legal wording and customer-visible content.

### CLAUDE performs in the repository

- Initialise and implement the Angular application.
- Create version-controlled Supabase migrations.
- Create and test RLS policies.
- Implement public pages and admin portal.
- Add validation, tests, documentation and deployment configuration.
- Maintain `STATUS.md` and `CONTENT_PENDING.md`.

## Recommended Claude workflow

Use Plan Mode for each large phase. Do not give Claude unrestricted permission to modify files outside this repository. Review diffs and create a Git commit after every successful milestone.

## First command sequence

```powershell
cd C:\Projects\kiamora-website
code .
claude
```

Then paste the contents of `PROMPTS/00_FIRST_SESSION.md`.

## Expected production URLs

```text
Public website: https://<final-domain>/
Admin portal:   https://<final-domain>/admin
Preview:        https://<cloudflare-project>.workers.dev
```

Do not publish the site until the security tests in `SECURITY.md` pass.
