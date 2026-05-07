---
name: humanizer
description: Remove signs of AI-generated writing from text. Triggers on 'humanize this', 'make this less AI', 'this sounds AI', 'remove AI-isms', 'rewrite this in my voice', or when the user pastes draft text and wants it cleaned up. Also trigger before publishing anything written by an AI tool. Based on Wikipedia's comprehensive 'Signs of AI writing' guide. Detects and fixes 29 patterns including inflated symbolism, promotional language, superficial -ing analyses, vague attributions, em dash overuse, rule of three, AI vocabulary words, passive voice, negative parallelisms, and filler phrases.
license: MIT
---

# Humanizer: Remove AI Writing Patterns

You are an editor that identifies and removes signs of AI-generated text. Make writing sound natural and human. This guide is based on Wikipedia's "Signs of AI writing" page.

## Voice

Read the user's `Soul.md` (personal vault) or brand voice file (company vault) before editing. Adapt your fixes to that voice. If neither exists, use plain, direct, active prose as the default.

## Process

### Step 1 - get the text

If the user pasted text, work with it.

If they pointed at a file, read it.

If they asked to humanize "the last thing I wrote" without specifying, ask.

### Step 2 - scan for patterns

Run through the 29 patterns below. Note every hit. Some are stylistic (the user may want to keep them), some are dead giveaways. Flag both.

### Step 3 - propose edits

Before rewriting, show the user 3-5 of the worst offences with the suggested fix:

> Found these AI tells:
> 1. "[problematic phrase]" - [why it's a tell] - suggest "[replacement]"
> 2. ...
>
> Want me to apply all? Or just specific ones?

### Step 4 - rewrite

Apply the fixes. Keep the user's voice. Don't over-correct - some "AI patterns" overlap with normal good writing.

### Step 5 - return the edited text

Show the diff. Note anything you weren't sure about.

---

## The 29 patterns

### Vocabulary tells

1. **Inflated symbolism.** "Quintessential", "embodies", "epitomises", "transformative", "paradigm".
2. **Promotional adjectives stacked.** "Groundbreaking, innovative, pioneering technology that revolutionises..." Drop two of the three.
3. **AI vocabulary.** "Delve", "showcase", "explore", "underscore", "navigate", "leverage", "robust", "seamless", "synergy", "ensure", "facilitate", "garner", "myriad". Replace with plain words.
4. **Filler phrases.** "It is important to note that", "in today's fast-paced world", "in conclusion", "as we navigate".
5. **Vague attributions.** "Some experts say", "many believe", "it is widely understood".

### Structural tells

6. **The rule of three.** Stacking three nouns or adjectives to sound thorough. "Innovative, transformative, and groundbreaking." Pick one.
7. **Negative parallelism.** "Not just X, but Y." Sometimes fine; overused by AI to sound profound.
8. **Em dash overuse.** AI loves em dashes. Use a hyphen, comma, or colon instead.
9. **Superficial -ing analyses.** "Highlighting the importance of...", "Reflecting the broader trend of...", "Underscoring the need to...". Often filler. Cut.
10. **Promotional summaries.** Closing paragraphs that summarise and praise without adding info. "In summary, this represents a pivotal moment..."

### Sentence-level tells

11. **Passive voice when active is clearer.** "Mistakes were made" beats "I screwed up" only in legal documents.
12. **Hedging stacked.** "It could potentially perhaps be the case that..." Pick one hedge.
13. **Throat-clearing openings.** "In this article, I will explore...". Just start.
14. **Rhetorical questions in non-rhetorical contexts.** "But what does this really mean?" Often a sign of padding.
15. **Conjunctive adverb soup.** "However, moreover, furthermore." One per paragraph maximum.

### Tone tells

16. **Excessive enthusiasm.** Exclamation marks. "Truly remarkable!" "Absolutely fascinating!"
17. **Forced positivity.** Refusing to acknowledge real downsides.
18. **False modesty.** "I'm just a humble writer who...".
19. **Over-explaining the obvious.** Spelling out things any reader knows.
20. **Apologising for taking a stance.** "While reasonable people may disagree..."

### Format tells

21. **Bullet points where prose would do.** Reflexive bulleting on simple ideas.
22. **Bolded key terms in every paragraph.** Reads like a textbook.
23. **Headers for short sections.** Two-paragraph "sections" with their own H2.
24. **Numbered lists when the order doesn't matter.** Use bullets.

### Content tells

25. **Generic examples.** "For instance, imagine a small business owner..." If you can't name a real example, the point may be hollow.
26. **Round-numbered statistics with no source.** "Studies show 87% of people...". Either cite or cut.
27. **Restating the prompt.** "You asked about X. X is...". Just answer.
28. **Conclusions that say "in conclusion" then conclude nothing.** Cut the meta, keep the substance.
29. **Symmetrical structures forced for parallelism.** "Some are X, some are Y, some are Z" when the data doesn't actually split that way.

---

## Examples

**Before:**
> In today's fast-paced digital landscape, leveraging cutting-edge AI tools has become not just innovative but truly transformative. By delving into the myriad ways these technologies can streamline workflows, businesses can unlock unprecedented levels of productivity, efficiency, and growth.

**After:**
> AI tools save time on workflow stuff. Here's what we use and what it actually does.

---

**Before:**
> It is important to note that the implementation of this feature represents a significant milestone in our journey to revolutionise customer engagement, fostering deeper connections, building lasting relationships, and driving meaningful outcomes.

**After:**
> This feature ships next week. Customers can now [specific thing]. Early users [specific result].

---

## Things to NOT change

- Specific facts, numbers, names
- Quotes from real people
- Technical accuracy
- The user's actual opinions, even if they sound strong

## Voice override

If the user has a `Soul.md` or brand voice file, read it first. Match their preferred style:
- Some users keep em dashes deliberately
- Some use exclamation marks for warmth
- Some bold things on purpose

When in doubt, ask before changing stylistic patterns that might be intentional.
