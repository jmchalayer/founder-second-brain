---
name: link-sweep
description: Audit and fix link hygiene across the vault. Detects red (unresolved) wikilinks, broken YAML frontmatter, missing aliases, and orphan files. Triggers on 'link sweep', 'fix red links', 'audit links', 'check vault links', 'clean up wikilinks', or 'link hygiene'. Run periodically as vault maintenance.
---

# Link Sweep

You audit and fix link hygiene across the vault. Goals: zero red (unresolved) wikilinks, valid YAML frontmatter, working aliases, no accidental orphans.

## The golden rule

Show the user what you plan to change before making any changes. Always pause for confirmation between phases. Format-fixing is mechanical; deciding whether a link should resolve to file A or file B is a judgement call. Propose, don't apply, until you have approval.

## What to detect

### Critical (always fix)
- **Red wikilinks** - `[[Some Note]]` where `Some Note.md` doesn't exist anywhere in the vault
- **Broken YAML** - frontmatter that doesn't parse (missing `---`, wrong indentation, mismatched quotes)
- **Duplicate file names** - two files with the same name in different folders (creates ambiguous wikilinks)

### Worth flagging (propose, don't fix)
- **Orphan files** - files that have no incoming links from anywhere
- **Missing aliases** - files with names like "John Smith.md" that should also alias "John" or "Smith"
- **Stale dates** - frontmatter `last_updated` more than 6 months old on files that should be living docs
- **Mismatched casing** - `[[apple]]` and `[[Apple]]` referring to the same thing inconsistently

## Process

### Step 1 - identify the vault

Read `CLAUDE.md` (or `AGENTS.md`) at the vault root to understand structure and conventions. Note any rules about wikilink targets (e.g. "people are linked as `[[Name]]`", "projects as `[[Project Name]]`").

### Step 2 - scan

Build an index of:
- All `.md` files (paths)
- All wikilinks `[[...]]` (sources and targets)
- All frontmatter (parsed)
- Aliases declared in frontmatter

### Step 3 - report

Print a summary before any fixes:

```
Found:
- [N] red wikilinks (will fix)
- [N] broken YAML files (will fix)
- [N] duplicate file names (need your input)
- [N] orphan files (worth reviewing)
- [N] aliases missing (proposed, not applied)
- [N] stale dates (flagged, not fixed)

Proceed with critical fixes, then review the rest?
```

### Step 4 - fix critical issues

For each red wikilink:
1. Check if target exists with different casing or punctuation
2. Check if a similar file exists (fuzzy match)
3. Propose: "rename target", "fix link", or "create stub file"
4. Apply only after confirmation

For each broken YAML:
1. Show the broken file
2. Show the proposed fix
3. Apply after confirmation

### Step 5 - review judgement calls

For duplicates, orphans, aliases:
- Show one at a time
- Suggest a fix or option
- Apply on user input

### Step 6 - report

End with:
```
Fixed:
- [N] red wikilinks
- [N] YAML errors
- [N] duplicates resolved

Skipped (your call):
- [N] orphans (listed in Logs/)
- [N] alias suggestions (listed in Logs/)

Suggest running again in [N] weeks.
```

Save the full audit log to `Logs/YYYY-MM-DD-link-sweep.md` so the user has a record.

## Vault-specific notes

The vault's `CLAUDE.md` may have specific rules. Common ones:

- Personal vaults often have `[[Person Name]]` for people, `[[Project Name]]` for projects
- Company vaults often have wikilinks to wiki pages: `[[Wiki/customers/voice-of-customer]]`
- Some vaults use aliases extensively for short references

Read `CLAUDE.md` first, follow its conventions.

## Things to be careful about

- **Don't auto-create stub files** without asking. The user might have meant to delete the broken link, not fill it in.
- **Don't move files** to fix duplicates. Renames break external bookmarks. Always confirm.
- **Don't rewrite frontmatter wholesale** if just one field is broken. Surgical fixes only.
- **Don't touch `Logs/` or `Archive/`** unless explicitly asked. Old session logs often have intentional broken links to deprecated state.

## Voice

Direct. Show the user the data before acting. Treat the vault as their territory; you're maintenance, not redesign.
