# Anti-Gravity Lazy Pack #09: Service Connection & Workflow Setup

> Version: v1.4 (English translated for actual environment)
> Update Date: 2026-07-04
> Language Preference: English

The goal of this lazy pack is to allow Anti-Gravity users to securely connect NotebookLM, Firebase, GitHub, and Obsidian, and establish a "Start Work / End Work / New Project Initialization" workflow.

This document only includes setup processes that can be publicly shared. It does NOT include any personal NotebookLM lists, notebook IDs, research reports, generated images, account tokens, or test projects.

---

## Prerequisites

- [ ] Anti-Gravity or an MCP-capable AI coding assistant installed
- [ ] Git installed (User scope: `~\AppData\Local\Programs\Git\cmd`)
- [ ] GitHub CLI (`gh`) installed (User scope via winget)
- [ ] Node.js / npm installed (User scope via winget)
- [ ] Python or `uv` installed
- [ ] Google account for NotebookLM / Firebase
- [ ] GitHub account
- [ ] Obsidian vault available, or know the notebook folder location

Windows Quick Check:

```powershell
git --version
gh --version
node --version
npm.cmd --version
python --version
```

---

## 1. Connect NotebookLM

### Core Principles

NotebookLM login must use browser OAuth authorization. Do not copy cookies or tokens, and do not put NotebookLM exported `notebooks.json` or notebook ID lists into public repos.

### Install NotebookLM MCP CLI

Use `uv` (recommended) to install:

```powershell
uv tool install notebooklm-mcp-cli
nlm --version
```

If `uv` is unavailable, use pip:

```powershell
pip install notebooklm-mcp-cli
nlm --version
```

### Re-login to Google Account

If logged into the wrong account, logout and re-OAuth:

```powershell
nlm logout
nlm login
```

`nlm login` will open a browser. Please select the correct Google account to authorize.

Verify:

```powershell
nlm doctor
nlm list notebooks
```

If Windows displays CP950 / Unicode encoding errors, run this in the same PowerShell window first:

```powershell
$env:PYTHONIOENCODING = "utf-8"
nlm doctor
```

### Register MCP

Please refer to the actual product documentation or UI for Anti-Gravity's MCP configuration file location. 

General configuration concept:

```json
{
  "mcp": {
    "notebooklm": {
      "type": "local",
      "command": ["nlm", "mcp"],
      "enabled": true
    }
  }
}
```

After completing, restart Anti-Gravity and ask it to list NotebookLM notebooks. Only report whether it was successful; do not commit the full list to the repo.

---

## 2. Connect GitHub

### Login to GitHub CLI

```powershell
gh auth status
gh auth login --web --git-protocol https
gh auth status
```

If the login process gets stuck, please complete the browser authorization in an interactive PowerShell window, then come back to verify.

### Set Git User

```powershell
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

If you don't want to expose your personal email, you can use a GitHub no-reply email.

### Security Rules

- GitHub and GitHub Copilot are different services; this workflow only requires a GitHub account, Git, and GitHub CLI.
- Do not write GitHub tokens into Markdown, AGENTS, ANTIGRAVITY, public Obsidian notes, or repos.
- Check the diff before committing. Do not blindly commit everything.

---

## 3. Connect Firebase

### Installation and Login

On Windows, it is recommended to use `npx.cmd` to avoid PowerShell execution policy restrictions blocking `.ps1`:

```powershell
npx.cmd -y firebase-tools@latest --version
npx.cmd -y firebase-tools@latest login
npx.cmd -y firebase-tools@latest projects:list
```

`firebase login` requires an interactive browser login. If the AI conversation gets stuck, manually open PowerShell to log in, then return to let the AI verify.

### Register Firebase MCP

Anti-Gravity's MCP configuration file location depends on the actual product. Configuration concept:

```json
{
  "mcp": {
    "firebase": {
      "type": "local",
      "command": ["npx.cmd", "-y", "firebase-tools@latest", "mcp"],
      "enabled": true
    }
  }
}
```

After completing, restart Anti-Gravity and test by listing Firebase projects and Firestore collections.

### Security Rules

- Firebase frontend configs can be public, but Admin SDK credentials CANNOT.
- If `.firebaserc` contains private project IDs, confirm if it's suitable before making it public.
- Student data should only store class codes and seat numbers, not real names.

---

## 4. Connect Obsidian

### Find the Vault

Confirm the physical path of your Obsidian vault. Common locations:

```text
C:\Users\<You>\OneDrive\Documents\Secondbrain
C:\Users\<You>\Documents\<vault name>
G:\My Drive\<vault name>
```

Confirmation conditions:
- The folder exists
- It contains an `.obsidian` folder
- It is the vault you actually use regularly

### Install MCPVault

```powershell
npm.cmd install -g @bitbonsai/mcpvault
where.exe mcpvault
```

Common path:
```text
C:\Users\<You>\AppData\Roaming\npm\mcpvault.cmd
```

### Register Obsidian MCP

Do not treat OpenCode's `opencode.json` as Anti-Gravity's fixed format. Please add it according to Anti-Gravity's actual MCP setup:

```json
{
  "mcp": {
    "obsidian": {
      "type": "local",
      "command": [
        "C:\\Users\\<You>\\AppData\\Roaming\\npm\\mcpvault.cmd",
        "C:\\Users\\<You>\\OneDrive\\Documents\\Secondbrain"
      ],
      "enabled": true
    }
  }
}
```

If Anti-Gravity uses a separated command/args format:

```json
{
  "command": "C:\\Users\\<You>\\AppData\\Roaming\\npm\\mcpvault.cmd",
  "args": ["C:\\Users\\<You>\\OneDrive\\Documents\\Secondbrain"]
}
```

After completing, restart Anti-Gravity. Test reading the vault root directory, create a test note, and read it back to confirm.

---

## 5. Generate Images

If Anti-Gravity has a built-in image generation tool, you can generate images directly using natural language without putting OpenAI API keys into the repo.

Suggested prompt format:

```text
Generate an image:
Purpose:
Aspect Ratio:
Subject:
Content:
Style:
Color:
Text:
Constraints:
Output Location:
```

Notes:
- It is recommended to post-process important text; image generation models might misspell words.
- Images referenced by the project should be placed in the project's `assets/` or Obsidian's attachments folder.
- Do not commit temporary generated images to the lazy pack repo.

---

## 6. Start / End Work / New Project Initialization

Anti-Gravity can use `ANTIGRAVITY.md` in the project root directory as the AI workflow rules entry. It should record fixed rules, paths, project boundaries, and Do's / Don'ts. Progress, pitfalls, and daily logs should be kept in the Obsidian project cockpit.

### Start Work

When the user says "Start Work", the AI should:

1. Read `ANTIGRAVITY.md` or the equivalent rules file in the project root.
2. Read the Obsidian project cockpit.
3. Run `git status` and check recent commits.
4. Report current status and suggest next steps.
5. Do not automatically pull, commit, or push.

### End Work

When the user says "End Work", the AI should:

1. Check for sensitive data: API keys, tokens, credentials, NotebookLM export lists, real names.
2. Update the Obsidian project cockpit: completed items, next steps, pitfalls.
3. Only update `ANTIGRAVITY.md` if fixed rules or paths change.
4. Run `git status` and check diffs.
5. Only stage relevant files for this session, avoiding indiscriminate `git add .`.
6. Generate a commit message, confirm, and commit/push.
7. Report the sync results for Obsidian, the rules file, and GitHub.

### New Project Initialization

When the user says "New Project Initialization", the AI should clarify:

- Project Name
- Purpose
- Working Directory
- Create GitHub repo?
- Repo public or private?
- Require GitHub Pages / Firebase / other deployments?
- Obsidian vault and project cockpit location

Then create or populate:
- `ANTIGRAVITY.md`
- `README.md`
- `.gitignore`
- Git repo
- GitHub repo (if requested)
- Obsidian project cockpit

If the folder is an existing project, first inventory the "exists / missing" list, only fill in gaps, and do not overwrite existing setups.

---

## Suggested ANTIGRAVITY.md Template

```markdown
# <Project Name> - ANTIGRAVITY.md

## Project Entry

Project Name:
Purpose:
Main Working Directory:
GitHub repo:
Default branch:

## Obsidian Corresponding Notes

Obsidian vault:
Project cockpit:

## Work Rules

- Respond in English.
- Report full output paths when handling files.
- Use PowerShell syntax.
- On "Start Work", read this file, read the Obsidian cockpit, and check Git status.
- On "End Work", update Obsidian, update this file if necessary, check diffs, and only commit relevant files.
- Do not write daily logs into this file.

## Do Not

- Do not commit API keys, tokens, passwords, Firebase Admin credentials.
- Do not commit NotebookLM personal export lists or notebook ID lists.
- Do not automatically include irrelevant git changes.
- Do not store student real names; use class codes and seat numbers for formal data.
```

---

## Completion Report Format

```markdown
## Anti-Gravity Lazy Pack Setup Complete

- NotebookLM: Logged in / Pending OAuth / Failed
- GitHub: Logged in / Pending Login / Failed
- Firebase: Logged in / Pending Login / Not Used
- Obsidian: Connected / Pending Setup / Failed
- Rule File: ANTIGRAVITY.md Created / Updated / Not Created
- Git Status: Clean / Uncommitted Changes
- Next Steps:
```

---

## Common Issues

| Issue | Solution |
|---|---|
| NotebookLM logged into wrong account | `nlm logout` then `nlm login`, select correct account in browser |
| `nlm doctor` shows unauthenticated | Rerun OAuth login, do not manually paste cookies |
| Windows encoding error | Run `$env:PYTHONIOENCODING = "utf-8"` and retry |
| GitHub CLI not logged in | `gh auth login --web --git-protocol https` |
| Firebase login stuck | Run `npx.cmd -y firebase-tools@latest login` manually in interactive PowerShell |
| PowerShell blocks `npm.ps1` / `npx.ps1` | Switch to `npm.cmd` / `npx.cmd` |
| Obsidian can't find vault | Search for folders containing `.obsidian`, ask user to confirm the actual vault used |
| End Work includes too many files | Check `git status` and diff first, only stage relevant files |
