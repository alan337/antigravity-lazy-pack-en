---
name: antigravity-github
description: Connect GitHub CLI in AntiGravity. Loads when you say "Connect GitHub" or "Setup GitHub".
---

# Connect GitHub (AntiGravity Version)

## Steps

### 1. Check
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
