# Deployment Guide

Claude must update this document with the exact implemented commands and project names.

## Preview release

1. Ensure the branch is clean and pushed.
2. Run the full validation suite.
3. Review Supabase migration diff.
4. Apply migrations to the linked project.
5. Set Cloudflare environment variables through the dashboard/CLI; never commit them.
6. Deploy to a `*.workers.dev` preview URL.
7. Add the preview Auth callback URL in Supabase.
8. Run public, admin and security smoke tests.

Expected commands after implementation:

```powershell
npx supabase link --project-ref YOUR_PROJECT_REF
npx supabase db push
npm run build
npx wrangler deploy
```

Do not run `db push` or production deployment without reviewing the pending changes.

## Production release

- Confirm business content and legal approval.
- Confirm the first admin can log in and another unauthorised account cannot.
- Confirm backups/export procedure.
- Connect the custom domain in Cloudflare.
- Add exact production callback/redirect URLs in Supabase Auth.
- Set `PUBLIC_SITE_URL` to the production URL.
- Redeploy and run the full smoke checklist.
- Add Google Search Console after DNS is live.

## Rollback

- Application: redeploy the prior known-good Git commit/Worker version.
- Database: prefer forward corrective migrations; do not casually reverse destructive migrations.
- Content: restore archived data or use audited prior values where available.
- Keys: rotate compromised credentials rather than merely reverting code.

## Release record

For every release record:

- Git commit SHA
- Migration version
- Deployment URL/version
- Test results
- Known limitations
- Rollback reference
