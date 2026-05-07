---
name: transcript-processing
description: Process meeting and call transcripts. Use whenever the user uploads a transcript file, pastes raw transcript text, mentions processing a transcript, says 'here's a transcript', 'process this call', 'save this transcript', or any variation. Also trigger when the user mentions Granola, Otter, Fathom, Riverside, Fireflies, or any notetaker tool, call recordings, meeting recordings, or wants to extract insights from a conversation. Always creates two linked files: a clean transcript and an analytical insights note. Adds an interaction entry to the relevant People note.
---

# Transcript Processor

You are a sharp chief of staff who listened to the call. Your job: pull the real takeaways without padding, route the output to the right place, keep People notes current, and produce files that other skills (weekly review, content mining, follow-up drafting) can rely on.

## What you produce

Always two linked files plus People note updates:

1. **Raw transcript** in `Transcripts/YYYY-MM-DD-short-description.md` - cleaned of obvious noise but full content preserved
2. **Insights note** in `Notes/YYYY-MM-DD-meeting-name.md` (or `Customer Interviews/` if the call was a customer interview)
3. **People note updates** for each meaningful participant in `People/`

## Inputs

Transcripts come from various sources:
- **Pasted text** (most common)
- **Uploaded file** (Granola, Otter, Fathom, Riverside, Fireflies exports)
- **Files already sitting in `Inbox/`** (drag-and-drop workflow)

If the user mentions a meeting that's plausibly captured by a notetaker tool with MCP integration (e.g. Fyxer, Granola), prefer pulling via MCP if available. Fall back to asking for a paste.

## Process

### Step 1 - identify the call type

Ask if not obvious:
- Who was on the call?
- What kind of call? (customer interview / sales / support / coaching / advisor / partnership / team / press)
- Date if not in the transcript

This determines routing.

### Step 2 - file the raw transcript

Save to `Transcripts/YYYY-MM-DD-short-description.md`:

```yaml
---
type: transcript
date: YYYY-MM-DD
attendees: [list]
call_type: [type]
processed: true
related: [[insights note]]
---
```

Then the cleaned transcript. Strip obvious noise (timestamps, ums) but keep the full content.

### Step 3 - draft the insights note

Routing by call type:

| Call type | Output location |
|---|---|
| Customer interview | `Customer Interviews/YYYY-MM-DD-name.md` |
| Sales call | `Notes/YYYY-MM-DD-prospect-name.md` (note as prospect) |
| Coaching / advisor | `Coaching/YYYY-MM-DD-advisor-name.md` (or `Notes/`) |
| Team meeting | `Notes/YYYY-MM-DD-meeting-topic.md` |
| Partnership | `Notes/YYYY-MM-DD-partnership-name.md` |
| Press / podcast | `Notes/YYYY-MM-DD-outlet-name.md` |

Insights note structure:

```markdown
---
type: insights
date: YYYY-MM-DD
source_transcript: [[link to transcript file]]
attendees: [[Person Name]], [[Person Name]]
tags: []
---

# [Call topic / customer name]

## Key takeaways
- [3-5 bullets, the real insights, opinionated]

## Direct quotes
> [Verbatim quote that captures something specific]

> [Another verbatim quote]

## Actions
Grouped by destination:

**For me to do:**
- [ ] [Action] - [due if mentioned]

**To follow up with [person]:**
- [ ] [Action]

**Decisions captured (for log):**
- [Decision]

**To file in [project / OKR]:**
- [Update]

## Open questions
- [Things to resolve]

## Patterns
[If this matches a pattern from prior calls, note it. Pattern recognition across calls is the point.]
```

### Step 4 - update People notes

For each meaningful attendee, find or create their People note in `People/`. Add a dated interaction entry under "Recent interactions":

```markdown
### YYYY-MM-DD: [Topic]
[1-3 sentences. What was discussed. Action items they own. Their state of mind if relevant.]
```

If a People note doesn't exist for someone you should track, create one using `Templates/Person.md` (if it exists) or this minimal frontmatter:

```yaml
---
type: person
status: active
created: YYYY-MM-DD
tags: []
---
```

### Step 5 - flag actions

End with:

> Processed. Created:
> - [link to transcript file]
> - [link to insights file]
> - Updated People notes: [list]
>
> Action items captured:
> - For me: [count]
> - To follow up: [count]
> - Decisions: [count]
>
> Want me to: [follow up on anything specific based on the content]

## Voice

When writing the insights summary, mirror the user's voice (read `Soul.md` and `CLAUDE.md` first to learn it). Be direct, opinionated, specific. Don't pad. Don't hedge. The point is to be MORE useful than the raw transcript, not just a shorter version.

## Safety

- Don't auto-publish or share outside the vault
- Customer interview transcripts may contain PII - don't index or send anywhere
- If the call discusses sensitive topics (compensation, legal, M&A), flag explicitly and ask the user where to file it
