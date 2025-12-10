---
name: Second Brain
description: |
  Personal knowledge management and productivity system combining GTD (Getting Things Done), Zettelkasten note-taking, and PARA organization for Obsidian vaults.

  Use this skill when:
  - User wants to capture thoughts, ideas, tasks, or notes ("capture this", "save this thought", "remember this", "note this down", "add to my inbox")
  - User wants to plan their day ("plan my day", "what should I work on today", "daily planning", "morning planning")
  - User wants to process their inbox ("process my inbox", "organize my captures", "clarify my tasks", "GTD processing")
  - User wants to review their day ("daily closeout", "review my day", "end of day review", "evening reflection")
  - User wants to set up or configure their Second Brain ("set up my second brain", "configure my vault", "second brain setup")
  - User asks about their projects, tasks, priorities, or goals
  - User is doing research or brainstorming and might want to preserve insights

  PROACTIVE BEHAVIOR: When the user is researching topics, discussing ideas, or working through problems, offer to capture valuable insights to their Second Brain. Ask: "Would you like me to capture this insight to your Second Brain?"
---

# Second Brain

A personal knowledge management and productivity system for Obsidian, combining:
- **GTD (Getting Things Done)** - Task and project management
- **Zettelkasten** - Atomic note-taking for knowledge building
- **PARA Method** - Folder organization (Projects, Areas, Resources, Archives)

## Configuration

**CRITICAL FIRST STEP:** Before any operation, check for configuration.

### Configuration Location

Check for config file at: `~/.second-brain/config.json`

```json
{
  "vaultPath": "/absolute/path/to/obsidian/vault",
  "setupComplete": true,
  "userName": "User Name",
  "userContext": "Permanent Notes/Assisting-User-Context.md"
}
```

**Alternative:** Check environment variable `SECOND_BRAIN_VAULT_PATH`

### If No Configuration Found

Guide the user through setup:

```
I'd like to help you with your Second Brain, but I don't see a configuration yet.

To get started, I need to know where your Obsidian vault is located.

Option 1: Set environment variable
   export SECOND_BRAIN_VAULT_PATH="/path/to/your/vault"

Option 2: Let me create a config file
   Tell me the full path to your Obsidian vault (e.g., /Users/you/Documents/MyVault)

Which would you prefer?
```

Once you have the path:
1. Create `~/.second-brain/` directory if needed
2. Create `config.json` with the vault path
3. Run the full [setup workflow](workflows/setup.md)

### If Configuration Exists

Read the config and use `vaultPath` for ALL file operations.

---

## Core Capabilities

### 1. Quick Capture

**Trigger phrases:** "capture this", "save this thought", "remember this", "note this down", "add to my inbox"

**What it does:** Instantly captures thoughts, tasks, or ideas to today's inbox without categorization.

**GTD Principle:** "Capture first, clarify later."

See: [Capture Workflow](workflows/capture.md)

---

### 2. Daily Planning

**Trigger phrases:** "plan my day", "what should I work on", "daily planning", "morning planning"

**What it does:**
- Checks inbox (prompts to process if 5+ items)
- Scans all projects for next actions
- Asks about energy, context, time available
- Generates prioritized task list (must-do, should-do, quick-wins)

See: [Daily Plan Workflow](workflows/daily-plan.md)

---

### 3. Inbox Processing

**Trigger phrases:** "process my inbox", "organize my captures", "clarify my tasks", "GTD processing"

**What it does:**
- Asks clarifying questions for vague items (batched, not one-by-one)
- Routes actionable items to Projects/Areas
- Routes knowledge items to Permanent Notes
- Reviews all active projects
- Archives completed projects

See: [Process Inbox Workflow](workflows/process-inbox.md)

---

### 4. Daily Closeout

**Trigger phrases:** "daily closeout", "review my day", "end of day review", "evening reflection"

**What it does:**
- Reads today's plan
- Asks what was accomplished
- Marks completed/partial/deferred items
- Asks about tomorrow's priorities
- Creates tomorrow's DRAFT plan

See: [Daily Closeout Workflow](workflows/daily-closeout.md)

---

### 5. Setup & Configuration

**Trigger phrases:** "set up my second brain", "configure my vault", "second brain setup", "reconfigure"

**What it does:**
- First-time: Full interactive setup (goals, relationships, first project)
- Re-run: Update existing configuration

See: [Setup Workflow](workflows/setup.md)

---

## Proactive Capture

**IMPORTANT:** When you notice the user:
- Discovering valuable information during research
- Having insights or realizations
- Discussing ideas worth preserving
- Solving problems in interesting ways

**Offer to capture:**
```
That's an interesting insight about [topic]. Would you like me to capture this to your Second Brain?
```

If they agree:
- Use the capture workflow
- Add context about where the insight came from
- Suggest relevant tags or connections

---

## Vault Structure

The system uses PARA + Zettelkasten organization:

```
{{vaultPath}}/
├── 00-Inbox/
│   ├── Daily/              # Captures go here (YYYY-MM-DD.md)
│   └── Fleeting-Notes/     # Knowledge items during processing
├── 01-Projects/            # Multi-step outcomes with deadlines
├── 02-Areas/               # Ongoing responsibilities
│   ├── Career-Development.md
│   ├── Health-Fitness.md
│   ├── Personal-Development.md
│   ├── Errands.md
│   ├── Personal-Todos.md
│   └── Relationships/      # Individual notes per person
├── 03-Resources/
│   └── Reference-Notes/    # Summaries of external sources
├── 04-Archives/            # Completed/inactive projects
├── Daily Plans/            # Generated daily plans
├── Meeting Notes/          # Meeting documentation
├── Permanent Notes/        # Zettelkasten - synthesized insights
│   └── Assisting-User-Context.md  # User's goals & context
└── Templates/              # Reusable templates
```

See: [PARA + Zettelkasten Guide](references/para-zettelkasten.md)

---

## Unified Task Structure

**ALL Projects, Areas, and Relationship notes use identical priority sections:**

```markdown
## High Priority / Critical
- Urgent/important items (scanned FIRST by daily planning)

## Next Actions / Current Tasks
- Regular priority items (scanned SECOND)

## Someday/Maybe
- Lower priority/exploratory (SKIPPED by daily planning)

## Waiting On
- Blocked by external dependencies

## Completed
- Finished tasks with dates
```

---

## Key References

- [GTD Methodology](references/gtd-methodology.md) - David Allen's Getting Things Done
- [PARA + Zettelkasten](references/para-zettelkasten.md) - Folder organization
- [Obsidian Mastery](references/obsidian-mastery.md) - Obsidian conventions
- [Tagging Strategy](references/tagging-strategy.md) - Tag taxonomy

---

## ADHD-Friendly Principles

The system is designed for users who may have ADHD:

1. **Read entire documents first** - Understand existing structure
2. **Make targeted edits** - Update specific sections, don't append
3. **Never just add to bottom** - Unless explicitly asked
4. **Keep it concise** - Remove redundancy
5. **One plan, not many** - Replace old plans, don't add "revised" sections

**Bad:** Adding "REVISED PLAN" below "TODAY'S PLAN"
**Good:** Replacing "TODAY'S PLAN" content with updated tasks

---

## Daily Workflow Summary

**The Complete Loop:**

1. **Throughout day:** Capture thoughts (30 sec each)
2. **3x per week:** Process inbox - Clarify + Organize (15 min)
3. **Every morning:** Daily plan - Choose what to work on (5 min)
4. **Every evening:** Daily closeout - Reflect + Prep tomorrow (5 min)

**Total time:** ~20-25 min/day + 45 min/week processing = Sustainable!

---

## Examples

### Example 1: Quick Capture

**User:** "Capture: Need to call the dentist and also research new project management tools"

**You:**
1. Read config to get vault path
2. Find/create today's inbox file at `{{vaultPath}}/00-Inbox/Daily/YYYY-MM-DD.md`
3. Append the capture with timestamp
4. Confirm: "Captured at 14:32. You have 3 captures today."

### Example 2: Daily Planning

**User:** "What should I work on today?"

**You:**
1. Check inbox count (process if 5+ items)
2. Scan all projects in `01-Projects/` for next actions
3. Ask: "How's your energy today? Any context constraints?"
4. Generate prioritized list based on goals from user context
5. Create/update `Daily Plans/YYYY-MM-DD.md`

### Example 3: Proactive Capture

**During conversation about a topic:**

**You:** "That insight about [topic] seems valuable. Would you like me to capture it to your Second Brain? I can add it to your inbox for later processing, or create a permanent note if it's already well-formed."

---

## Tool Usage

The skill uses these tools:
- **Read** - Check files, load context
- **Write** - Create new files
- **Edit** - Update existing files
- **Glob** - Find files by pattern
- **Bash** - Create directories if needed

Always use the configured `vaultPath` from `~/.second-brain/config.json` for all operations.
