# Kiamora Repository Instructions

Read these files before changing code:

1. `SPEC.md`
2. `PLAN.md`
3. `STATUS.md`
4. `ADMIN_REQUIREMENTS.md`
5. `DATABASE_DESIGN.md`
6. `SECURITY.md`
7. `CONTENT_PENDING.md`
8. `UI_SPECS.md`

## Operating rules

1. Treat `SPEC.md` as the product source of truth.
2. Follow the milestones in `PLAN.md`; do not silently expand scope.
3. Update `STATUS.md` after every milestone with files changed, commands run, results, decisions and next action.
4. Missing customer content is non-blocking. Use clearly marked placeholders and update `CONTENT_PENDING.md`.
5. Never use company code, company accounts, company prompts, company skills or proprietary assets.
6. Keep all work inside this repository unless the user explicitly approves otherwise.
7. Do not expose or commit passwords, access tokens, service-role keys, recovery codes or customer personal data.
8. The Supabase service-role key must never appear in client-side code or a `PUBLIC_*` variable.
9. Enable RLS on every exposed table and test both allow and deny cases.
10. Public users may read only published products, active categories and public settings.
11. Only active Kiamora administrators may create, update, archive or delete data and storage objects.
12. There is no public registration page. Administrator onboarding is invite-only/manual.
13. Prefer archive/soft delete for business content. Confirm permanent deletion.
14. Every order is bespoke. Do not add cart, checkout, payment or `Buy Now` wording.
15. Keep the public storefront fast, accessible, mobile-first and SEO-friendly.
16. Treat all `mockups/storefront-*` screens as the minimum storefront quality and hierarchy baseline; implement original Kiamora design rather than copying a benchmark retailer.
17. Homepage carousel motion must respect reduced-motion, keyboard focus and page visibility, and must not compromise LCP or cause layout shift.
18. Keep forms typed and validated with readable errors.
19. Do not claim completion until checks, tests and production build pass.
20. Stop and ask before adding a paid dependency or service.

## Required stack

- Latest stable Angular 22.x patch at project creation
- Angular standalone components, strict TypeScript and Signals
- Angular hybrid rendering: SSR for public catalogue/product routes, CSR for protected admin interactions, and prerendering for suitable static pages
- Angular Material 3 and Angular CDK for accessible admin primitives; custom Kiamora styling for storefront
- Supabase PostgreSQL, Auth and Storage
- `@supabase/supabase-js` with an SSR-safe session approach
- Zod or equivalent typed validation
- Angular's current Vitest-based unit testing
- Playwright for critical browser journeys
- SCSS/CSS design tokens matching `UI_SPECS.md`

## Definition of done

- Public website and `/admin` work on mobile and desktop.
- Product/category/image CRUD works for an authorised administrator.
- Draft and archived products are not public.
- Anonymous writes and unauthorised storage uploads fail.
- WhatsApp messages contain the correct product reference and URL.
- Type checks, lint, unit tests, security-policy tests, browser smoke tests and production build pass.
- Deployment and administrator handover documentation is complete.
