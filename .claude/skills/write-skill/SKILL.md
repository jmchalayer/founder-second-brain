---
name: write-skill
description: Create a new skill for this vault, or improve an existing one. Use when a workflow gets repeated 3+ times. Triggers on "write a skill", "create a skill", "new skill for X", "I need a skill for", or when describing a repeatable workflow you want codified.
---

# Write Skill

You help the user codify repeatable workflows into skills. A skill is just a markdown file at `.claude/skills/<skill-name>/SKILL.md`. Frontmatter says when it triggers. Body says what to do.

## When to write a skill

- A workflow has been done 3+ times and follows the same shape
- The user keeps explaining the same thing
- You want consistency in tone, format, or output

**Don't write a skill for:**
- One-off tasks
- Things that need fresh judgement every time
- Workflows that vary too much

## Process

### Step 1 - capture intent

Ask in one or two questions per turn (don't fire all at once):

1. **What's the workflow?** End-to-end. What triggers it? What does success look like?
2. **What inputs?** (Transcript, URL, customer name, file, etc.)
3. **What output?** (A draft, a saved file, an updated note?)
4. **Where does the output go?** Specific folder? File naming convention?
5. **Examples of "good"?** Get one or two real examples.
6. **Voice / tone?**
7. **What should NEVER happen?** (Don't auto-send, don't include X, don't reference Y.)

### Step 2 - check for duplicates

Before drafting, check `~/.claude/skills/` and `.claude/skills/` in this vault. If a similar skill exists, surface it and ask whether to use it, modify it, or create a variant.

### Step 3 - propose [GOAL] and [PERSONA]

Before drafting the body, propose:

- **[GOAL]:** what success looks like in one sentence (outcome, not format)
- **[PERSONA]:** who the skill behaves as (e.g. "sharp chief of staff", "ruthless editor", "supportive coach")

Get the user to confirm both before writing. These shape everything else.

### Step 4 - draft the skill

Use this structure:

```markdown
---
name: [skill-name-kebab-case]
description: [One paragraph. What it does, when it triggers, what it produces. Triggers on "X", "Y", and similar phrases.]
---

# [Skill Name]

[1-2 sentence intro. The persona + the outcome.]

## When to use this

- [Trigger 1]
- [Trigger 2]

## What you need

- [Input 1]
- [Input 2]

## Process

### Step 1 - [first step]
[Specific instructions for the AI.]

### Step 2 - [next step]
[More instructions.]

## Output

[Where it goes. File naming. Frontmatter. Structure.]

## Voice / tone

[Reference the user's voice or override for this specific skill.]

## Safety

- [Things never to do without confirmation]
```

### Step 5 - self-audit

Before showing the user, check the draft against these:

- **Outcome-oriented, not format-prescriptive?** Good skills describe what success looks like, not the exact words.
- **Trigger description specific enough?** The frontmatter description is what the LLM reads to decide whether to fire.
- **Under 500 lines without heroics?** If it's longer, the workflow is probably too complex - split it.
- **Resistant to recipe accumulation?** Steps describe outcomes, not exact prompts. Don't bake in brittle recipes.
- **References existing files** (e.g. "Read `Soul.md` first to learn the voice")?

Fix anything failing.

### Step 6 - test on a real example

Once the user approves, save to `.claude/skills/[name]/SKILL.md`. Then say:

> Saved. Want to test it on a real example now? Give me [the input it needs] and I'll run through it.

If the test reveals issues, edit the SKILL.md and retest.

## Tips for great skills

- **Lead with what NOT to do** if there's a common mistake
- **Reference files the skill should read** (`Soul.md`, `Goals/`, etc.)
- **Keep voice consistent** with the vault's brand voice unless there's a specific reason to override
- **Define triggers concretely.** "Process the transcript" is vague. "Save raw to Transcripts/, extract insights to Notes/, update relevant People note" is a skill.
- **Use [GOAL] and [PERSONA] tags** at the top of the body if the skill is opinionated (most are)

## Naming conventions

- Use kebab-case: `customer-success-reply` not `customerSuccessReply`
- Verb-first or noun-first, your choice, but be consistent
- Keep it short enough to type as a slash command

## Examples in this vault

Look at these for reference:
- `.claude/skills/onboard/SKILL.md` - long, multi-step interview skill
- `.claude/skills/transcript-processing/SKILL.md` - input → multi-output skill
- `.claude/skills/update-wiki/SKILL.md` - read-many → write-many skill
