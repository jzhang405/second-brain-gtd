# Second Brain Skill

A personal knowledge management and productivity system powered by GTD, Zettelkasten, and Obsidian - designed as a skill for Claude Desktop (and compatible with Claude Code).

**Version:** 4.1
**Last Updated:** 2025-12-11
**Compatible With:** Claude Desktop, Claude Code

---

## Why Second Brain?

**The problem:** Your brain is great at having ideas, but terrible at storing them. Important thoughts slip away. Tasks get forgotten. Notes end up scattered across apps, files, and sticky notes. You spend more time searching for information than actually using it.

**The solution:** A Second Brain - a single, organized system where everything lives together and nothing falls through the cracks.

### What This Skill Gives You

**An AI assistant that knows your system.** Claude becomes your personal productivity partner. It captures your thoughts, organizes your tasks, plans your day, and keeps everything in sync - all through natural conversation. No learning complex apps or remembering special commands.

**The GTD methodology, without the overhead.** Getting Things Done (GTD) is one of the most effective productivity systems ever created, but implementing it yourself takes discipline. This skill handles the methodology for you:
- **Capture** everything that has your attention (tasks, ideas, notes)
- **Clarify** what each item means and what action is needed
- **Organize** into projects, areas, and reference material
- **Review** regularly to keep the system current
- **Plan** each day based on your priorities and energy

**Templates for everything.** Pre-built templates for projects, meeting notes, permanent notes, relationships, and daily plans. No more staring at blank pages wondering how to structure information.

**Everything in one place.** All your notes, tasks, projects, and knowledge live in your Obsidian vault - plain markdown files you own forever. No vendor lock-in, no proprietary formats.

**Use Obsidian alongside Claude.** Your vault is always accessible in Obsidian for browsing, searching, linking, and editing. Claude handles the capture and organization; you can dive into your notes anytime with Obsidian's powerful features (graph view, search, backlinks, plugins).

**Perfect for:**
- Knowledge workers juggling multiple projects
- Anyone wanting structure without complexity
- People with ADHD who need low-friction capture
- Users who want AI-assisted task management they actually own

---

## Quick Start

### Prerequisites

- **Obsidian** installed with a vault created (or Claude will create one)
- **Claude Desktop** (recommended) OR **Claude Code**

### Installation

#### Option A: Claude Desktop (Recommended)

1. **Install the Filesystem Extension** (required for file access):
   - Open Claude Desktop
   - Click the **Extensions** icon (or go to Settings → Extensions)
   - Browse the extension store and find **"Filesystem"**
   - Click **Install** (one-click, no coding required)
   - When prompted, grant access to your Obsidian vault folder

   > **Why?** Claude Desktop needs the Filesystem extension to read and write files in your vault. This is a one-time setup.

2. **Download and install the skill:**
   - Download `second-brain-skill.zip` from the releases
   - Or zip the `.claude/skills/second-brain/` folder yourself
   - Open Claude Desktop → Settings → Skills
   - Click "Install Skill" and select the zip file
   - The skill will be available in all conversations

3. **Set up your vault:**
   - Start a new conversation with Claude
   - Say: **"Set up my Second Brain"**
   - Claude will ask for your vault path and guide you through setup
   - Your vault path will be saved to Claude's Memory (persists across sessions)

#### Option B: Claude Code

1. **Clone this repository:**
   ```bash
   git clone https://github.com/sean-esk/second-brain-gtd.git
   cd second-brain-gtd
   ```

2. **Open Claude Code** in the repository directory

3. **Run setup:**
   - Say: **"Set up my Second Brain"**
   - Claude will detect the skill and guide you through setup

---

## How It Works

### Natural Language Triggers

The skill responds to natural conversation. No special commands needed - just talk to Claude:

| What You Want | What To Say |
|--------------|-------------|
| Capture a thought | "Capture: [your thought]", "Remember this: [idea]", "Note this down" |
| Plan your day | "Plan my day", "What should I work on?", "Morning planning" |
| Process captures | "Process my inbox", "Organize my captures", "GTD processing" |
| End of day review | "Daily closeout", "Review my day", "Evening reflection" |
| Initial setup | "Set up my Second Brain", "Configure my vault" |

### The Core Workflow

```
CAPTURE → PROCESS → PLAN → CLOSEOUT → (repeat)
```

1. **Capture** - Get thoughts out of your head instantly (30 seconds)
2. **Process** - Clarify and organize captures (3x/week, 15 min each)
3. **Plan** - Choose what to work on today (every morning, 5 min)
4. **Closeout** - Review and prep for tomorrow (every evening, 5 min)

**Total time commitment:** ~20-25 min/day

---

## Skill Features

### 1. Quick Capture

**Say:** "Capture: need to schedule dentist appointment" or "Remember this: great idea for the blog post"

**What happens:**
- Claude appends your thought to today's inbox file
- Timestamped and organized
- No categorization yet - just capture (GTD principle: "capture first, clarify later")

### 2. Daily Planning

**Say:** "Plan my day" or "What should I work on today?"

**What happens:**
- Claude checks your inbox (prompts to process if 5+ items)
- Scans all your projects and areas for tasks
- Asks about your energy level and available time
- Generates a prioritized list: must-do, should-do, quick-wins
- Creates a daily plan in your vault

### 3. Inbox Processing

**Say:** "Process my inbox" or "Let's organize my captures"

**What happens:**
- Claude reads all unprocessed captures
- Asks clarifying questions for vague items (batched, not one-by-one)
- Routes actionable items to Projects or Areas
- Routes knowledge items to Permanent Notes
- Reviews all active projects
- Archives completed projects

### 4. Daily Closeout

**Say:** "Daily closeout" or "Review my day"

**What happens:**
- Claude reads today's plan
- Asks what you accomplished
- Marks tasks as completed/partial/deferred
- Asks about tomorrow's priorities
- Creates tomorrow's draft plan (refined in morning)

### 5. Proactive Capture

**Automatic behavior:** When you're discussing ideas or researching topics with Claude, it will offer to capture valuable insights:

> "That's an interesting insight about [topic]. Would you like me to capture this to your Second Brain?"

This ensures valuable knowledge from conversations isn't lost.

---

## Vault Structure

After setup, your Obsidian vault will have this structure:

```
YourVault/
├── 00-Inbox/                  # Unprocessed captures
│   ├── Daily/                 # All captures go here
│   └── Fleeting-Notes/        # Knowledge items during processing
├── 01-Projects/               # Active projects (multi-step outcomes)
├── 02-Areas/                  # Ongoing responsibilities
│   ├── Career-Development.md
│   ├── Health-Fitness.md
│   ├── Personal-Development.md
│   ├── Errands.md
│   ├── Personal-Todos.md
│   └── Relationships/         # Notes per important person
├── 03-Resources/              # Reference materials
│   └── Reference-Notes/       # Summaries of external sources
├── 04-Archives/               # Completed projects
├── Daily Plans/               # Generated daily plans
├── Meeting Notes/             # Meeting documentation
├── Permanent Notes/           # Your synthesized insights (Zettelkasten)
└── Templates/                 # Reusable templates
```

**Key folders:**

- **00-Inbox** - Everything you capture lands here first
- **01-Projects** - Multi-step outcomes with end dates
- **02-Areas** - Ongoing responsibilities (no end date)
- **Permanent Notes** - Your original insights and ideas

---

## Configuration

The skill stores configuration in **Claude's Memory**, which persists across all sessions automatically.

### What Gets Remembered

Claude remembers:
- **Vault path** - Where your Obsidian vault is located
- **Your name** - For personalized interactions
- **Setup status** - Whether initial setup is complete
- **Preferences** - Proactive capture, inbox threshold, etc.

### Why Memory?

Skills in Claude Desktop run in a sandboxed environment and cannot write to arbitrary file paths. Claude's Memory feature provides persistent storage that works in both Claude Desktop and Claude Code.

### Viewing/Editing Memory

In Claude Desktop: **Settings → Capabilities → View and edit memory**

You'll see entries like:
- "User's Second Brain vault is at /Users/sean/Documents/MyVault"
- "Second Brain setup is complete"

### Reconfiguring

To update your setup, just say: **"Reconfigure my Second Brain"** or **"Update my Second Brain setup"**

Claude will show your current configuration and let you update goals, add projects, or change settings.

### Claude Code Fallback

For Claude Code users: If Memory is empty, the skill also checks for a legacy config file at `~/.second-brain/config.json`.

---

## Packaging for Claude Desktop

If you want to modify the skill and reinstall it:

### Using Claude Code

1. Open this repository in Claude Code
2. Make your changes to files in `.claude/skills/second-brain/`
3. Test changes by using the skill directly in Claude Code
4. When satisfied, zip the skill folder:
   ```bash
   cd .claude/skills
   zip -r second-brain-skill.zip second-brain/
   ```
5. Install the new zip in Claude Desktop (Settings → Skills → Install)

### Skill Structure

```
.claude/skills/second-brain/
├── SKILL.md              # Main skill definition and triggers
├── config/               # Configuration templates
├── references/           # Methodology documentation
│   ├── gtd-methodology.md
│   ├── para-zettelkasten.md
│   ├── obsidian-mastery.md
│   └── tagging-strategy.md
├── templates/            # Note templates
│   ├── project.md
│   ├── area.md
│   ├── permanent-note.md
│   └── ...
└── workflows/            # Step-by-step workflow guides
    ├── setup.md
    ├── capture.md
    ├── daily-plan.md
    ├── daily-closeout.md
    └── process-inbox.md
```

---

## Customization

### Your Context

During setup, Claude creates `Permanent Notes/Assisting-User-Context.md` with your:
- Goals (6-month, 3-month, 1-month)
- Work style and schedule
- Communication preferences

This helps Claude prioritize tasks aligned with what matters to you.

### Templates

Templates in the skill can be customized for your workflow:
- Project Template - How new projects are structured
- Area Template - Ongoing responsibility tracking
- Permanent Note Template - Zettelkasten-style notes

### Existing Vaults

The skill works with existing Obsidian vaults. During setup, Claude will:
- Analyze your existing folder structure
- Offer to work alongside your current organization
- Optionally help migrate content to the Second Brain structure
- Never delete or modify existing content without permission

---

## Methodology

The skill combines three proven productivity systems:

### GTD (Getting Things Done)
- **Capture** everything that has your attention
- **Clarify** what each item means and what to do about it
- **Organize** into appropriate categories
- **Reflect** regularly to keep the system current
- **Engage** with confidence in what you're doing

### Zettelkasten
- **Atomic notes** - One idea per note
- **Your own words** - Not copy-paste, synthesis
- **Connected** - Notes link to related ideas
- **Progressive elaboration** - Ideas develop over time

### PARA Method
- **Projects** - Multi-step outcomes with deadlines
- **Areas** - Ongoing responsibilities
- **Resources** - Reference materials
- **Archives** - Completed/inactive items

---

## FAQ

**Q: Do I need to install anything besides the skill?**
A: Yes, for Claude Desktop you need the **Filesystem extension** (one-click install from the extension store). This lets Claude read and write files in your vault.

**Q: Do I need Claude Code?**
A: No. The skill is designed for Claude Desktop. Claude Code is only needed if you want to modify the skill.

**Q: Do I need Node.js or any developer tools?**
A: No. The Filesystem extension installs with one click from the built-in store. No coding required.

**Q: Can I use an existing Obsidian vault?**
A: Yes. The skill works with existing vaults and won't overwrite your content.

**Q: What if I don't have Obsidian?**
A: The skill requires Obsidian as the note storage. [Download Obsidian](https://obsidian.md) (free).

**Q: Is this free?**
A: The skill is free. Obsidian is free. You need a Claude account (free tier or subscription).

**Q: How do I backup my vault?**
A: Your vault is just markdown files. Use Obsidian Sync, iCloud, Dropbox, or Git.

**Q: Can I use this on mobile?**
A: The vault syncs via Obsidian Sync or cloud storage. Claude Desktop is currently desktop-only.

**Q: How does Claude remember my vault path?**
A: Claude uses its Memory feature to remember your vault path across sessions. You can view/edit this in Settings → Capabilities → View and edit memory.

---

## Troubleshooting

### "Claude can't read/write files in my vault" (Claude Desktop)

**This is the most common issue.** You need the Filesystem extension:

1. Open Claude Desktop → Settings → Extensions
2. Install the **Filesystem** extension from the store
3. Grant access to your Obsidian vault folder
4. Restart Claude Desktop

Without this extension, Claude cannot access files on your computer.

### "Claude doesn't know my vault path"

Claude Memory may not have your vault path saved. Say **"Set up my Second Brain"** to reconfigure.

To check what Claude remembers: Settings → Capabilities → View and edit memory

### "Skill not responding to triggers"

1. Make sure the skill is installed (Settings → Skills)
2. Make sure the Filesystem extension is installed (Settings → Extensions)
3. Try restarting Claude Desktop

### "Changes in Claude Code not reflected in Claude Desktop"

Re-zip and reinstall the skill after making changes in Claude Code.

### "Obsidian shows empty vault"

You may have opened the wrong folder. Check your vault path:
- Ask Claude: "What's my Second Brain vault path?"
- Or check Memory: Settings → Capabilities → View and edit memory

### "Permission denied" errors

The Filesystem extension only has access to folders you've explicitly granted. Make sure your Obsidian vault folder is in the allowed list:
1. Settings → Extensions → Filesystem
2. Check the allowed directories
3. Add your vault folder if it's not listed

---

## Learning Path

### Week 1: Foundation
- Set up your Second Brain
- Use "Capture:" throughout the day
- Run "Plan my day" each morning

### Week 2: Build the Habit
- Add "Daily closeout" each evening
- Run "Process my inbox" 3x this week
- Start seeing the system work for you

### Week 3: Refine
- Notice patterns in what you capture
- Adjust your daily rhythm
- Create more projects as needed

### Week 4: Mastery
- The workflow becomes natural
- Customize templates if desired
- The system adapts to you

---

## Credits

**Methodologies:**
- GTD - David Allen
- Zettelkasten - Niklas Luhmann
- PARA - Tiago Forte

**Built with:**
- [Obsidian](https://obsidian.md)
- Claude (Anthropic)

---

## License

This skill is provided as-is for personal use. Customize freely.

**Version:** 4.1
**Last Updated:** 2025-12-11
**Status:** Production Ready
