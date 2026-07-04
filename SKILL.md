---
name: antigravity-lazy-packs
description: Anti-Gravity Lazy Pack — Service connections and workflow configurations. Loads when the user says "Anti-Gravity Lazy Pack" or "Install Antigravity Setup".
---

# Anti-Gravity Lazy Pack — AI Agent Auto-Installation Entry

When the user provides the URL to this repo and asks to install it, please follow this process.

## Step 1: Recognize Available Lazy Packs

| Number | Skill Name | Description |
|--------|------------|-------------|
| 01 | `01-notebooklm` | Connect NotebookLM MCP |
| 02 | `02-github` | Connect GitHub CLI |
| 03 | `03-firebase` | Connect Firebase MCP |
| 04 | `04-draw` | Image Generation Guidelines |
| 05 | `05-workflow` | Start / End / New Project Initialization |
| 06 | `06-obsidian` | Connect Obsidian MCP (MCPVault) |
| 00 | `00-install-all`| Install everything at once |

## Step 2: Prompt the User for Selection

Show the table above to the user, then ask: "Which ones would you like to install? You can say 'all' or provide a combination of numbers (e.g., 01, 02, 03)."

## Step 3: Install Sequentially

For each selected skill:
```bash
npx skills add alan337/antigravity-lazy-pack-en --skill <skill_name> -g -y
```

If `npx skills add` is unavailable, install manually: Read the content of `skills/<name>/SKILL.md` and execute the instructions directly.

## Step 4: Report Results

Report the installation status for each item (✅/⚠️/❌), and provide a summary table at the end.
