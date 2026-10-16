# STEP 0 — Manual Accounts, Tools and Project Setup

Complete this before asking Claude to implement the application. Items labelled **YOU** require human action. Do not paste passwords, recovery codes or secret keys into Claude.

## 0.0 Ownership decision — YOU

Use personal/business-controlled accounts only. Do not reuse company accounts or devices.

Recommended ownership:

| Resource | Owner |
|---|---|
| GitHub repository | Personal Kiamora/Tarun GitHub account initially |
| Supabase organisation | Kiamora-controlled email |
| Cloudflare account | Kiamora-controlled email |
| Domain | Kiamora/business owner |
| WhatsApp Business | Kiamora/business owner |
| Claude subscription | Personal account |

Record account ownership in a private password manager, not in the repository.

## 0.1 Create the Kiamora email and security baseline — YOU

- [ ] Create or confirm a Kiamora-controlled email.
- [ ] Enable two-factor authentication.
- [ ] Store recovery codes in a password manager.
- [ ] Use unique passwords for GitHub, Supabase and Cloudflare.
- [ ] Add a recovery email/phone controlled by the business owner.

## 0.2 Install Windows development tools — YOU

Install:

- Visual Studio Code
- Git for Windows
- Node.js LTS
- Google Chrome or Microsoft Edge
- Claude Code CLI

Recommended VS Code extensions:

- Claude Code
- Angular Language Service
- ESLint
- Prettier
- EditorConfig
- GitHub Pull Requests and Issues

Install Claude Code from PowerShell:

```powershell
winget install Anthropic.ClaudeCode
```

Git for Windows is recommended because it provides Git Bash. The Claude Code CLI can also use PowerShell on native Windows.

Verify:

```powershell
git --version
node --version
npm --version
code --version
claude --version
```

Start Claude once and complete personal browser authentication:

```powershell
claude
```

- [ ] Confirm the logged-in Claude account is personal.
- [ ] Do not import company Claude configuration, sessions or skills.

## 0.3 Configure personal Git identity — YOU

```powershell
git config --global user.name "Tarun Mittal"
git config --global user.email "YOUR_PERSONAL_EMAIL"
git config --global init.defaultBranch main
git config --global --list
```

Replace the placeholder email before continuing.

## 0.4 Create GitHub account and repository — YOU

1. Sign in to or create a personal GitHub account.
2. Enable two-factor authentication.
3. Create a repository named `kiamora-website`.
4. Set visibility to **Private**.
5. Do **not** add a README, `.gitignore` or licence during creation; this pack supplies them.
6. Copy the HTTPS clone URL.

Clone it:

```powershell
New-Item -ItemType Directory -Force C:\Projects
Set-Location C:\Projects
git clone https://github.com/YOUR_ACCOUNT/kiamora-website.git
Set-Location kiamora-website
code .
```

Extract this pack's contents into `C:\Projects\kiamora-website`. `CLAUDE.md` and `SPEC.md` must be directly inside that folder.

Create the seed checkpoint:

```powershell
git add .
git commit -m "Add Kiamora Claude implementation pack"
git push -u origin main
```

## 0.5 Create Supabase organisation and project — YOU

1. Create/sign in to Supabase with the Kiamora-controlled email.
2. Enable two-factor authentication if offered.
3. Create an organisation such as `Kiamora`.
4. Create a project such as `kiamora-production`.
5. Select the nearest appropriate available region.
6. Generate a strong database password and save it in the password manager.
7. Wait for provisioning to finish.
8. Open Project Settings/API and record privately:
   - Project URL
   - Publishable/anonymous key
   - Project reference ID
9. Never copy the service-role key into frontend code, `.env`, an Angular environment file or chat.
10. Do not manually create tables yet; Claude will create version-controlled migrations.

Create `.env` locally from `.env.example`:

```powershell
Copy-Item .env.example .env
```

Populate only the public URL and publishable/anonymous key. Confirm `.env` is ignored by Git.

### Auth preparation — YOU

- [ ] Enable email/password authentication.
- [ ] Disable public self-registration if the dashboard exposes that option.
- [ ] Do not create a public registration page.
- [ ] Add `http://localhost:4200/auth/callback` as a local redirect URL when required.
- [ ] Add the Cloudflare preview and final domain callback URLs after deployment.
- [ ] Create the first Supabase Auth user for the initial Kiamora super admin only after migrations and policies exist.
- [ ] Ask Claude to provide the reviewed, one-time SQL statement that links that Auth user to an active `super_admin` profile; run it in the Supabase SQL Editor and retain no secret in the repository.

### Privileged admin-user function — YOU, after Claude implements it

The `/admin/users` screen needs a trusted Supabase Edge Function or equivalent protected server endpoint for invitations, role changes and account deactivation.

- [ ] Review the function implementation and its authorisation tests before deployment.
- [ ] Add `SUPABASE_SERVICE_ROLE_KEY` through Supabase Edge Function secrets (or the chosen server platform's encrypted secret store) only.
- [ ] Do not prefix this secret with `PUBLIC_` and do not add it to `.env.example` or the Angular build.
- [ ] Deploy the function, then verify a content admin receives `403` while an active super admin succeeds.
- [ ] Verify the last active super admin cannot be deactivated or demoted.
- [ ] Send an invitation to a test personal address before inviting production administrators.

## 0.6 Prepare Supabase CLI access — YOU

Claude may use `npx` so a permanent global install is unnecessary.

```powershell
npx supabase --version
npx supabase login
```

After Claude creates the local Supabase configuration:

```powershell
npx supabase link --project-ref YOUR_PROJECT_REF
```

Approve migration deployment only after reviewing the SQL diff.

## 0.7 Create Cloudflare account — YOU

1. Create/sign in with the Kiamora-controlled email.
2. Enable two-factor authentication.
3. Use the Free plan.
4. Do not create a paid Workers plan.
5. Authorise the CLI when prompted later:

```powershell
npx wrangler login
```

Claude will create the Workers configuration. You will approve the first preview deployment.

## 0.8 Domain — YOU, optional before MVP

- [ ] Confirm who owns the final domain.
- [ ] Do not transfer the domain until the preview is approved.
- [ ] Keep registrar recovery details under business control.
- [ ] Connect the domain only after preview QA passes.

The `*.workers.dev` URL is sufficient for the first preview.

## 0.9 WhatsApp Business and contact details — YOU

- [ ] Confirm the production WhatsApp Business number.
- [ ] Record it in international format without `+`, spaces or punctuation.
- [ ] Complete business name, logo, description, hours and email.
- [ ] Approve the website's default pre-filled enquiry message.

No paid WhatsApp API is required for the MVP.

## 0.10 Customer content — YOU

Send `STEP_0_1_CUSTOMER_INFORMATION_REQUEST.md` immediately. Development can proceed with placeholders.

## 0.11 STEP 0 completion gate

Do not begin implementation until:

- [ ] Personal GitHub repository exists and is cloned.
- [ ] Seed pack is committed and pushed.
- [ ] Supabase project exists.
- [ ] Cloudflare account exists.
- [ ] VS Code, Git, Node and Claude CLI work.
- [ ] Claude is authenticated with the personal account.
- [ ] `.env` exists locally and is not tracked.
- [ ] No company file, credential or configuration was copied.
