---
name: antigravity-firebase
description: Connect Firebase MCP in AntiGravity. Loads when you say "Connect Firebase" or "Setup Firebase".
---

# Connect Firebase (AntiGravity Version)

This skill provides instructions for the AI assistant and the user to securely connect the Firebase CLI and its MCP server.

## Prerequisites
- Node.js and npm/npx installed.
- Google account with Firebase projects.

## Installation & Authentication
On Windows, it is highly recommended to use `npx.cmd` to bypass PowerShell execution policy restrictions.

Check the CLI version:
```powershell
npx.cmd -y firebase-tools@latest --version
```

Login to Firebase:
```powershell
npx.cmd -y firebase-tools@latest login
```
*Note: `firebase login` requires an interactive browser session. If the AI assistant gets stuck trying to run this, the user must open a fresh PowerShell terminal manually, run the command, complete the browser login, and then return to the AI assistant to verify.*

### Verification
Once logged in, verify the connection by listing the projects:
```powershell
npx.cmd -y firebase-tools@latest projects:list
```

## MCP Server Registration
To register the Firebase MCP server with your AI assistant, use the following configuration structure:

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

After configuration, restart the AI assistant and test it by asking to list your Firebase projects or Firestore collections.

## Security Principles
- The frontend Firebase configuration (like `apiKey`, `projectId`) is safe to be public, but **Firebase Admin SDK credentials** must NEVER be committed to a repository.
- If your `.firebaserc` file contains private project IDs, ensure you do not push it to a public GitHub repository.
- Do not commit sensitive data or test database files automatically. Always use targeted Git commits.
