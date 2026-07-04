# Anti-Gravity Lazy Pack

This repository only stores the publicly applicable lazy pack documents for Anti-Gravity users. It does not contain personal NotebookLM lists, research outputs, generated images, test projects, or any account data.

## Current Files

- `09-AntiGravity-Lazy-Pack.md`: The main lazy pack. Organizes the workflows for NotebookLM, Firebase, GitHub, and how to start/end work or initialize new projects. Obsidian is kept only as manual project notes, MCPVault is no longer installed.
- `.gitignore`: Ignores local configurations, NotebookLM exports, generated images, test apps, API keys, and temporary data.

## How to Use

### Method 1: Ask the AI to install it directly (Easiest)

Paste this prompt to your AI agent:

```
This is the Anti-Gravity Lazy Pack: https://github.com/alan337/antigravity-lazy-pack-en
Please read the repository contents, list all available lazy packs, and ask me which ones to install.
```

The AI will automatically read `SKILL.md` (the installation entry point), list the available skills, ask which ones you want to install, and then automatically install them.

### Method 2: Manually Open the MD Files

1. Open `09-AntiGravity-Lazy-Pack.md`
2. Hand the document contents over to Anti-Gravity or your AI coding assistant.
3. Sequentially complete environment checks, OAuth logins, NotebookLM / Firebase MCP configurations, and workflow setups.

## Security Principles

- NotebookLM login uses browser OAuth; do not copy cookies, tokens, or private export files.
- Do not commit `notebooks.json`, NotebookLM notebook ID lists, research reports, or generated images into public repositories.
- Do not hardcode API keys, GitHub tokens, or Firebase Admin credentials in Markdown files or push them to GitHub.
- When finishing work, check the diff first. Only commit the relevant files for that session. Avoid using indiscriminate `git add .`.
