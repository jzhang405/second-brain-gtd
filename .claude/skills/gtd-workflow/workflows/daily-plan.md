# Daily Plan Workflow

Create an optimized daily execution plan by analyzing all active projects and available context.

> **GTD Stage:** This workflow implements the Engage stage (choosing what to work on)

---

## Context

**CRITICAL FIRST STEP:** Read `.claude/vault-config.json` to get the vault folder name.

**If vault-config.json doesn't exist:**
- User hasn't run `/setup` yet
- Respond: "Please run `/setup` first to configure your Second Brain!"
- Do not proceed

**Extract `vaultFolder` value and use it for all paths in this workflow.**

---

**Then read these files:**
1. `{{vaultFolder}}/_Context.md` - Current system state (if exists)
2. `.claude/skills/gtd-workflow/references/gtd-methodology.md` - GTD principles (four criteria model)
3. `{{vaultFolder}}/Permanent Notes/Assisting-User-Context.md` - User's goals and priorities

---

## Generate an intelligent daily plan, checking previous day and inbox first

---

## Step -1: Check Previous Day's Plan (PREVENTS TASK LOSS!)

Before doing anything else, check if yesterday's plan was properly closed out.

**Read yesterday's plan:** `{{vaultFolder}}/Daily Plans/{{YYYY-MM-DD minus 1 day}}.md`

**Check the frontmatter `status` field:**

**If file exists AND status = `active` (not `completed`):**

```
⚠️ PREVIOUS DAY NOT CLOSED OUT

I see yesterday's plan ({{date}}) wasn't closed out yet.

This means tasks might not have been returned to their projects/areas, and we could lose track of incomplete work.

Would you like to:
1. Close out yesterday first (recommended) - ensures tasks are tracked
2. Skip and plan today anyway (risky - incomplete tasks may be lost)
3. Show me yesterday's plan so I can review it

What would you like to do?
```

**If user selects Option 1:**
- Inform them: "I'll close out yesterday now. This ensures nothing is lost."
- **Execute the daily-closeout workflow** for yesterday (load [workflows/daily-closeout.md](daily-closeout.md) and follow it for yesterday's date)
- After completion, continue to Step 0 below

**If user selects Option 2:**
- **Warn:** "⚠️ Warning: Proceeding without closeout. Yesterday's incomplete tasks won't be returned to source and may be lost."
- Note in today's plan: "Previous day not closed out - manual task review needed"
- Continue to Step 0

**If user selects Option 3:**
- Read and display yesterday's plan
- Then ask Options 1 or 2 again

**If file doesn't exist OR status = `completed`:**
- Yesterday was properly closed out (or no plan existed)
- Continue to Step 0

**Why this matters:** Without closeout, incomplete tasks stay orphaned in yesterday's plan and aren't returned to their source projects/areas. This step prevents task loss.

---

## Step 0: Check Inbox (CRITICAL - DO THIS SECOND!)

Before planning, check if the inbox needs processing:

**Scan these locations:**
- `{{vaultFolder}}/00-Inbox/Daily/` - Daily captures
- `{{vaultFolder}}/00-Inbox/Fleeting-Notes/` - Fleeting notes

**Count unprocessed items:**
- Look for files created in the last 3 days
- Count total items across all inbox files

**If 5+ items in inbox:**

Ask the user:
```
📥 INBOX CHECK

I found {{N}} unprocessed items in your inbox from the last few days.

Would you like to process your inbox before planning your day? This ensures all captured tasks and ideas are considered in your plan.

Options:
1. Yes - Process inbox first (recommended)
2. No - Skip for now and just plan with what's in projects
3. Quick review - Show me what's in the inbox first
```

**If user selects Option 1:**
- Inform them: "I'll process your inbox now. This may take a few minutes."
- **Execute the process-inbox workflow** (load [workflows/process-inbox.md](process-inbox.md) and follow it)
- After completion, continue to Step 1 below

**If user selects Option 2:**
- Note: "Skipping inbox processing. I'll plan based on your current projects."
- Continue to Step 1

**If user selects Option 3:**
- List the inbox items briefly (first few words of each capture with timestamp)
- Then ask Options 1 or 2 again

**If fewer than 5 items:**
- Mention: "Your inbox looks good ({{N}} items). Proceeding with daily plan."
- Continue to Step 1

---

## Step 1: Gather Intelligence

**Read:**
- All files in `{{vaultFolder}}/01-Projects/` with status = `active` (check frontmatter)
- `{{vaultFolder}}/_Context.md` for high-level overview (if exists)
- `{{vaultFolder}}/Permanent Notes/Assisting-User-Context.md` for user's goals

**Check for active projects:**
- Count how many files have `status: active`

**If ZERO active projects found:**

Ask the user:
```
I don't see any active projects yet!

To create a daily plan, I need projects with next actions to prioritize.

Would you like to:
1. Process your inbox to create projects from your captures
2. Manually create your first project in 01-Projects/
3. Skip planning for now (come back after you have projects)

What would you like to do?
```

If user selects option 1: Execute the process-inbox workflow (load [workflows/process-inbox.md](process-inbox.md)) then continue to planning.
If user selects option 2 or 3: Exit gracefully.

**If projects exist, continue:**

**Scan for tasks across all locations:**

1. **Projects:** Read all files in `{{vaultFolder}}/01-Projects/` with `status: active`
   - Extract from "High Priority Next Actions" section (highest priority)
   - Extract from "Next Actions" section (regular priority)
   - Extract from "Waiting On" section
   - SKIP "Someday/Maybe" section

2. **Areas:** Read all area files in `{{vaultFolder}}/02-Areas/`
   - Extract from "High Priority Tasks" or "Critical Tasks" section (highest priority)
   - Extract from "Next Actions" or "Current Tasks" section (regular priority)
   - Extract from "Waiting On" section
   - SKIP "Someday/Maybe" section
   - SKIP "Recurring Responsibilities" unless overdue

3. **Relationships:** Read all person notes in `{{vaultFolder}}/02-Areas/Relationships/`
   - Extract from "High Priority" section (urgent people items)
   - Extract from "Next Actions → To Discuss" section (things to talk about)
   - Extract from "Waiting On" section (things you're waiting on from people)
   - SKIP "Someday/Maybe"

4. **Context:** Check `_Context.md` for flagged priorities

**Note:** You don't need to exhaustively scan every section. Focus on High Priority sections first, then sample Next Actions sections based on user's stated focus and available time.

---

## Step 1b: Tag Tasks with Source Information (CRITICAL FOR TASK TRACKING!)

As you scan tasks, **preserve their origin** so they can be returned during closeout.

**For each task you're considering for today's plan:**

1. **Note the source location:**
   - Projects: `01-Projects/Project-Name.md`
   - Areas: `02-Areas/Area-Name.md`
   - Relationships: `02-Areas/Relationships/Person-Name.md`

2. **Create source tag** from file path:
   - `01-Projects/Website-Redesign.md` → `#source/projects/website-redesign`
   - `02-Areas/Personal-Todos.md` → `#source/areas/personal-todos`
   - `02-Areas/Relationships/John.md` → `#source/relationships/john`

**Format pattern:** `#source/{folder-type}/{file-name-lowercase-with-hyphens}`

**Why this matters:** The #source tag is the "breadcrumb trail" back to where the task lives. During closeout, this tag tells you exactly where to return/update the task.

**Task remains in source:** Don't remove tasks from projects/areas yet. They stay in source until closeout confirms what happened (completed/partial/deferred). This prevents loss if planning is interrupted.

---

## Step 2: Assess Context (GTD Four Criteria)

Ask the user about today's context (from gtd-methodology.md - four criteria for choosing actions):

1. **What's your energy level today?** (High/Medium/Low)
2. **What contexts are available?** (Office, Computer, Phone, Home, Errands, Travel)
3. **How much time do you have?** (Rough blocks: morning, afternoon, evening)
4. **Any hard deadlines today?** (Things that MUST happen)

---

## Step 3: Generate Plan

Create a prioritized action list using these criteria:

**Priority Scoring:**
- High priority project = +3
- Medium priority project = +2
- Low priority project = +1
- Due today = +5
- Due this week = +2
- Matches available context = +2
- Matches energy level = +2
- Time available fits task = +1

**Sort tasks by total score, then present:**

**Top 3 Must-Do:**
- Highest scoring tasks
- Focus on project advancement
- Clear, concrete actions

**Next 5 Should-Do:**
- Important but not urgent
- Context-appropriate
- Time-boxed

**Waiting On:**
- Items blocked by others
- Check if any can be unblocked today

**Quick Wins (5-15 min):**
- Low-energy, short tasks
- Good for between meetings or low energy periods

---

## Step 4: Create Daily Plan File

Create today's daily plan file in the Daily Plans folder:

**File:** `{{vaultFolder}}/Daily Plans/{{YYYY-MM-DD}}.md`

**Check if file already exists:**

- If exists with `status: draft` (from last night's closeout):
  - Read the draft priorities
  - Keep the priorities but enhance with today's energy/context
  - Update status to `active`
  - Add note: "Enhanced from last night's draft based on your energy and context today"

- If exists with `status: active` (re-running plan during day):
  - Update with new plan
  - Note: "Plan updated at {{time}}"

- If doesn't exist:
  - Create new plan file

**Plan File Structure:**

```markdown
---
title: "Daily Plan - {{YYYY-MM-DD}}"
created: "{{YYYY-MM-DD HH:mm}}"
type: daily-plan
status: active
plan-date: "{{YYYY-MM-DD}}"
previous-plan-status: completed
tags:
  - daily-plan
  - planning
---

# Daily Plan - {{Day of Week}}, {{Month DD, YYYY}}

**Generated:** {{HH:mm}}
**Status:** Active

---

## 🎯 Today's Plan

**Energy:** 🔋🔋🔋 [User input]
**Context:** [User input]
**Available Time:** [User input]

### Must-Do Today (Top 3)

- [ ] [[Website-Redesign]] - Call vendor about pricing `#high #context/phone #energy/medium #time/15m #source/projects/website-redesign`
- [ ] [[Client-Proposal]] - Finish budget spreadsheet `#high #context/computer #energy/high #time/1h #source/projects/client-proposal`
- [ ] [[Personal-Todos]] - Schedule dentist appointment `#medium #context/phone #energy/low #time/10m #source/areas/personal-todos`

### Should-Do (Next 5)

- [ ] [[Marketing-Campaign]] - Draft social media posts `#medium #context/computer #energy/medium #time/45m #source/projects/marketing-campaign`
- [ ] [[Health-Fitness]] - Review meal plan `#low #context/anywhere #energy/low #time/15m #source/areas/health-fitness`
[...]

### Carried Over from Yesterday

{{If tasks carried from previous day's plan}}

- [ ] [[Project]] - Task description (partial from {{yesterday}}) `#tags #source/X`

### ⏳ Waiting On (Check-ins)

- John's response (budget) - *Follow up if no response by EOD*
- API key from vendor - *Email if not received*

### ⚡ Quick Wins (Fill gaps)

- [ ] [[Errands]] - Pick up dry cleaning `#context/errands #energy/low #time/5m #source/areas/errands`
- [ ] [[Personal-Development]] - Read one article `#context/anywhere #energy/low #time/10m #source/areas/personal-development`

---

## Task Format Notes

**Every task MUST include #source tag:**
- Format: `#source/{folder-type}/{file-name}`
- This tracks where task lives in projects/areas
- Used during closeout to return/update tasks

---

*Plan generated at {{time}}*
*Based on [N] active projects with [N] next actions available*
*Tasks remain in source until closeout*
```

**Frontmatter Fields Explained:**
- `status`: `draft` (from closeout) → `active` (being worked on) → `completed` (closeout done) → `archived` (old)
- `plan-date`: The date this plan is for (may differ from created date if made night before)
- `previous-plan-status`: Status of yesterday's plan (helps track if closeout was skipped)

---

## Step 5: Update Context File

If `_Context.md` exists, update it with today's priorities:

```markdown
# _Context.md

Last Updated: {{date:YYYY-MM-DD HH:mm}}

## Today's Focus ({{date:YYYY-MM-DD}})

**Top Priority:**
1. [[Project A]] - Next: [Action]
2. [[Project B]] - Next: [Action]
3. [[Project C]] - Next: [Action]

**Context:** [User's available contexts]
**Energy:** [User's energy level]

[... rest of context file ...]
```

If `_Context.md` doesn't exist, create it with this basic structure.

---

## Output Format

After generating the plan:

```
✅ DAILY PLAN GENERATED

📊 Intelligence Gathered:
- Active Projects: [N]
- Available Next Actions: [N]
- Waiting On: [N]

🎯 Plan Summary:
- Must-Do Today: 3 tasks
- Should-Do: 5 tasks
- Quick Wins: [N] tasks
- Waiting On Check-ins: [N]

📝 Files Updated:
- Daily Plan: {{vaultFolder}}/Daily Plans/{{date}}.md
- Context File: {{vaultFolder}}/_Context.md

💡 Recommendation:
Start with: [[Project]] - [Next Action]
This is your highest priority based on context and energy.
```

---

## Important Notes

- Always consider user's actual available time
- Match energy to task complexity
- Respect context constraints (can't make phone calls in a meeting)
- Flag overcommitment (more than 8 hours of tasks)
- Suggest what to defer if plan is too packed

---

## Tools Available

- **Read** - Read project files, area files, relationship notes, context files
- **Write** - Create daily plan file
- **Edit** - Update existing daily plan, update _Context.md
- **Glob** - Find all active projects
- **Grep** - Search for specific tasks or priorities
