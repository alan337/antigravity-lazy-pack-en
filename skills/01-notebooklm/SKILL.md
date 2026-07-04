---
name: antigravity-notebooklm
description: Connect NotebookLM MCP in AntiGravity. Loads when you say "Connect NotebookLM" or "Setup NotebookLM".
---

# Connect NotebookLM (AntiGravity Version)

This skill provides instructions for the AI assistant and the user to securely connect the NotebookLM MCP (Model Context Protocol).

## Prerequisites
- Python installed (preferably with `uv` package manager).
- Google account with NotebookLM access.

## Installation
Use `uv` (recommended) or `pip` to install the NotebookLM MCP CLI tool:

```powershell
uv tool install notebooklm-mcp-cli
# Or if uv is not available:
pip install notebooklm-mcp-cli
```

Verify installation:
```powershell
nlm --version
```

## Authentication
NotebookLM uses browser-based OAuth. Do not copy or store raw cookies, tokens, or private export files in public repositories.

To authenticate:
```powershell
nlm logout
nlm login
```
*Note: `nlm login` will open a browser window. The user must manually complete the Google OAuth flow in the browser.*

### Verification
Verify that the login was successful and the account is linked. First, set the encoding to prevent Windows parsing errors:
```powershell
$env:PYTHONIOENCODING = "utf-8"
nlm doctor
nlm list notebooks
```

## MCP Server Registration
To register this tool with the AI assistant's MCP configuration, use the following JSON structure (adjust paths depending on the exact AI assistant you are using):

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

After configuring, restart the AI assistant and ask it to list your NotebookLM notebooks to confirm it works. Do not commit the complete notebook list to your repository.
