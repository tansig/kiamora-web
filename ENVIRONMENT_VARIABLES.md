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

If privileged server credentials become necessary, document why, keep them server-only, add them through the hosting dashboard and never expose them through client bundles. The MVP should avoid the service-role key during normal application runtime.

## Environments

Use separate values for:

- Local development
- Preview
- Production

Update Supabase Auth redirect allowlists for each legitimate URL. Do not use unrestricted wildcard production redirects.
