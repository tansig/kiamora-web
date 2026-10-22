# Environment Variables

## Local file

Create `.env` from `.env.example`. Never commit `.env`.

## Variables

```text
PUBLIC_SUPABASE_URL
PUBLIC_SUPABASE_ANON_KEY
PUBLIC_SITE_URL
PUBLIC_WHATSAPP_NUMBER
```

The Supabase URL and publishable/anonymous key are designed for browser use only when RLS is correctly configured. They are not substitutes for RLS.

## Forbidden client variables

Never create:

```text
PUBLIC_SUPABASE_SERVICE_ROLE_KEY
PUBLIC_DATABASE_PASSWORD
PUBLIC_GITHUB_TOKEN
```

Administrator invitation and Supabase Auth Admin operations require a privileged credential. Configure `SUPABASE_SERVICE_ROLE_KEY` only as an encrypted secret of the protected Supabase Edge Function or server runtime that performs those operations. It must never be placed in `.env.example`, an Angular environment file, a `PUBLIC_*` variable, a browser bundle, logs or screenshots.

The Angular application sends the signed-in administrator's access token to that protected endpoint. The endpoint must validate the token, confirm an active `super_admin` role and enforce the last-super-admin rule before using the Auth Admin API. Ordinary catalogue and admin data operations continue to use the browser-safe publishable/anonymous key with RLS.

## Environments

Use separate values for:

- Local development
- Preview
- Production

Update Supabase Auth redirect allowlists for each legitimate URL. Do not use unrestricted wildcard production redirects.
