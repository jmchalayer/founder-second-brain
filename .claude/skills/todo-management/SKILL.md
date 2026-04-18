---
name: todo-management
description: "Manage the founder's Todo.md file at the vault root. Use whenever the user wants to add a task, check off a task, move a task between sections, review their todo list, or capture something they need to do later. Trigger phrases: 'add a task', 'todo', 'remind me to', 'I need to', 'don't let me forget', 'mark that done', 'what's on my list', 'move that to backlog', 'capture this', or any variation of task management. Also trigger when the user casually mentions something they need to do in conversation and it sounds like they want it tracked, even if they don't explicitly say 'add a task'. When in doubt, ask: 'Want me to add that to your todo list?'"
---

# Todo Management

You manage `Todo.md` at the vault root. This is the founder's single capture point for open tasks. Keep it clean, fast, and low-friction.

Todo.md is also read and written by `/morning-planning` (pulls tasks into daily plans, flags overdue) and `/evening-reflection` (marks completed, captures tasks that surfaced during the day).

## Before doing anything

Read `Todo.md` to see the current state. If it doesn't exist, create it with the scaffold below.

## Todo.md structure

```markdown
# Todo

## Inbox
_New tasks land here. Triaged weekly._

## This Week
_Active tasks for the current week. Promoted from Inbox during weekly planning._

## Backlog
_Tasks that matter but aren't this week._

## Someday / Maybe
_Ideas and low-priority items. Revisit quarterly._

## Done
_Completed tasks. Cleared during weekly review._
```

## Core operations

### Adding a task

Default: add to **Inbox**, newest first.

If the user specifies a project or area AND it's not urgent this week, add directly to **Backlog** instead.

If a deadline is given, append `` `due:YYYY-MM-DD` `` after the task. Parse natural language:
- "by Friday" = the coming Friday
- "end of month" = last day of current month
- "next week" = the following Monday
- "by April 1" = nearest future April 1

Format: `- [ ] Task description` or `- [ ] Task description \`due:YYYY-MM-DD\``

If the task relates to a project that has a note in `Projects/`, include the wiki link: `- [ ] Task description [[Project Name]]`. This makes tasks show up in the project's backlinks view in Obsidian. Don't force-link every task; only when the project is obvious.

Only add deadlines for real external commitments (meetings, submissions, events). Most tasks don't need them.

Confirm briefly after adding: "Added to inbox: [task]" or "Added to backlog: [task] (due Apr 1)". One line. Don't be verbose.

### Completing a task

Find it, change `- [ ]` to `- [x]`, append `` `done:YYYY-MM-DD` ``, and move to the Done section.

### Moving a task

Common moves:
- Inbox → This Week (during morning or weekly planning)
- Inbox → Backlog (during weekly triage)
- Backlog → This Week (promoting for the week)
- Anything → Someday/Maybe (deprioritising)

### Reviewing

When asked to review or show the list, give a concise summary:
- Count in each section
- Overdue items (due date passed, still open)
- Items in Inbox > 7 days (stale, need triage)

Don't read the whole file back. Highlight what needs attention.

### Clearing completed tasks

During weekly review (or when asked), clear the Done section. The daily files have the record.

## Rules

- Keep descriptions short and actionable. If vague, rewrite before adding. "Sort out launch" becomes "Confirm launch date with team, post announcement by Friday."
- No duplicates. If similar exists, flag it: "You already have '[X]'. Update it or add separately?"
- Don't reorganise the file unless asked. Do the operation and get out.
- No em dashes.

## Tone

Brief. Transactional. This is a utility, not a conversation. Add, confirm, done.
