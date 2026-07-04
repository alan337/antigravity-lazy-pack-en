---
name: antigravity-obsidian
description: Connect Obsidian MCP (MCPVault) in AntiGravity. Loads when you say "Connect Obsidian" or "Setup Obsidian".
---

# Connect Obsidian (AntiGravity Version)

## Steps

### 1. Find the vault
Confirm the physical path of your Obsidian vault. Common locations:
- `C:\Users\<You>\OneDrive\Documents\Secondbrain`
- `C:\Users\<You>\Documents\<vault name>`
- `G:\My Drive\<vault name>`

### 2. Install MCPVault
Execute installation in Command Prompt or PowerShell:
```powershell
npm.cmd install -g @bitbonsai/mcpvault
where.exe mcpvault
```
Common path is:
`C:\Users\<You>\AppData\Roaming\npm\mcpvault.cmd`

### 3. Register Obsidian MCP
Add to the configuration file based on AntiGravity's actual MCP setup format:
```json
"obsidian": {
  "type": "local",
  "command": [
    "C:\\Users\\<You>\\AppData\\Roaming\\npm\\mcpvault.cmd",
    "C:\\Users\\<You>\\OneDrive\\Documents\\Secondbrain"
  ],
  "enabled": true
}
```

If using a separated command / args format:
```json
{
  "command": "C:\\Users\\<You>\\AppData\\Roaming\\npm\\mcpvault.cmd",
  "args": ["C:\\Users\\<You>\\OneDrive\\Documents\\Secondbrain"]
}
```

### 4. Verify
Restart AntiGravity. Test reading the vault root directory, create a test note, and read it back.

⚠️ Security Reminder: Do not commit your physical vault path or any sensitive note content into public repositories.
