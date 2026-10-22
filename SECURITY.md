# Security Design and Verification

## Threat boundary

The browser and all public visitors are untrusted. Hiding buttons or routes is not authorisation. Database and Storage policies are the enforcement layer.

## Mandatory controls

1. Enable RLS on every table exposed through Supabase APIs.
2. Revoke unnecessary grants before adding policies.
3. Anonymous users may select only published products, active categories, currently published/scheduled carousel slides and public content/settings.
4. Authenticated users receive no admin capability merely by being authenticated.
5. Admin write policies must also verify an active row in `admin_profiles`.
6. Super-admin-only operations must verify role.
7. Do not expose Auth user lists publicly.
8. Disable public registration/invitation UI.
9. Protect admin routes server-side and enforce RLS independently.
10. Never expose `service_role` in client code, logs or committed files.
11. Validate uploads by size and MIME type; use unique sanitised paths.
12. Rate-limit or otherwise protect authentication and expensive mutation endpoints where practical.
13. Use secure, HTTP-only session cookies through the supported SSR approach.
14. Avoid raw HTML from the admin editor; sanitise any rich text.
15. Add security headers: CSP where practical, HSTS on production, frame protection, referrer policy and content-type protection.
16. Only `super_admin` may list, invite, activate/deactivate or change roles for administrators.
17. Auth Admin API operations must run in a protected server-side or Edge Function and must re-check the caller's JWT and active super-admin role.
18. Prevent removal or demotion of the last active super admin.

## Storage policy

Recommended buckets:

- `product-images`: public read, active-admin insert/update/delete.
- `site-assets`: public read, active-admin insert/update/delete.

Object paths should include entity ID and unique filename. Deleting a database record must not silently orphan or remove a shared file.

## Required policy tests

Automate or document tests for:

| Actor | Action | Expected |
|---|---|---|
| Anonymous | Read published product | Allow |
| Anonymous | Read draft product | Deny/no rows |
| Anonymous | Insert/update/delete product | Deny |
| Anonymous | Upload/delete storage object | Deny |
| Authenticated non-admin | Read draft | Deny |
| Authenticated non-admin | Mutate product/category | Deny |
| Inactive admin | Mutate content | Deny |
| Active content admin | Product/category CRUD | Allow |
| Active admin | Storage CRUD | Allow |
| Content admin | Super-admin-only operation | Deny |
| Super admin | Approved privileged action | Allow |
| Content admin | Invite/change administrator | Deny |
| Super admin | Invite administrator through protected function | Allow |
| Last super admin | Deactivate/demote self | Deny |

## Manual security review before production

- Open `/admin` in an incognito browser: must redirect to login.
- Attempt direct Supabase anonymous writes: must fail.
- Log in with an authenticated user missing `admin_profiles`: must be denied.
- Deactivate an admin and verify the next protected request fails.
- Verify no secret appears in browser source, JavaScript bundles or network responses.
- Search Git history for accidental `.env` or key commits.
- Verify password reset returns only to allowed domains.
- Verify error messages do not reveal database details.
- Verify archived/draft product URLs do not reveal private content.

## Incident basics

If a key or password is exposed:

1. Rotate/revoke it immediately.
2. Remove it from active configuration.
3. Assess logs and access.
4. Remove it from Git history if committed.
5. Redeploy with replacement credentials.
6. Record the incident privately; do not add secrets to repository documentation.
