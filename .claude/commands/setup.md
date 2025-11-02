---
description: Interactive step-by-step setup to configure your Second Brain system
---

# Second Brain Setup

Welcome! I'm your assistant. Let me help you set up your Second Brain system.

---

## Your Task

Guide the user through setup with ONE question at a time.

**There are TWO possible flows based on setupComplete flag:**
- **Flow A:** setupComplete = false → Full setup (first time)
- **Flow B:** setupComplete = true → Update existing setup

---

## Step 0: Determine Flow (CHECK FIRST!)

**Read:** `.claude/vault-config.json`

```json
{
  "vaultFolder": "ObsidianVault",
  "setupDate": "",
  "setupComplete": false,
  "userName": "",
  "userContext": "Permanent Notes/Assisting-User-Context.md"
}
```

**Check the `setupComplete` field:**

**If setupComplete = false:**
- This is FIRST-TIME SETUP
- Continue to **FLOW A: Full Setup** below

**If setupComplete = true:**
- This is RE-RUN / UPDATE
- Continue to **FLOW B: Update Setup** below

---

# FLOW A: Full Setup (setupComplete = false)

User is setting up for the first time.

---

## Step 1: Detect Vault Folder

**Read vault-config.json to get current vaultFolder** (default: "ObsidianVault")

**Scan root directory for other potential vaults:**

Use Glob or ls to find folders containing:
- `.obsidian/` subfolder (Obsidian vault marker)

**If ONLY "ObsidianVault" found (or no other vaults):**
```
✓ Using vault folder: ObsidianVault

I'll configure the system to work with this vault.
```
- Use "ObsidianVault" as vaultFolder
- Continue to Step 2

**If OTHER vaults found beyond ObsidianVault:**
```
I see the default vault folder is set to "ObsidianVault", but I detected other vaults in this directory:

- ObsidianVault (default example vault)
- {{Other vault 1}}
- {{Other vault 2}}

Would you like to:
1. Use ObsidianVault (the example vault)
2. Use {{Other vault 1}}
3. Use {{Other vault 2}}

Which vault should I configure your Second Brain in?
```

**Wait for user selection.**

**Update vault-config.json with selected vault:**
- Read `.claude/vault-config.json`
- Update `vaultFolder` field with selected name
- Write back

**Store vault folder name for all remaining steps.**

---

## Step 2: Welcome and Introduction

```
Welcome to your Second Brain setup! 🧠

This will take about 10 minutes. I'll ask you a few questions to understand your needs, then set up everything automatically.

We'll cover:
✓ Your goals and what you're working toward (1-2 min)
✓ Important people you interact with (2-3 min)
✓ Your first project (2-3 min)

Then I'll create your personalized system and you'll be ready to start!

Sound good? Ready to begin?
```

**Wait for confirmation.**

---

## Step 3: Get to Know Them (Two-Part Questions)

### Step 3a: Who They Are

```
To set up the system and assist you properly, I need to know a bit about you.

Tell me about yourself - your name, what you do, family situation, and what you're working toward.

For example:
- "I'm John, a software engineer, married with two kids. I'm trying to grow my freelance business while staying healthy and being present with family."

- "I'm Sarah, running a small consulting firm, single, focused on scaling my business and learning new skills. I'm trying to get things more organized."

Just share whatever feels relevant - the more you can share the better context I will have.
```

**Wait for response.**

**Extract:**
- Name
- Career/work context
- Family situation
- Goals and what they're working toward

**Update vault-config.json with userName:**
- Read `.claude/vault-config.json`
- Update `userName` field
- Write back

---

### Step 3b: How They Work

```
Great! Now let me understand how you like to work so I can assist you better.

Tell me about your typical schedule and work preferences:

- What's your normal work schedule? (days per week, typical hours)
- Do you have regular breaks? (lunch time, other breaks)
- How do you prefer to interact with an assistant?
  - Quick, direct suggestions?
  - Detailed explanations?
  - Questions to help you think through decisions?
- Any other preferences about how you like to work?
  - Deep focus blocks vs. task switching?
  - Morning vs. evening productivity?
  - Prefer structured plans or flexible lists?

Share whatever helps me understand your rhythm and preferences!
```

**Wait for response.**

**Extract:**
- Work schedule
- Break times
- Communication preferences
- Energy patterns
- Planning preferences

---

## Step 4: Create Personal Context File

**File:** `{{vaultFolder}}/Permanent Notes/Assisting-User-Context.md`

**Use template:** `{{vaultFolder}}/Templates/User Context.md`

**Fill from Step 3 responses:**
- Name, role, family situation
- Goals (6-month, 3-month, 1-month)
- Work schedule, energy patterns
- Communication and planning preferences

**Inform user:**
```
✅ Created your personal context file!

This helps me:
- Respect your schedule when planning
- Align suggestions with your goals
- Match your communication preferences
- Understand what's "high priority" for you

(You can review/update it anytime at: Permanent Notes/Assisting-User-Context.md)
```

---

## Step 5: Create Default Areas

**Create these 5 areas automatically (if don't exist):**

1. `{{vaultFolder}}/02-Areas/Career-Development.md`
2. `{{vaultFolder}}/02-Areas/Health-Fitness.md`
3. `{{vaultFolder}}/02-Areas/Personal-Development.md`
4. `{{vaultFolder}}/02-Areas/Errands.md`
5. `{{vaultFolder}}/02-Areas/Personal-Todos.md`

**Use Area Template for each, leave task sections empty.**

**Inform:**
```
✅ Created your default areas for organizing tasks:

- Career & Work
- Health & Fitness
- Personal Growth
- Errands & Shopping
- Personal Todos

These give you organized places for one-off tasks.
```

---

## Step 6: Important People

```
Now let's set up relationship tracking for important people in your life.

Who are some people you interact with regularly and want to track conversations/tasks with?

Think about:
- Business partners or co-founders
- Key colleagues or team members
- Family members you coordinate with often
- Mentors, advisors, or clients

List 2-5 people (first name or "John Smith" format), or say "skip":
```

**Wait for response.**

**If they provide names:**

For EACH person:
```
For {{Person}}:

What's your relationship?
- business-partner
- colleague
- family
- mentor
- client
- friend
```

**Create:** `{{vaultFolder}}/02-Areas/Relationships/{{Person-Name}}.md`

**After all created:**
```
✅ Created relationship notes for:
- {{Person 1}} ({{type}})
- {{Person 2}} ({{type}})

When you capture "Discuss budget with {{Person}}", it will route to their note!
```

**If "skip":**
```
No problem! You can add relationship notes later.
```

---

## Step 7: Create First Project

```
Let's create your first project so you can start using the daily planner.

A "project" in GTD is anything that takes more than one step.

Examples:
- Small: "Organize garage" (5-6 steps)
- Large: "Launch website" (20+ steps)

What's ONE thing you're working on right now that has multiple steps?
```

**Wait for response.**

**Ask:**
```
For "{{Their project}}":

1. What does "done" look like?
```

**Wait.**

```
2. What's the very next action you could take?
```

**Wait.**

**Create:** `{{vaultFolder}}/01-Projects/{{Project-Name}}.md`

**Fill in:**
- Desired Outcome
- First next action in High Priority section
- Status: active
- Priority: high (if aligns with goals) or medium

**Offer:**
```
✅ Created: [[{{Project Name}}]]

Want to add another project?
1. Yes - add another
2. No - let's finish up
```

**Allow multiple projects.**

---

## Step 8: Ensure Folder Structure

Create any missing folders:
```
{{vaultFolder}}/
├── 00-Inbox/Daily/
├── 00-Inbox/Fleeting-Notes/
├── 01-Projects/
├── 02-Areas/
├── 02-Areas/Relationships/
├── 03-Resources/Reference-Notes/
├── 04-Archives/
├── Daily Plans/
├── Meeting Notes/
├── Permanent Notes/
└── Templates/
```

**Don't mention to user - just do it.**

---

## Step 9: Create _Context.md

**File:** `{{vaultFolder}}/_Context.md`

**Structure:**
```markdown
---
title: "_Context"
created: "{{YYYY-MM-DD}}"
modified: "{{YYYY-MM-DD}}"
type: meta
status: active
tags:
  - context
  - system
---

# _Context

**Last Updated:** {{YYYY-MM-DD}}

## Active Projects
- [[{{Project 1}}]] - {{Outcome}}

## Key Relationships
- [[{{Person 1}}]] ({{type}})

## Top Priorities
1. {{Priority from user goals}}
2. {{Priority 2}}
3. {{Priority 3}}

## Notes for Assistant
**User Focus:** {{Goals brief}}
**Setup Date:** {{YYYY-MM-DD}}
```

---

## Step 10: Update vault-config.json

**Update setup completion:**

```json
{
  "vaultFolder": "{{ActualVaultUsed}}",
  "setupDate": "{{YYYY-MM-DD}}",
  "setupComplete": true,
  "userName": "{{From Step 3}}",
  "userContext": "Permanent Notes/Assisting-User-Context.md"
}
```

**This marks setup as complete.**

---

## Step 11: Completion Summary

```
✅ SETUP COMPLETE!

I've created your personalized Second Brain system:

📁 **Folder Structure**
- Full PARA organization (Projects, Areas, Resources, Archives)
- Inbox for captures
- Daily Plans folder

📝 **Your Personal Context**
- Saved your goals in: Permanent Notes/Assisting-User-Context.md

📋 **{{N}} Projects**
- [[{{Project 1}}]] - {{Outcome}}
- [[{{Project 2}}]] - {{Outcome}}

🤝 **{{N}} Relationship Notes**
- {{Person 1}} ({{type}})
- {{Person 2}} ({{type}})

🗂️ **5 Default Areas**
- Career, Health, Personal Dev, Errands, Personal Todos

---

## What's Next?

1. `/capture [anything on your mind]` - Start capturing
2. `/daily-plan` - Plan your day tomorrow morning
3. `/process-inbox` - Organize captures (3x/week)
4. `/daily-closeout` - Review each evening

📖 Check out: `START HERE - First Week Guide.md` in your vault!

🎯 Open `{{vaultFolder}}` in Obsidian (download from obsidian.md)

---

Your Second Brain is ready. Let's get things done! 🚀
```

---

# FLOW B: Update Setup (setupComplete = true)

User has already completed setup and is re-running the command.

---

## Step 1: Load Existing Configuration

**Read `.claude/vault-config.json`:**
- Extract vaultFolder, setupDate, userName

**Read user context:** `{{vaultFolder}}/Permanent Notes/Assisting-User-Context.md`

**Scan existing setup:**
- Count area files in `{{vaultFolder}}/02-Areas/`
- Count relationship notes in `{{vaultFolder}}/02-Areas/Relationships/`
- Count active projects in `{{vaultFolder}}/01-Projects/` (status: active)

---

## Step 2: Show Summary and Ask What to Update

```
📊 EXISTING SETUP DETECTED

Your Second Brain is already configured!

**Vault:** {{vaultFolder}}
**Setup Date:** {{setupDate}}
**User:** {{userName}}

**Current Configuration:**
- {{N}} Active Projects: {{list project names}}
- {{N}} Relationship Notes: {{list people names}}
- 5 Default Areas (Career, Health, Personal Dev, Errands, Personal Todos)

**Your Current Goals (from Assisting-User-Context.md):**
{{Extract and show brief summary:}}
- 6-month: {{goal}}
- 3-month: {{goal}}
- 1-month: {{goal}}

**Work Style:**
- Schedule: {{from context}}
- Energy: {{from context}}
- Preferences: {{from context}}

---

Would you like to update anything?

1. Update personal information (goals, work style, preferences)
2. Add more relationship notes
3. Add more projects
4. Switch to a different vault folder
5. No changes needed (exit)

What would you like to do?
```

**Wait for user selection.**

---

## Step 3: Handle Update Request

**If Option 1 (Update personal information):**

```
What would you like to update in your personal context?

Current goals:
- 6-month: {{goal}}
- 3-month: {{goal}}
- 1-month: {{goal}}

Current work style:
- {{summary}}

Tell me what you'd like to change, or provide updated information.
```

**Wait for response.**

**Update Assisting-User-Context.md:**
- Read existing file
- Update ONLY the sections user mentioned
- Use Edit tool (targeted changes)
- Keep rest unchanged

**Confirm:**
```
✅ Updated your personal context!

Changes made:
- {{List what was updated}}

Anything else you'd like to update?
```

---

**If Option 2 (Add relationship notes):**

```
Who would you like to add? (name and relationship type)
```

**For each person:**
- Check if `{{vaultFolder}}/02-Areas/Relationships/{{Person}}.md` exists
- If exists: "{{Person}} already has a note - skipping"
- If not: Create using Relationship Note template

**Confirm:**
```
✅ Added relationship notes:
- {{Person 1}} ({{type}})
- {{Person 2}} ({{type}})

Anything else you'd like to update?
```

---

**If Option 3 (Add projects):**

```
What project would you like to add?
```

**Ask:**
1. What does "done" look like?
2. What's the next action?

**Create:** `{{vaultFolder}}/01-Projects/{{Project-Name}}.md`

**Confirm:**
```
✅ Created project: [[{{Project}}]]

Want to add another project or update something else?
```

---

**If Option 4 (Switch vault folder):**

**Scan for other vaults in root directory.**

```
Available vaults in this directory:
- ObsidianVault (currently selected)
- {{Other vault 1}}
- {{Other vault 2}}

Which vault would you like to switch to?
```

**Update vault-config.json:**
- Change `vaultFolder` to selected vault
- Update `setupDate` to today
- Write back

**Confirm:**
```
✅ Switched to vault: {{NewVault}}

All future commands will use this vault.

Anything else you'd like to update?
```

---

**If Option 5 (No changes):**

```
Your setup is unchanged. You're all set!
```

Exit gracefully.

---

## Step 4: After Any Update

**Update vault-config.json:**
```json
{
  "vaultFolder": "{{Current}}",
  "setupDate": "{{Original}}",
  "setupComplete": true,
  "userName": "{{Current}}",
  "userContext": "Permanent Notes/Assisting-User-Context.md",
  "lastModified": "{{YYYY-MM-DD}}"
}
```

**Update _Context.md:**
- Update "Last Updated" date
- Update active projects list
- Update relationships list
- Update priorities if goals changed

**Final confirmation:**
```
✅ SETUP UPDATED!

Changes applied:
- {{List what was changed}}

📊 Current System:
- {{N}} Active Projects
- {{N}} Relationship Notes
- 5 Default Areas
- Updated: {{YYYY-MM-DD}}

You're all set! Continue using:
- `/capture` - Capture thoughts
- `/daily-plan` - Plan your day
- `/daily-closeout` - Review and prep
```

---

# FLOW A: Full Setup Steps (Continued)

## Step 3: Get to Know Them
[Same as above - Step 3a and 3b]

## Step 4: Create Personal Context File
[Same as above - create new file using template]

## Step 5: Create Default Areas
[Same as above - create 5 areas]

## Step 6: Important People
[Same as above - create relationship notes]

## Step 7: Create First Project
[Same as above - create at least one project]

## Step 8: Ensure Folder Structure
[Same as above - create all folders]

## Step 9: Create _Context.md
[Same as above - create system context]

## Step 10: Mark Setup Complete

**Update vault-config.json:**
```json
{
  "vaultFolder": "{{ActualVaultUsed}}",
  "setupDate": "{{YYYY-MM-DD}}",
  "setupComplete": true,
  "userName": "{{From Step 3}}",
  "userContext": "Permanent Notes/Assisting-User-Context.md"
}
```

**This is critical** - marks setup as done so re-runs use Update flow.

---

## Step 11: Completion Summary

```
✅ SETUP COMPLETE!

I've created your personalized Second Brain system:

📁 **Folder Structure**
- Full PARA organization (Projects, Areas, Resources, Archives)
- Inbox for captures
- Daily Plans folder

📝 **Your Personal Context**
- Saved your goals in: Permanent Notes/Assisting-User-Context.md

📋 **{{N}} Projects**
- [[{{Project 1}}]] - {{Outcome}}

🤝 **{{N}} Relationship Notes**
- {{Person 1}} ({{type}})

🗂️ **5 Default Areas**
- Career, Health, Personal Dev, Errands, Personal Todos

---

## What's Next?

1. `/capture [your first thought]` - Start capturing
2. `/daily-plan` - Plan your day tomorrow morning
3. `/process-inbox` - Organize captures (3x/week)
4. `/daily-closeout` - Review each evening

📖 Check: `START HERE - First Week Guide.md` in your vault

🎯 Open `{{vaultFolder}}` folder in Obsidian (download from obsidian.md)

---

Your Second Brain is ready. Let's get things done! 🚀
```

---

## Important Notes

**Vault detection:**
- ONLY scans for other vaults if setupComplete = false (first-time setup)
- Asks user to choose if multiple vaults found
- Default is ObsidianVault (the example vault)

**setupComplete flag:**
- false → Full setup flow
- true → Update flow

**No conditional logic in every step:**
- Two separate, clean flows
- Simple fork at the beginning
- Much easier to maintain

**Update flow is simple:**
- Read existing config and context
- Show summary
- Ask what to update
- Update only what user specifies
- Done

---

Now run the setup process!
