# Prompt 02 — Database, Authentication and Security

```text
Read CLAUDE.md, DATABASE_DESIGN.md, SECURITY.md, PLAN.md and latest STATUS.md.
Implement Milestone 2 only.

Before applying anything remotely:
1. Create version-controlled Supabase migrations for schema, constraints,
   indexes, seed data, RLS and Storage policies.
2. Implement browser/server Supabase clients and secure session handling.
3. Implement invite-only login, logout, callback and protected admin routes.
4. Implement policy tests for anonymous, non-admin, inactive-admin,
   content-admin and super-admin cases.
5. Prove that public users can read only published/active content.
6. Prove anonymous and unauthorised writes/uploads fail.
7. Confirm that no service-role key is required in browser code.
8. Implement a protected server-side/Edge Function contract for super-admin invitations,
   role changes and deactivation. Never expose Auth Admin credentials to Angular.

Apply migrations locally or to an isolated local test environment first. Show me
the migration summary and security-test results before requesting approval to
link or push to the remote Supabase project.

Do not run a remote database push without my explicit approval. Update STATUS.md
and stop at the manual approval checkpoint.
```
