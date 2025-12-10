# Second Brain Skill for Claude Desktop

A personal knowledge management and productivity skill combining GTD (Getting Things Done), Zettelkasten note-taking, and PARA organization for Obsidian vaults.

## Features

- **Quick Capture** - Instantly capture thoughts, tasks, and ideas with natural language
- **Daily Planning** - AI-powered daily planning based on your projects and energy
- **Inbox Processing** - GTD-style clarification and organization
- **Daily Closeout** - End-of-day review and tomorrow preparation
- **Proactive Capture** - Claude offers to save valuable insights during conversations

## Installation

### Step 1: Copy the Skill

Copy the `second-brain` folder to your Claude skills directory:

```bash
# Create the skills directory if it doesn't exist
mkdir -p ~/.claude/skills

# Copy the skill
cp -r second-brain ~/.claude/skills/
```

### Step 2: Configure Your Vault Path

Choose ONE of these options:

#### Option A: Environment Variable (Recommended)

Add to your shell profile (`~/.bashrc`, `~/.zshrc`, etc.):

```bash
export SECOND_BRAIN_VAULT_PATH="/path/to/your/obsidian/vault"
```

Then reload your shell:
```bash
source ~/.bashrc  # or ~/.zshrc
```

#### Option B: Config File

Create the config directory and file:

```bash
mkdir -p ~/.second-brain
```

Create `~/.second-brain/config.json`:

```json
{
  "vaultPath": "/path/to/your/obsidian/vault",
  "setupComplete": false,
  "userName": "",
  "userContext": "Permanent Notes/Assisting-User-Context.md",
  "preferences": {
    "defaultCaptureType": "inbox",
    "proactiveCapture": true,
    "inboxThreshold": 5
  }
}
```

#### Option C: Interactive Setup

Simply start using the skill and say "set up my second brain" - Claude will guide you through configuration.

### Step 3: Initial Setup

After installation, tell Claude:

> "Set up my Second Brain"

This will:
1. Validate your vault path
2. Create the required folder structure
3. Ask about your goals and preferences
4. Create your personal context file
5. Set up default areas (Career, Health, Personal Dev, Errands, Todos)
6. Create relationship notes for important people
7. Help you create your first project

## Usage

### Natural Language Commands

Just talk to Claude naturally. The skill responds to phrases like:

**Capture:**
- "Capture: need to call the dentist tomorrow"
- "Save this thought: idea for new project..."
- "Remember this: meeting notes from today..."

**Daily Planning:**
- "Plan my day"
- "What should I work on today?"
- "I need to figure out my priorities"

**Process Inbox:**
- "Process my inbox"
- "Organize my captures"
- "Help me clarify my tasks"

**Daily Closeout:**
- "Daily closeout"
- "Review my day"
- "Let's wrap up for today"

**Setup:**
- "Set up my Second Brain"
- "Configure my vault"
- "I want to update my goals"

### Proactive Capture

When you're discussing topics with Claude and something valuable comes up, Claude will offer:

> "That's an interesting insight about [topic]. Would you like me to capture this to your Second Brain?"

## Vault Structure

The skill creates/uses this structure:

```
YourVault/
├── 00-Inbox/
│   ├── Daily/              # Captures (YYYY-MM-DD.md)
│   └── Fleeting-Notes/     # Knowledge items
├── 01-Projects/            # Active projects
├── 02-Areas/               # Ongoing responsibilities
│   ├── Career-Development.md
│   ├── Health-Fitness.md
│   ├── Personal-Development.md
│   ├── Errands.md
│   ├── Personal-Todos.md
│   └── Relationships/      # People notes
├── 03-Resources/
│   └── Reference-Notes/
├── 04-Archives/            # Completed projects
├── Daily Plans/            # Generated plans
├── Meeting Notes/
├── Permanent Notes/        # Zettelkasten notes
│   └── Assisting-User-Context.md
└── Templates/
```

## Daily Workflow

1. **Throughout day:** "Capture: [anything on your mind]" (30 sec each)
2. **3x per week:** "Process my inbox" (15 min)
3. **Every morning:** "Plan my day" (5 min)
4. **Every evening:** "Daily closeout" (5 min)

**Total time:** ~20-25 min/day + 45 min/week = Sustainable!

## Skill Contents

```
second-brain/
├── SKILL.md                    # Main skill definition
├── config/
│   ├── config-template.json    # Config template
│   └── README.md               # Config documentation
├── workflows/
│   ├── setup.md                # Initial setup
│   ├── capture.md              # Quick capture
│   ├── process-inbox.md        # GTD processing
│   ├── daily-plan.md           # Daily planning
│   └── daily-closeout.md       # End of day review
├── references/
│   ├── gtd-methodology.md      # GTD reference
│   ├── para-zettelkasten.md    # Organization system
│   ├── obsidian-mastery.md     # Obsidian conventions
│   └── tagging-strategy.md     # Tag taxonomy
└── templates/
    ├── project.md
    ├── area.md
    ├── permanent-note.md
    ├── relationship.md
    └── user-context.md
```

## Troubleshooting

### Skill Not Activating

1. Verify the skill is in `~/.claude/skills/second-brain/`
2. Check that `SKILL.md` exists and has valid YAML frontmatter
3. Try being more explicit: "Use my Second Brain to capture..."

### Vault Path Issues

1. Check your config at `~/.second-brain/config.json`
2. Or verify environment variable: `echo $SECOND_BRAIN_VAULT_PATH`
3. Ensure the path is absolute (starts with `/`)

### Setup Not Working

1. Delete the config file: `rm ~/.second-brain/config.json`
2. Say "set up my second brain" to restart setup
3. Provide the full absolute path when asked

## Integration with Obsidian

This skill works with any Obsidian vault. For best results:

1. Install [Obsidian](https://obsidian.md)
2. Open your vault folder in Obsidian
3. Enable the following core plugins:
   - Backlinks
   - Tags
   - Search
4. Optional but recommended:
   - Dataview plugin (for advanced queries)
   - Tasks plugin (for task management)

## Updates

To update the skill, pull the latest version and copy again:

```bash
cp -r second-brain ~/.claude/skills/
```

Your configuration at `~/.second-brain/config.json` is preserved.

## Contributing

This skill is part of the [second-brain-gtd](https://github.com/sean-eskerium/second-brain-gtd) project.

## License

MIT
