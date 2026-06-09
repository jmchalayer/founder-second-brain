# Founder Second Brain

As a founder you're juggling a thousand priorities. It's overwhelming, all the time.

I've tried every system. Paper diaries, productivity planners, Freeflow, OKRs, Notion dashboards. They worked for a while, then the habit dropped. Or something happened and I got sidetracked. Back to chaos.

Here's what I realised: none of them were what I actually needed. Which is an accountability partner and a coach. Someone who remembers what I said yesterday, pushes back when I drift, and stress-tests my plans before I burn a week on the wrong thing.

Paying a human to do that every day would cost thousands. Not accessible to anyone, really. Until AI.

The other thing I knew: journaling works. I could just never do it consistently.

So I built this. A framework that blends productivity planning, journaling, and accountability coaching into one daily loop. It's transformed the way I work. Productivity is up. Work satisfaction is up. Happiness is up.

The best part: I stop going to bed feeling like I have too much on my plate. Everything's planned, scheduled, organised. In the vault, and in my head.

This is for founders who are tired of catching up, who want to get ahead and stay there.

> *"Brought back my sanity. I sleep better knowing all the stuff rattling around my brain is stored and not lost. Love planning my week and days with it. It's made me way more focused and effective."*
>
> — Daniel Van Binsbergen, Founder of DraftPilot.ai

## Built portable, by design

This vault is plain markdown in plain folders. Nothing is locked into Claude. The skills work with **Claude Code, Codex CLI, Cursor**, and anything else that respects `CLAUDE.md` or `AGENTS.md`. When the best AI tool changes (and it will), you switch in an hour. Not a month.

That's the principle: the value is in the structure of your second brain, not in any one tool. The tool is replaceable. The brain isn't.

## How it works

Three layers:

```
        Claude Code, Codex, Cursor, anything next
                          │
                          ▼
        ┌──────────────────────────────┐
        │  CLAUDE.md / AGENTS.md       │  ← the map (read first)
        ├──────────────────────────────┤
        │  Wiki/                       │  ← synthesis layer
        ├──────────────────────────────┤
        │  Soul, Goals, Journal,       │  ← data layer
        │  People, Projects, Notes     │
        └──────────────────────────────┘
```

The agent reads the map first, drills into the wiki when it needs an overview, opens raw data files only when it needs a specific document. Token-efficient, fast, scales.

## How the daily loop works

Daily, weekly, and quarterly rituals that run themselves:

- **Morning:** pick 1-3 priorities, tie each one to a quarterly goal, block the time.
- **Evening:** review what actually happened vs what you planned.
- **Friday:** score the week, plan the next one.
- **Start of each quarter:** set OKRs that force focus.
- **Whenever you have an idea:** stress-test it before you build.

The AI reads your past entries. Pushes back when you overload. Flags patterns you can't see in the moment. Stress-tests your thinking. It's a coach that doesn't forget what you told it on Monday.

## What it does

15 skills that run the full loop:

| Skill | When to use it |
|---|---|
| `/onboard` | Once. First-time setup. Interviews you and writes your Soul.md, CLAUDE.md, AGENTS.md, first OKR file, and stub people/project notes. |
| `/daily-briefing` | First thing in the morning. Surfaces dropped balls, must-reply-today, and today's calendar from your personal comms (email + calendar by default; extends to Slack/WhatsApp if connected). Read-only, evidence-backed. Pairs with `/morning-planning`. |
| `/morning-planning` | Start of each day, after the briefing. Picks 1-3 priorities, connects them to your OKRs, creates the daily planner file. |
| `/evening-reflection` | End of each day. Reviews what got done, captures wins, mood, learnings. Updates your todo list. |
| `/weekly-planning` | Friday evening. Reviews the week against OKRs, force-ranks next week's priorities, audits what could have been delegated to AI. |
| `/weekly-sweep` | Weekly vault hygiene. Detects drift in People, OKRs, Projects, Wiki, Inbox. Produces a sweep-review file you approve item by item. |
| `/okr-planning` | Start of each quarter. Closes out last quarter honestly, sets 2-3 objectives with 2-3 KRs each. Force-ranks against capacity. |
| `/office-hours` | Before you build anything new. YC-style stress-test of an idea, feature, or pivot. Produces a design doc, never code. |
| `/todo-management` | Anytime. Add, complete, or move tasks in `Todo.md`. |
| `/transcript-processing` | Whenever you have a transcript (Granola, Otter, Fathom, etc.). Creates a structured note, updates People/, extracts action items. |
| `/update-wiki` | Monthly, or when big things change. Refreshes the agent-readable synthesis layer in `Wiki/`. |
| `/prd` | When you need to spec a feature, side project, or build. 6-section framework. Saves to `Projects/` or `Notes/`. |
| `/humanizer` | Before publishing anything written by AI. Strips 29 AI-tells: filler phrases, em dash overuse, promotional language, rule of three, etc. |
| `/link-sweep` | Periodic vault maintenance. Audits red wikilinks, broken frontmatter, orphans. Fixes the mechanical, flags the judgement calls. |
| `/write-skill` | When a workflow gets repeated 3+ times. Codify it as a new skill. |

## Why this and not PARA or Zettelkasten

Frameworks tell you how to file things. They don't change what you do on Tuesday.

The shift happened for me when I stopped treating my vault like a filing system and started treating it like a standing appointment with a coach. Same routine every day. Same hard questions. A record I can actually use on Friday when I'm deciding what matters next week.

The Wiki folder makes your vault legible to other AI agents (chief-of-staff tools, custom GPTs, whatever you layer on). The daily files build the record that makes Friday's review honest.

## Requirements

- [Obsidian](https://obsidian.md) (or any markdown editor, but Obsidian's the easiest)
- An LLM tool with file access. Tested with [Claude Code](https://claude.com/claude-code), [Codex CLI](https://github.com/openai/codex), and [Cursor](https://cursor.com).

That's it.

## Install

```bash
git clone https://github.com/jmchalayer/founder-second-brain.git my-vault
cd my-vault
```

1. Open the folder in Obsidian (`Open folder as vault`).
2. Open the same folder in Claude Code (or Codex / Cursor).
3. Run `/onboard` in your AI tool.
4. Answer the interview questions (takes about 15 minutes).
5. You're set.

## Obsidian setup

After cloning, configure these in Obsidian:

- **Daily notes plugin:** enable it. Set the folder to `Journal/`. Set the date format to `YYYY-MM-DD-daily`.
- **Templates plugin:** enable it. Point it at the `Templates/` folder.
- **File explorer:** put `Soul.md`, `Todo.md`, and the active OKR file in pinned tabs. You'll reference them constantly.

## Optional: comms integration

The skills detect MCP tools at runtime and extend automatically when they're connected. Without any of these, the skills still work, they just ask you to describe things in words.

**Calendar** (used by `/morning-planning`, `/weekly-planning`, `/daily-briefing`)
- Connect a Google Calendar MCP server. Morning plans factor in meetings and free blocks. Weekly planning sees next week's load before you commit. The daily briefing surfaces today's schedule alongside the inbox.
- Recommended: [gcal-mcp](https://github.com/nspady/google-calendar-mcp) or any MCP server that exposes `gcal_list_events` or similar.

**Email** (required by `/daily-briefing`)
- Connect a Gmail MCP server. The briefing pulls inbox state, verifies dropped balls against sent mail, and detects deadlines.
- Without an email MCP, `/daily-briefing` won't run - it refuses to fake the inbox from vault content alone. The other skills are unaffected.

**Other personal comms** (optional, used by `/daily-briefing`)
- If you connect a Slack MCP, WhatsApp MCP, or any other personal-comms MCP, `/daily-briefing` extends to those channels: unread DMs, mentions, threads where you owe a reply. Treated as additional input streams that feed the same buckets (Must Reply Today, dropped balls, etc.).
- Skip any channels you don't use. The briefing scopes to whatever is actually connected.

Install per each MCP server's instructions, then the skills detect the tools automatically.

## Vault structure

```
founder-second-brain/
├── Soul.md              # Identity, values, voice. Written by /onboard.
├── Todo.md              # Single capture point for open tasks.
├── CLAUDE.md            # Instructions for Claude. The map.
├── AGENTS.md            # Same content, mirror for non-Claude agents.
├── Goals/               # Quarterly OKR files (one with status: active)
├── Journal/             # Daily entries + weekly plans
├── Projects/            # One note per active project
├── People/              # One note per person
├── Notes/               # Meeting notes and general notes
├── Wiki/                # Agent-readable synthesis layer
├── Templates/           # Templates referenced by skills
├── Logs/                # Session summaries
└── .claude/skills/      # The 15 built-in skills
```

## The loop

```
Quarterly:  /okr-planning             ->  close out last quarter, set next 90 days
Morning:    /daily-briefing           ->  inbox + calendar, dropped balls, top 3 moves
            /morning-planning         ->  reads Todo.md + OKRs + briefing, creates daily file
During day: /todo-management          ->  capture tasks as they come up
            /transcript-processing    ->  paste transcripts, get structured notes
            /office-hours             ->  stress-test an idea before you build
Evening:    /evening-reflection       ->  closes tasks, captures mood + learnings
Friday PM:  /weekly-planning          ->  review week, plan next week
Sunday PM:  /weekly-sweep             ->  detect vault drift, approve fixes
Monthly:    /update-wiki              ->  refresh the agent-readable layer
            /link-sweep               ->  fix red links, broken frontmatter
Anytime:    /write-skill              ->  codify a workflow you do often
```

## Writing style

The skills are opinionated about voice. They enforce:

- Short paragraphs (2-3 lines)
- Direct, warm, conversational tone
- Specific over generic
- No em dashes
- No corporate jargon or motivational fluff
- First person when writing for you

If you hate this style, you can override it during `/onboard` when it asks about your writing voice. Your answers get baked into your CLAUDE.md.

## Customising

Everything in `.claude/skills/*/SKILL.md` is plain markdown. Edit it. Change the questions, tweak the tone, add your own steps.

Common customisations:

- **Adjust the OKR scope.** The `/onboard` skill defaults to max 3 objectives x 3 KRs. Edit `onboard/SKILL.md` if you want more or fewer.
- **Change the daily template.** `Templates/Daily Planner.md` controls what the morning planning skill writes. Add a gratitude section, habit tracker, whatever you want.
- **Add skills.** Run `/write-skill` to scaffold one. Or drop a new folder in `.claude/skills/` with a `SKILL.md` file. Claude Code picks it up automatically.

## Companion: company brain

Once you've got the personal one running, the same architecture works at the team level. See [company-second-brain](https://github.com/jmchalayer/company-second-brain) for the team starter (brand voice, customer interviews, support FAQs, content briefs, all sharable).

## What's deliberately not here

- **Fyxer / automated email processing** - too specific, varies by tool.
- **Integrations (calendar, Notion, Linear)** - out of scope for v1. Keep the template stack simple.
- **Persistent agent memory** - handled by whatever chief-of-staff agent you layer on top.
- **Content publishing** - this is the input layer. Publishing belongs in a separate system.

## Contributing

Found a bug or have a better prompt? PRs welcome. Keep it opinionated.

## Licence

MIT. Do whatever you want with it.

## Credits

Built on Andrej Karpathy's LLM Wiki pattern for the agent-readable layer. The rest is the routine I wish someone had given me three years ago.

---

Built by JM Chalayer, founder of [JENA](https://jena.so).

Want help adapting this to your own workflow, team, or training programme? Find me on [LinkedIn](https://www.linkedin.com/in/jmchalayer/) or [Instagram](https://www.instagram.com/jmchalayer/).
