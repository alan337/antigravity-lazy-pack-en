---
name: antigravity-github
description: Connect GitHub CLI in AntiGravity. Loads when you say "Connect GitHub" or "Setup GitHub".
---

# Connect GitHub (AntiGravity Version)

## Steps

### 1. Installation (User Level Only)
If Git or GitHub CLI are not installed, you must install them at the user level to avoid administrator (UAC) prompts.
- **Git**: Download and extract MinGit to your user profile (e.g., `~\AppData\Local\Programs\Git`).
- **GitHub CLI**: `winget install --id GitHub.cli --scope user`

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
