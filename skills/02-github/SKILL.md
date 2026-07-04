---
name: antigravity-github
description: Connect GitHub CLI in AntiGravity. Loads when you say "Connect GitHub" or "Setup GitHub".
---

# Connect GitHub (AntiGravity Version)

## Steps

### 1. Installation

**🤖 AI AGENT INSTRUCTIONS: TWO SCENARIOS**
Before installing anything, evaluate if the user is running in Admin Mode (default) or User Level Only (no admin account).
- **Admin Mode**: You can use standard global installers.
- **User Level Only**: If the user prompts to install at the user level only, you MUST NOT trigger UAC prompts. First, search the system to see if Git or GitHub CLI are already installed in user paths (e.g., `~\AppData\Local\Programs\Git\cmd`, `AppData\Local\Microsoft\WinGet\Packages`). If missing, you must install them strictly at the user level:
  - **Git**: Download and extract MinGit to the user profile (e.g., `~\AppData\Local\Programs\Git`).
  - **GitHub CLI**: Use `winget install --id GitHub.cli --scope user`.

### 2. Check
```bash
gh auth status
```

### 2. Login
```bash
gh auth login --web --git-protocol https
```

### 3. Set Git User
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

### 4. Security Rules
- Do not write GitHub tokens into Markdown, AGENTS, or repos.
- Check diff before committing; avoid indiscriminate `git add .`.
