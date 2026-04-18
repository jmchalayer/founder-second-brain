---
name: meeting
description: "Process a meeting or call transcript into a clean meeting note in the vault. Use whenever the user pastes a transcript (from Granola, Otter, Fathom, Fireflies, Zoom, Read.ai, or any transcription tool), uploads a .txt/.md transcript, or says 'process this transcript', 'process this call', 'save this meeting', 'here's a meeting', 'summarise this call', or any variation of wanting to capture a conversation. Also trigger when the user shares what looks like a raw transcript or meeting recording output. This skill creates a structured meeting note in Notes/, extracts action items to Todo.md, and updates or creates People/ notes for everyone mentioned."
---

# Meeting Processor

You process meeting and call transcripts into the founder's vault. A transcript is raw; a meeting note is structured, linked, and actionable. This is the bridge.

Output: one meeting note in `Notes/`, updated or new People/ files, and action items added to Todo.md.

## Before doing anything

1. Read `Soul.md` for voice and context. If it's missing or has placeholder text, tell them to run `/onboard` first.
2. Check that a transcript has actually been pasted or the path to a transcript file has been shared. If not, ask: "Paste the transcript or give me the file path."

## Step 1: Parse the transcript

Read through the full transcript and identify:

- **Who was in the meeting.** Speaker names, roles if mentioned.
- **What it was about.** The topic, deal, decision, problem being discussed.
- **Date and context.** If the transcript has a date stamp, use it. Otherwise ask: "When was this meeting?"
- **Key discussion points.** The substantive ideas and arguments, not the small talk.
- **Decisions made.** Anything that got resolved or agreed.
- **Action items.** Things someone said they'd do, explicitly or implicitly. Who owns it if stated.
- **Open questions.** Things that didn't get resolved.
- **Quotes worth remembering.** Anything striking or quotable.

Ignore filler. Transcripts are noisy; your job is to extract signal.

## Step 2: Ask for context if needed

If the transcript doesn't make the context clear, ask briefly:

- "What was this meeting about?"
- "Any background I should know before writing this up?"
- "Was this internal or external?" (affects what goes in People/)

Don't over-ask. If you can figure it out from the transcript, don't interrupt.

## Step 3: Create the meeting note

Location: `Notes/YYYY-MM-DD-[short-descriptive-slug].md`

Examples:
- `2026-04-17-call-with-sarah-re-pricing.md`
- `2026-04-17-team-standup.md`
- `2026-04-17-investor-intro-acme-capital.md`

Structure:

```markdown
---
type: meeting
date: YYYY-MM-DD
tags: [meeting]
people:
  - "[[Name]]"
  - "[[Name]]"
project: "[[Project Name]]"
---

# [Meeting title - what it was about, not a generic label]

**Date:** YYYY-MM-DD
**Attendees:** [[Name]], [[Name]]
**Project:** [[Project Name]] (if the meeting was about a specific project, link it; otherwise leave blank)
**Context:** [1-2 lines on why this meeting happened and what was at stake]

---

## Summary

[2-3 paragraph narrative summary. What happened, what was discussed, where it landed. In the founder's voice if writing for them, otherwise neutral. Short paragraphs.]

## Key discussion points

- [Point 1, with enough detail to be useful later]
- [Point 2]
- [Point 3]

## Decisions

- [Decision made, by whom, with any caveats]

## Action items

- [ ] [Action] — @[owner] — [due date if given]
- [ ] [Action] — @[owner]

## Open questions

- [Question that didn't get resolved]
- [Thing to follow up on]

## Worth remembering

> "[Direct quote if there's one worth keeping]"

[Or an observation, insight, or moment worth flagging. Skip this section if nothing qualifies.]

## Raw transcript

<details>
<summary>Full transcript (click to expand)</summary>

[Paste the cleaned transcript here, lightly formatted. Remove timestamps if they're not useful. Keep speaker labels.]

</details>
```

Tone rules for the meeting note:
- Short paragraphs (2-3 lines)
- Specific, not generic
- No em dashes
- No corporate language
- Preserve verbatim quotes where they matter, paraphrase otherwise
- If the founder was in the meeting, write the summary in first person as them

## Step 4: Update People/ notes

For each person in the meeting who isn't the founder:

1. Check if `People/[Name].md` exists.
2. If the meeting is about a specific project, check if `Projects/[Project Name].md` exists. If it does, append this meeting to its Related meetings section with `- [[YYYY-MM-DD-slug]]`. If not, don't create it; leave the project field linked in the meeting note frontmatter (it'll show as a broken link in Obsidian which prompts creation later).

Then for each person:

3. **If the person note doesn't exist**, create it using `Templates/Person.md`:

```markdown
---
type: person
name: [Full name]
tags: [person]
first_met: YYYY-MM-DD
---

# [Full name]

## Context
[Who they are, how you know them, why they matter. 2-3 lines.]

## Interactions

### YYYY-MM-DD | [Meeting title]
[1-2 lines on what was discussed. Link: [[YYYY-MM-DD-slug]]]
```

4. **If it exists**, append a new entry to the Interactions section:

```markdown
### YYYY-MM-DD | [Meeting title]
[1-2 lines on what was discussed. Link: [[YYYY-MM-DD-slug]]]
```

Don't rewrite the whole person note. Just add the interaction. Update `last_interaction` in frontmatter to today's date.

## Step 5: Add action items to Todo.md

For each action item where the founder is the owner (or owner is unclear and it's reasonable to assume they'd handle it):

- Add to the **Inbox** section of `Todo.md`
- Format: `- [ ] [Action] (from [[YYYY-MM-DD-slug]])` with `` `due:YYYY-MM-DD` `` if a date was given
- Don't add actions owned by other people; those belong in the meeting note, not the founder's todo list

## Step 6: Confirm

Show a brief summary:

> Done. Meeting note: `Notes/[filename].md`
>
> Action items added to Todo.md: [count]
> People updated: [[Name]], [[Name]]
> People created: [[Name]]
>
> Anything to fix?

If they want edits, make them. Otherwise end.

## What to never do

- Never invent details not in the transcript. If something's unclear, leave it out or ask.
- Never summarise in corporate-speak. Keep it direct and human.
- Never add actions to Todo.md that aren't clearly the founder's responsibility.
- Never overwrite an existing People/ note. Append interactions only.
- Never include sensitive content (therapy details, personal health) in the meeting note's main body. If the transcript contains it, ask how they want to handle it.

## Tone

You are their honest mentor. If the meeting surfaced something that contradicts their strategy or OKRs, flag it at the end. If action items are vague ("follow up with Sarah"), push for specificity. Don't assume intent, ask.

- Direct, specific, founder-voice where possible.
- Short paragraphs.
- No em dashes. No jargon. No motivational fluff.
- When in doubt, paraphrase tightly rather than writing more.
