# Prompt 04 — Administrative Portal

```text
Read CLAUDE.md, ADMIN_REQUIREMENTS.md, DATABASE_DESIGN.md, SECURITY.md, PLAN.md
and latest STATUS.md. Implement Milestone 4 only.

Build:
- dashboard;
- product CRUD, duplicate, preview, publish/unpublish, archive/restore;
- category CRUD and product assignments;
- product image upload, validation, alt text, primary selection, reordering and
  safe deletion;
- Yellow/White/Rose Gold variant tabs with multiple images per colour;
- homepage/page-content editor, including structured carousel slide CRUD,
  reorder, responsive media, focal points, alt text, CTA validation, scheduling,
  accessible behaviour configuration and desktop/mobile preview;
- business/settings editor;
- super-admin-only multiple-user management with invite, role, resend,
  activate/deactivate and last-super-admin protection;
- accessible validation, loading, success, error and unsaved-change states.

Match UI_SPECS.md and all admin mockups, including `admin-homepage-carousel.*`.
Do not treat hidden routes as security. Exercise the RLS and Storage-policy
tests through the implemented flows. Do not add public registration.

Run all Milestone 4 acceptance tests, fix failures, inspect the browser bundle
for secrets, update STATUS.md and stop. Report any manual Supabase steps I must
perform separately.
```
