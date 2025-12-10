# Configuration

The Second Brain skill stores its configuration at `~/.second-brain/config.json`.

## Setup

### Option 1: Environment Variable

Set the vault path via environment variable:

```bash
export SECOND_BRAIN_VAULT_PATH="/path/to/your/obsidian/vault"
```

Add to your shell profile (`~/.bashrc`, `~/.zshrc`, etc.) for persistence.

### Option 2: Config File

Create the config directory and file:

```bash
mkdir -p ~/.second-brain
cp config-template.json ~/.second-brain/config.json
```

Then edit `~/.second-brain/config.json` with your vault path.

### Option 3: Interactive Setup

Just ask Claude: "Set up my Second Brain" and it will guide you through creating the config.

## Configuration Options

```json
{
  "vaultPath": "/absolute/path/to/vault",
  "setupComplete": true,
  "userName": "Your Name",
  "userContext": "Permanent Notes/Assisting-User-Context.md",
  "preferences": {
    "defaultCaptureType": "inbox",
    "proactiveCapture": true,
    "inboxThreshold": 5
  }
}
```

### Fields

| Field | Description |
|-------|-------------|
| `vaultPath` | **Required.** Absolute path to your Obsidian vault |
| `setupComplete` | Whether initial setup has been completed |
| `userName` | Your name (used for personalization) |
| `userContext` | Path within vault to your context file |
| `preferences.defaultCaptureType` | Where to capture by default ("inbox") |
| `preferences.proactiveCapture` | Enable proactive capture suggestions |
| `preferences.inboxThreshold` | Items in inbox before prompting to process |

## Vault Requirements

Your Obsidian vault should have this structure (created during setup):

```
YourVault/
├── 00-Inbox/
│   ├── Daily/
│   └── Fleeting-Notes/
├── 01-Projects/
├── 02-Areas/
│   └── Relationships/
├── 03-Resources/
│   └── Reference-Notes/
├── 04-Archives/
├── Daily Plans/
├── Meeting Notes/
├── Permanent Notes/
└── Templates/
```

If these folders don't exist, the setup workflow will create them.
