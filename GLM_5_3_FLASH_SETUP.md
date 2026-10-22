# Claude Code with Z.AI GLM-5.3-Flash — Personal Windows Setup

Use a personal Z.AI GLM Coding Plan. Coding Plan keys and standard model API keys are different; create the key under **Personal Coding Plan → Plan Overview**.

## 1. Verify tools

Open a new PowerShell window after installing Node.js LTS and Claude Code:

```powershell
git --version
node --version
npm --version
npx.cmd --version
claude --version
claude doctor
```

If `npx` is blocked as a PowerShell script, use `npx.cmd`; do not weaken the execution policy merely for this command.

## 2. Configure the personal provider

Create/edit the global user file, never a repository file:

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude"
notepad "$env:USERPROFILE\.claude\settings.json"
```

Merge the following configuration, replacing only the placeholder with the personal Coding Plan key:

```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "REPLACE_WITH_PERSONAL_ZAI_CODING_PLAN_KEY",
    "ANTHROPIC_BASE_URL": "https://api.z.ai/api/anthropic",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "glm-5.3-flash[1m]",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "glm-5.3-flash[1m]",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "glm-5.3-flash[1m]",
    "CLAUDE_CODE_AUTO_COMPACT_WINDOW": "1000000",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": 1,
    "API_TIMEOUT_MS": "3000000"
  }
}
```

The real key must never enter Git, `.env`, project `.claude/`, prompts, screenshots or documentation.

## 3. Test outside the project

Close all terminals, open a new PowerShell window, then:

```powershell
New-Item -ItemType Directory -Force C:\Projects\claude-test
Set-Location C:\Projects\claude-test
claude
```

Accept the configured API key when prompted and trust only the test directory. Run `/status` and verify:

```text
Anthropic base URL: https://api.z.ai/api/anthropic
Credential: ANTHROPIC_AUTH_TOKEN
Effective mapping: GLM-5.3-Flash
```

Send a read-only test prompt, then `/exit`. If a Claude/Anthropic browser-login page appears instead, exit and fix the global settings before continuing.

## 4. Common failures

- `npx` not recognised: install Node.js LTS, restart VS Code/PowerShell and use `npx.cmd`.
- `401`: use the Personal Coding Plan key, remove copied spaces and confirm the key is active.
- `404`: the Claude Code base URL must be exactly `https://api.z.ai/api/anthropic`.
- Wrong model: confirm all three `ANTHROPIC_DEFAULT_*_MODEL` values are `glm-5.3-flash[1m]`, close every Claude session and restart.
- Settings ignored: validate JSON with `claude doctor`, close all terminals and reopen.

Official references are listed in `REFERENCE_LINKS.md`.
