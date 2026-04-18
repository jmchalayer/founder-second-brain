---
name: update-wiki
description: "Update the Wiki/ folder in the founder's second brain vault. Use whenever the user says 'update the wiki', 'refresh the wiki', 'wiki update', 'sync the knowledge base', 'refresh the knowledge base', or anything about the agent-readable Wiki layer. Also trigger during weekly planning if the wiki hasn't been updated in 2+ weeks, and when new major information lands (strategy shift, new OKR quarter, new key person, major project launch). The Wiki/ folder is a synthesis layer - raw vault sources get distilled into 15-20 structured pages any external AI agent can parse quickly."
---

# Update Wiki

You maintain the `Wiki/` knowledge base in the founder's vault. This folder is an agent-readable synthesis layer following the Karpathy LLM Wiki pattern: raw sources (the vault) get distilled into structured wiki pages that any AI agent can parse quickly.

The wiki exists so external agents don't have to read 200+ vault files. They read `Wiki/` and get the full picture in 15-20 files.

## The golden rule

**Show the user your plan before making any changes. Always.**

## Step 1: Understand current state

Read these to see what the wiki currently contains and when it was last updated:

1. `Wiki/SCHEMA.md` (structure and rules, if it exists)
2. `Wiki/index.md` (master catalog)
3. `Wiki/log.md` (last update date and history)

If the Wiki/ folder is empty or those files don't exist, this is a first-time wiki build. Tell the user that and offer to scaffold it. First-time build creates `SCHEMA.md`, `index.md`, `log.md`, and a starter set of pages based on what's in the vault.

Note the date of the last update. Everything after that date is what you're looking for.

## Step 2: Read vault sources

Focus on what might have changed since the last wiki update.

**Always read:**
- `Soul.md` (identity, may have been updated)
- `Goals/` - find the file with `status: active` (current OKR file)
- `Projects/` - all `.md` files
- `People/` - all `.md` files

**Read recent:**
- `Journal/` - most recent 2 weekly plans and last 14 days of daily files (for themes, not detail)
- `Notes/` - files modified after the last wiki update

**How to find recent changes:** file modification dates and filenames (they start with YYYY-MM-DD). Anything dated after the last wiki update in `log.md` is a candidate.

## Step 3: Identify changes

Compare vault sources against current wiki pages. Look for:

- **New information** not yet in the wiki (new strategy decisions, new people, new projects)
- **Changed information** that makes pages out of date (OKR progress, pricing, positioning)
- **New pages needed** (a significant new concept, person, or project that deserves its own page)
- **Stale information** that's no longer true

Don't flag trivial changes. Focus on things that would matter to an external agent reading the wiki cold.

## Step 4: Present the plan

Use this format:

```
## Wiki Update: [date]

### Changes since last update ([last update date]):

**New/changed sources:**
- [list of vault files with new content]

**Wiki pages to update:**
- `context/current-okrs.md` - [what changed and why]
- `business/strategy.md` - [what changed and why]

**New pages to create:**
- `business/[name].md` - [why this deserves its own page]

**Pages to archive (no longer relevant):**
- `...`

Anything you want me to add, skip, or change?
```

Wait for confirmation. They might want to add, skip, or redirect.

## Step 5: Execute updates

After confirmation:

1. **Update affected pages.** For each:
   - Read current page
   - Update with new information
   - Update `last_updated` in frontmatter to today
   - Update `sources` in frontmatter if new sources were used
   - Keep writing factual, structured, agent-optimised. No prose, no fluff.

2. **Create new pages** if needed. Every new page has:

```yaml
---
type: wiki
domain: [identity|business|context|framework]
sources: [list of vault files]
related: [[[wiki-page-1]], [[wiki-page-2]]]
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
---
```

**Cross-linking rules:**

- **Always use full paths** in wiki links: `[[business/overview]]`, not `[[overview]]`. Wiki pages live in subdirectories and name collisions are possible (e.g. both `Projects/Product.md` and `Wiki/business/product.md` could exist).
- **Use the alias syntax for readable prose:** `[[business/overview|DentaScribe]]` renders as "DentaScribe" while still linking. Prefer this when the page path looks technical and the text should read naturally.
- **Do not link to source files under `Projects/` or `People/`.** Wiki pages synthesize; they don't point back at raw sources. The `sources` frontmatter field tracks what fed into the page, not the body prose.
- **The `related` frontmatter** lists 2-4 of the most closely connected wiki pages. Body prose should inline-link naturally beyond that.

Examples:
- `business/strategy.md` links to `[[context/current-okrs]]` when discussing goals
- `business/overview.md` links to `[[business/product|the product]]` and `[[business/strategy|the strategy]]` using aliases
- `context/key-people.md` links to `[[identity/profile|the founder]]` and to other wiki pages about those people (if any exist), not to `People/[Name].md` source files

External agents use these links to navigate the synthesis layer.

3. **Update `index.md`** if pages were added, removed, or renamed. One line per entry: markdown link + short description.

4. **Append to `log.md`:**

```markdown
## [YYYY-MM-DD] update-type | Short description

**Trigger:** [user request / weekly planning / first build]

**Pages updated:**
- page-name.md (what changed)

**Pages created:**
- page-name.md (why)

**Sources read:**
- [list of vault files]

**Notes:** [anything worth noting]
```

## First-time wiki build

If the wiki is empty, scaffold this structure:

```
Wiki/
├── SCHEMA.md              # Rules for agents (the only file the user maintains manually)
├── index.md               # Master catalog
├── log.md                 # Update history
├── identity/
│   ├── profile.md         # Who they are, what they're building
│   └── communication.md   # Writing style, voice
├── business/
│   ├── overview.md        # Company/project summary
│   ├── product.md         # What the product is
│   └── strategy.md        # Current strategic direction
├── context/
│   ├── current-okrs.md    # This quarter's objectives
│   ├── active-projects.md # What's in flight
│   └── key-people.md      # Who matters right now
└── frameworks/
    └── decision-log.md    # Significant decisions and rationale
```

Generate `SCHEMA.md` using the template below. **Substitute `[OWNER_NAME]` with the owner's actual name from `Soul.md` frontmatter's `owner` field.** Do not leave the placeholder literal in the final file.

```markdown
---
type: wiki-schema
---

# Wiki Schema

This folder is an agent-readable synthesis layer. External AI agents read these pages to understand [OWNER_NAME]'s context without reading the full vault.

## Rules

- **Factual, not narrative.** Write for agent consumption. No marketing fluff.
- **Structured.** Use headings, bullet points, tables. Make it scannable.
- **Domain-organised.** Identity, business, context, frameworks.
- **Sources tracked.** Every page's frontmatter lists its source files.
- **Last-updated tracked.** Stale pages should be visible.
- **No private content.** Therapy, relationship details, family matters stay out of the wiki.

## Domains

- `identity/` - Who the owner is. Rarely changes.
- `business/` - The company/project. Changes with strategy.
- `context/` - Current state. Changes quarterly.
- `frameworks/` - Reusable thinking tools.
```

Populate the other pages from vault sources. For a first build, keep each page short and honest. It's a skeleton to iterate on, not a finished artefact.

## What to never do

- **Never modify `SCHEMA.md` after first creation.** The user owns that file.
- **Never include personal/private content.** Therapy, relationships, family matters. The wiki is for professional/business context.
- **Never delete wiki pages.** If something becomes irrelevant, add `## Archived` at the bottom with a date. Keep it in the index marked archived.
- **Never make changes without showing the plan first.** Step 4 is not optional.

## What belongs in the wiki vs what doesn't

**Include (durable knowledge):**
- Identity, values, communication style
- Product, pricing, strategy, customers
- Current OKRs and active projects
- Key people
- Strategic decisions and rationale
- Frameworks

**Exclude (temporal or private):**
- Daily journal entries
- Raw meeting notes or transcripts
- Inbox items
- Session logs
- Personal/private details

## Tone

Write wiki content for agent consumption: factual, structured, scannable. No marketing, no motivational fluff. An agent reading `business/product.md` should get the full picture in 30 seconds, not a narrative about the journey.
