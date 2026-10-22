# Kiamora Implementation Plan

Claude must update `STATUS.md` after each milestone. A milestone is complete only after its validation gate passes.

## Milestone 0 — Manual readiness

Owner: User.

- Complete `STEP_0_MANUAL_SETUP.md`.
- Commit and push this seed pack.
- Create Supabase and Cloudflare accounts.
- Create local `.env` without committing it.

Gate: every item in Step 0.11 is checked.

## Milestone 1 — Application foundation

- Initialise the latest stable Angular 22.x application in the existing repository without deleting seed documents.
- Use standalone components, strict TypeScript, SCSS, routing, Signals and Angular hybrid rendering.
- Add Angular Material 3/CDK for admin primitives without applying a generic Material look to the storefront.
- Add lint, formatting, typecheck, unit-test and browser-test scripts.
- Create base layouts, routing, error handling and design tokens.
- Create a minimal public homepage and admin login shell.
- Configure environment validation.

Gate:

```powershell
npm install
npm run typecheck
npm run lint
npm run test
npm run build
```

## Milestone 2 — Supabase schema, RLS, Auth and Storage

- Initialise Supabase local structure.
- Add versioned migrations for all MVP tables and constraints.
- Add public and admin RLS policies.
- Add protected server-side administrator invitation and role-management functions with authorisation tests.
- Add storage buckets/policies through migrations where supported.
- Add safe seed data.
- Implement Supabase browser/server clients and session middleware.
- Implement login, logout, callback and protected admin route handling.
- Add policy tests for anonymous, non-admin, inactive-admin and active-admin actors.

Gate: migrations apply cleanly from zero; RLS allow/deny tests pass; service-role key is absent from browser code.

Manual checkpoint: user reviews SQL and applies it to the linked project, then creates/invites the first admin.

## Milestone 3 — Public storefront

- Header, navigation, footer and responsive shell.
- Professional editorial homepage driven by database content, including an accessible responsive carousel, category discovery, signature feature, featured products, assurance and consultation conversion.
- Collections/category pages.
- Catalogue search/filter.
- Product detail pages.
- Image gallery and related products.
- Customisation enquiry form and WhatsApp message.
- About, Bespoke, Guide, FAQ, Contact and policy pages.
- Sitemap, robots, metadata and structured data.

Gate: only published/active records are public; core journey passes at 390px, 768px and 1440px.

## Milestone 4 — Administrative portal

- Dashboard.
- Product CRUD and publication workflow.
- Category CRUD.
- Multiple category assignment.
- Image upload/reorder/primary/alt text/delete safeguards.
- Yellow/White/Rose Gold variants with independent multi-image galleries and storefront preview.
- Homepage/page content editor with carousel slide CRUD/reorder/schedule, responsive media, focal points, preview and atomic publishing.
- Business settings editor.
- Super-admin user-management page for multiple administrators.
- Preview and storefront shortcuts.
- Accessible validation, loading and error states.

Gate: every acceptance scenario in `ADMIN_REQUIREMENTS.md` and `SECURITY.md` passes.

## Milestone 5 — Content, polish and performance

- Apply Kiamora deep-green/ivory/gold identity.
- Use diamond-present approved emblem assets when supplied.
- Add optimised placeholders.
- Seed 8–12 draft products or supplied launch catalogue.
- Complete responsive, accessibility and performance corrections.
- Update content and admin guides.

Gate: no unapproved placeholder is accidentally public; images are optimised; Lighthouse/manual accessibility issues are addressed.

## Milestone 6 — Release, deployment and handover

- Configure Cloudflare Workers deployment.
- Add preview/prod environment variables through the platform.
- Apply reviewed Supabase migrations.
- Configure Auth redirect URLs.
- Deploy preview.
- Run production-like smoke and security tests.
- Connect custom domain only after approval.
- Complete `ADMIN_GUIDE.md` based on the implemented UI.

Final gate:

```powershell
npm run typecheck
npm run lint
npm run test
npm run test:e2e
npm run build
```

The final report must include URLs, commit SHA, migration version, validation results, open content items and rollback steps.
