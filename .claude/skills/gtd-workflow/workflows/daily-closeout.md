# Daily Closeout Workflow

End your day with intention by reviewing what you accomplished and preparing for tomorrow.

> **GTD Stage:** This workflow implements the Reflect stage (daily review and tomorrow prep)

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
1. Today's daily plan: `{{vaultFolder}}/Daily Plans/{{YYYY-MM-DD}}.md`
2. `{{vaultFolder}}/_Context.md` - Current system state
3. `{{vaultFolder}}/Permanent Notes/Assisting-User-Context.md` - User's goals and priorities

---

## Guide the user through an end-of-day review and set up tomorrow's plan

---

## Step 0: Check Inbox (CRITICAL - DO THIS FIRST!)

Before reviewing the day, check if there are items to process:

**Scan these locations:**
- `{{vaultFolder}}/00-Inbox/Daily/` - Daily captures
- `{{vaultFolder}}/00-Inbox/Fleeting-Notes/` - Fleeting notes

**Count unprocessed items:**
- Look for files created today or in the last 2 days
- Count total items across all inbox files

**If 5+ items in inbox:**

Ask the user:
```
📥 INBOX CHECK

Before we review your day, I found {{N}} unprocessed items in your inbox.

Would you like to process your inbox before closeout? This helps ensure everything is organized before planning tomorrow.

Options:
1. Yes - Process inbox first (recommended)
2. No - Skip for now and just review the day
3. Quick review - Show me what's in the inbox first
```

**If user selects Option 1:**
- Inform them: "I'll process your inbox now. This may take a few minutes."
- **Execute the process-inbox workflow** (load [workflows/process-inbox.md](process-inbox.md) and follow it)
- After completion, continue to Step 1 below

**If user selects Option 2:**
- Note: "Skipping inbox processing. Let's review your day."
- Continue to Step 1

**If user selects Option 3:**
- List the inbox items briefly (first few words of each capture with timestamp)
- Then ask Options 1 or 2 again

**If fewer than 5 items:**
- Mention: "Your inbox looks good ({{N}} items). Let's review your day."
- Continue to Step 1

---

## Step 1: Load Today's Plan

**Read:** `{{vaultFolder}}/Daily Plans/{{YYYY-MM-DD}}.md`

If file doesn't exist:
```
I don't see a daily plan for today. That's okay!

Let me ask you about your day anyway, and we'll make sure tomorrow starts strong.
```

If file exists:
- Extract the must-do, should-do, and quick-win tasks
- Note how many tasks were planned

---

## Step 2: Review Accomplishments

Ask the user about what they completed:

```
Let's review your day! 🌟

What did you accomplish today?

You can:
- Tell me what you got done (I'll match it to your plan)
- Share anything you worked on (even if it wasn't on the plan)
- Just say "show me the plan" and I'll walk you through each item

What would you like to do?
```

**If user chooses "show me the plan":**

Go through each planned item one by one:
```
Here's what was on your plan today:

### Must-Do Tasks
1. [Task 1] - Did you complete this? (y/n/partial)
2. [Task 2] - Did you complete this? (y/n/partial)
3. [Task 3] - Did you complete this? (y/n/partial)

### Should-Do Tasks
[Ask about these next]

### Quick Wins
[Ask about these last]
```

**If user provides narrative:**

Parse their response and identify:
- Tasks they completed (mark with [x])
- Tasks they partially completed (note progress)
- Tasks they didn't get to (leave as [ ])
- New things they worked on (not on plan)

---

## Step 3: Update Today's Plan

Update `{{vaultFolder}}/Daily Plans/{{YYYY-MM-DD}}.md` with completion status:

**Mark completed tasks:**
```markdown
- [x] Task description (✅ Completed)
```

**Mark partial tasks:**
```markdown
- [~] Task description (🔄 In Progress - {{user's note on progress}})
```

**Leave incomplete as:**
```markdown
- [ ] Task description (⏭️ Deferred)
```

**Add section for unplanned work:**

If user did things not on the plan:

```markdown
## 🎯 Actual Work Done (Not Planned)

- {{Item 1}}
- {{Item 2}}

*Note: These were valuable but not on today's plan. Consider adding similar work to future plans.*
```

**Add completion summary at bottom:**

```markdown
---

## 📊 Day Summary

**Planned Tasks:** {{N total}}
**Completed:** {{N}} ({{%}})
**Partial:** {{N}}
**Deferred:** {{N}}

**Unplanned Work:** {{N items}}

**Overall:** {{Encouraging assessment - "Great focus day!" or "Lots of unexpected work today" or "Good progress despite challenges" etc.}}

*Closeout completed: {{HH:mm}}*
```

---

## Step 3b: Synchronize Tasks Back to Source Documents (CRITICAL - PREVENTS TASK LOSS!)

Now update the source projects/areas with task completion status. This is where the #source tags become critical.

**For EACH task in today's plan:**

### 1. Parse the #source Tag

Every task should have a `#source/folder-type/file-name` tag.

**Example tags:**
- `#source/projects/website-redesign` → `01-Projects/Website-Redesign.md`
- `#source/areas/personal-todos` → `02-Areas/Personal-Todos.md`
- `#source/relationships/john` → `02-Areas/Relationships/John.md`

**Convert to file path:**
```
#source/projects/website-redesign → {{vaultFolder}}/01-Projects/Website-Redesign.md
#source/areas/health-fitness → {{vaultFolder}}/02-Areas/Health-Fitness.md
```

### 2. Handle Based on Task Status

**For COMPLETED tasks (marked [x]):**

1. **Find the task in source document:**
   - Read the source file
   - Search for the task text (the part before the tags)
   - Should be in "High Priority" or "Next Actions" section

2. **Update in source:**
   - Change from `- [ ] Task description` to `- [x] Task description - Completed {{YYYY-MM-DD}}`
   - Move to "Completed" section in source document
   - Use Edit tool to update the source file

3. **Keep in today's plan:**
   - Task stays marked [x] in plan (for record)
   - No changes needed to plan

**For PARTIAL tasks (marked [~] or with progress note):**

1. **Find the task in source document**

2. **Update in source:**
   - Task stays in "High Priority" or "Next Actions" section (not completed yet)
   - Add progress note: `- [ ] Task description (In progress: {{user's note}})`
   - Keep task active in source

3. **Add to tomorrow's DRAFT plan:**
   - Task gets carried forward with note: `- [ ] [[Project]] - Task (partial from {{today}}) #tags #source/X`
   - User can continue working on it

**For DEFERRED tasks (not worked on, left as [ ]):**

1. **Task stays in source document unchanged:**
   - No modifications to source needed
   - Task remains in its original section

2. **User decision for tomorrow:**
   - Ask: "Do you want to carry this to tomorrow's plan?"
   - If YES: Add to tomorrow's DRAFT plan
   - If NO: Leave in source only (not priority for tomorrow)

### 3. Update Today's Plan Status

After all tasks are synchronized:

**Update today's plan frontmatter:**

```yaml
status: completed  # Change from 'active' to 'completed'
closeout-time: "{{YYYY-MM-DD HH:mm}}"
```

**Why this matters:**
- `completed` status tells tomorrow's planning that closeout was done
- Prevents "previous day not closed out" warning
- Marks this plan as finalized

### 4. Verification

**Before moving on, verify:**
- ✅ All completed tasks moved to "Completed" section in source
- ✅ All partial tasks updated with progress notes in source
- ✅ Deferred tasks left alone in source
- ✅ Today's plan status = `completed`

**If any #source tags are missing:**
- **Warn:** "Task '{{task}}' has no #source tag - cannot return to source automatically"
- Ask user: "Which project/area does this belong to?"
- Manually update the appropriate source

---

## Step 4: Identify Tomorrow's Priorities

Ask the user about tomorrow:

```
Great work today! Let's set up tomorrow. 🚀

Do you have specific things you want to focus on tomorrow, or should I build the plan based on your priorities and incomplete items?

Options:
1. I'll tell you what I want to focus on tomorrow
2. Build a plan based on priorities and what didn't get done today
3. Both - I'll share my focus, and you add other priorities
```

**If Option 1:**

Ask: "What are your top priorities for tomorrow?"

Capture their response, then:
- Use their priorities as the foundation
- Add incomplete items from today as secondary priorities
- Add high-priority items from projects

**If Option 2:**

Build plan automatically:
- Start with incomplete must-do items from today (highest priority)
- Add highest-scoring items from projects
- Consider user's goals from Assisting-User-Context

**If Option 3:**

Ask: "What would you like to focus on tomorrow?"

Then combine:
- User's stated priorities (highest)
- Incomplete items from today (medium-high)
- Project priorities (medium)

---

## Step 5: Generate Tomorrow's DRAFT Plan

Create tomorrow's daily plan without asking energy/context questions (will be asked when they run daily planning in the morning if they want to adjust).

**File:** `{{vaultFolder}}/Daily Plans/{{YYYY-MM-DD+1}}.md`

**Template:**

```markdown
---
title: "Daily Plan - {{Tomorrow's Date}}"
created: "{{YYYY-MM-DD HH:mm}}"
type: daily-plan
status: draft
plan-date: "{{Tomorrow YYYY-MM-DD}}"
previous-plan-status: completed
tags:
  - daily-plan
  - planning
---

# Daily Plan - {{Day of Week}}, {{Month DD, YYYY}}

**Generated:** {{YYYY-MM-DD HH:mm}} (during yesterday's closeout)
**Status:** Draft - Use daily planning workflow in the morning to adjust based on energy and context

---

## 🎯 Priorities for Tomorrow

{{If user provided specific focus, list it here}}

---

## Must-Do (Top 3)

- [ ] [[Project-Name]] - Task description `#high #context/X #energy/X #time/Xm #source/projects/project-name`
- [ ] [[Project-Name]] - Task description `#high #context/X #energy/X #time/Xm #source/projects/project-name`
- [ ] [[Area-Name]] - Task description `#medium #context/X #energy/X #time/Xm #source/areas/area-name`

### Context Notes
- {{Any important context about these tasks}}

---

## Should-Do (Next 5)

- [ ] [[Project]] - Task `#tags #source/X`
- [ ] [[Project]] - Task `#tags #source/X`
- [ ] [[Area]] - Task `#tags #source/X`
- [ ] [[Area]] - Task `#tags #source/X`
- [ ] [[Project]] - Task `#tags #source/X`

---

## Carried Over from Today

{{If any partial or deferred items carried from today}}

- [ ] [[Project]] - Task (partial from {{today}}) `#tags #source/X`
- [ ] [[Project]] - Task (deferred from {{today}}) `#tags #source/X`

---

## ⚡ Quick Wins

{{Quick tasks that can fill gaps}}

- [ ] [[Area]] - Quick task `#context/X #energy/low #time/5m #source/areas/X`
- [ ] [[Area]] - Quick task `#context/X #energy/low #time/10m #source/areas/X`

---

## 💡 Notes for Tomorrow

{{Any thoughts, reminders, or context}}

{{If user mentioned challenges today, reference them}}

---

## Task Format Reminder

**Every task MUST include #source tag:**
- Format: `#source/{folder-type}/{file-name}`
- This tracks where task lives in projects/areas
- Used during tomorrow's closeout to return/update tasks

---

*This is a draft plan created during closeout.*
*Use daily planning workflow in the morning to refine based on your energy and available contexts.*
*All tasks include #source tags for tracking.*
```

**Important:**
- `status: draft` indicates this needs to be refined in the morning
- `plan-date` is tomorrow's date (when plan will be used)
- `previous-plan-status: completed` confirms today was closed out
- ALL tasks must include #source tags (even in draft plan)

---

## Step 6: Update Context File

Update `{{vaultFolder}}/_Context.md` with tomorrow's priorities:

**Update the "Today's Focus" section:**

```markdown
## Today's Focus ({{Tomorrow's Date}})

**Top Priority:**
1. {{Must-do 1}}
2. {{Must-do 2}}
3. {{Must-do 3}}

**Key Context for Tomorrow:**
{{Any important notes}}

**Carried Over:**
- {{N}} tasks from {{Today's date}}

---

## Yesterday's Results ({{Today's date}})

**Completed:** {{N}}/{{N total}} tasks ({{%}})
**Key Wins:** {{1-2 notable accomplishments}}
{{If unplanned work was significant, note it}}
```

---

## Output Format

After completing closeout:

```
✅ DAILY CLOSEOUT COMPLETE

## Today's Results ({{Date}})

📊 Task Completion:
- Planned: {{N}} tasks
- Completed: {{N}} ({{%}}) ✅
- Partial: {{N}} 🔄
- Deferred: {{N}} ⏭️

{{If unplanned work:}}
🎯 Unplanned Work:
- {{N}} additional items completed

🌟 Highlights:
- {{Notable accomplishment 1}}
- {{Notable accomplishment 2}}

{{If challenges:}}
💭 Reflection:
{{Brief note on what got in the way, said encouragingly}}

---

## Tomorrow's DRAFT Plan ({{Date+1}})

📅 Preliminary plan created for {{Day of Week}}, {{Month DD}}

> **This is a DRAFT** - priorities identified but not yet adjusted for tomorrow's energy/context.

🎯 Proposed Top Priorities:
1. {{Must-do 1}}
2. {{Must-do 2}}
3. {{Must-do 3}}

{{If carried over items:}}
⏭️ Carrying Over:
- {{N}} tasks from today

📝 Files Updated:
- Today's Plan: {{vaultFolder}}/Daily Plans/{{today}}.md (✅ marked complete)
- Tomorrow's DRAFT Plan: {{vaultFolder}}/Daily Plans/{{tomorrow}}.md (📝 draft created)
- Context File: {{vaultFolder}}/_Context.md (🔄 updated)

---

📋 **Tomorrow Morning:**

Use daily planning workflow to refine this draft based on:
- Your energy level tomorrow
- Your available contexts (office, computer, phone, etc.)
- Your available time
- Any new priorities that come up

The draft gives you a starting point, but daily planning will optimize it for your actual state tomorrow.

---

💡 Tips for Tomorrow:

{{If completion rate was low:}}
- Consider using daily planning in the morning to adjust priorities
- You had {{%}} completion today - maybe plan fewer tasks tomorrow

{{If lots of unplanned work:}}
- You handled a lot of unplanned work today - great adaptability!
- Consider blocking time for unexpected items

{{If high completion rate:}}
- Great execution today! Keep the momentum going 🚀

{{Always:}}
- Use daily planning workflow in the morning to refine based on energy and context
- Use `/capture` throughout the day for new thoughts and tasks

---

Have a great evening! See you tomorrow. 🌙
```

---

## Important Notes

**Tone:**
- Encouraging and positive
- Acknowledge progress, even if incomplete
- No judgment on unfinished tasks
- Celebrate wins
- Frame challenges constructively

**Flexibility:**
- If user had a rough day, be extra encouraging
- If they crushed it, celebrate enthusiastically
- If they did totally different work than planned, acknowledge adaptability

**Tomorrow's Plan:**
- Keep it draft status - they can refine in the morning
- Base on priorities, not energy/context (that's for morning)
- Carry over incomplete items thoughtfully (understand why they weren't done)

**Update Context Accurately:**
- Track patterns (e.g., always defer certain types of tasks)
- Keep recent history visible

---

## Error Handling

**If no plan exists for today:**
- Still do the review conversation
- Create tomorrow's plan from scratch
- Suggest using daily planning workflow going forward

**If tomorrow's plan already exists:**
- Ask: "I see tomorrow already has a plan. Should I update it or leave it?"
- If update: Merge the content
- If leave: Just update context file

**If user is very brief:**
- Ask follow-up: "Anything else you got done today?"
- Probe: "How do you feel about what you accomplished?"

---

## Tools Available

- **Read** - Read today's plan, context files, user goals
- **Write** - Create tomorrow's draft plan
- **Edit** - Update today's plan with completion status, update _Context.md
- **Glob** - Find project files if needed for tomorrow's priorities
