---
name: unslop
description: Cut AI tells from writing. Use when the user wants text to sound less like AI, or asks to edit, clean up, or humanize a draft.
argument-hint: "File path, or the text to edit (defaults to your last draft)"
---

Edit the target text to remove AI patterns. Preserve meaning, facts, and the intended tone.

## Target

Resolve the target from the arguments, in this order:

1. A file path: edit the file in place with the Edit tool, one pattern fix at a time, so the diff stays reviewable.
2. Pasted text: return the rewritten text.
3. No arguments: take your most recent draft in this conversation and return the rewrite.

Leave code blocks, inline code, identifiers, quoted material, URLs, and frontmatter untouched. In source files, edit only comments and docstrings. When the text is not in English, apply the equivalent patterns in its language.

## Process

1. Read the whole target before changing anything, so the tone is clear.
2. Scan for every pattern below and rewrite each hit.
3. Re-read the result for patterns that the rewrite introduced.

Report in two lines: the number of edits, and the patterns that fired most. Add nothing else, since the rewrite is the deliverable.

Done when a second scan finds no hits and every claim in the original survives in the rewrite.

## Patterns

### Content

- **Superficial -ing phrases.** "highlighting...", "ensuring...", "reflecting...", "showcasing...", "fostering...". Delete, or expand with real sources.
- **Vague attributions.** "Experts believe", "Industry reports suggest", "Some critics argue". Name the source or delete.

### Language

- **AI vocabulary.** Additionally, crucial, delve, enduring, enhance, fostering, garner, interplay, intricate, landscape (abstract), pivotal, showcase, tapestry (abstract), testament, underscore, vibrant. Replace with plain words.
- **Fancy ways to say "is".** "serves as", "stands as", "boasts", "features". Say "is" or "has".
- **"Not just X, but Y."** State the point directly.
- **Rule of three.** Use the natural number of items instead of forcing groups of three.
- **Synonym cycling.** Protagonist, main character, central figure, and hero in one paragraph. Pick one term and repeat it.
- **False ranges.** "from X to Y" where X and Y are not on a meaningful scale. List the topics directly.

### Style

- **Em dashes.** Use periods or commas only. Use no parentheses, en dashes, or hyphen-as-dash substitutes. If a thought needs separation, end the sentence or use a comma.
- **Colons.** Keep them before a list or example. As a mid-sentence connector they add nothing: "If you're coming from traditional automation: instead of registering event handlers, you describe conditions" becomes "Describing when the scheduler should fire works best as plain English."
- **Boldface.** Reserve it for terms the reader must find again. Leave proper nouns and acronyms plain.
- **Inline-header lists.** A bold label plus colon that restates the line ("**Performance:** Performance improved...") becomes prose. A bold lead-in that ends in a period, names the item, and is followed by new detail ("**Schema in TypeScript.** Tables live in one file.") stays.
- **Title case headings.** Use sentence case.
- **Decorative emojis.** Remove them from headings and bullets.
- **Curly quotes.** Use straight quotes.

### Communication artifacts

- **Chatbot phrases.** "I hope this helps!", "Let me know if...", "Of course!", "Certainly!", "Found the smoking gun!". Remove.
- **Sycophantic tone.** "Great question! You're absolutely right!". Respond directly.

### Filler

- **Filler phrases.** "In order to" becomes "To". "Due to the fact that" becomes "Because". Delete "It is important to note that".
- **Excessive hedging.** "could potentially possibly be argued that it might" becomes "may".
- **Generic conclusions.** "The future looks bright." State specific plans or facts.

### Jargon

- **Abstract metaphor nouns.** Substrate (base), wedge or wedge in (add), vector (way, method), locus, vantage, nexus, primitive as a noun, harness as a metaphor, surface as in "API surface", bedrock, scaffolding as a metaphor, modality, paradigm, gold-plating (more than the job needs), ratchet as a metaphor (the mechanism's real name, or a limit that only tightens), evacuate for moving code (move out), endgame (the last phase), north star, flywheel. Use the concrete word.

### Plain speech

- **Mechanism over mood.** "the database stays close at hand", "SQL you can read", and "types that follow your schema" name a feeling. Name the mechanism or a number: "`.toSQL()` returns the exact string sent to the database", "a column rename fails the build". Ask what the sentence tells the reader to do or know, then write that. If it cannot be restated as a concrete instruction, fact, or number, cut it. A sentence that could appear unchanged in another project's docs says nothing about this one, so cut it.
- **Short sentences.** When the reader has to backtrack to parse a sentence, split it in two or drop clauses. One idea per sentence.
- **Active voice.** Catch "is/are/was/were + past participle" and name the actor: "queries are validated" becomes "the compiler validates queries". Passive stays only when the actor is unknown or irrelevant.
- **Strong verbs over adverbs.** "runs quickly" becomes "is fast" or the number. "significantly improves" becomes the measured delta. An adverb propping up a weak verb means the verb is wrong.
- **Plain words.** "utilize" and "leverage" become "use", "facilitate" becomes "help", "numerous" becomes "many", "in the event that" becomes "if".
- **Literal over mannered.** Replace flourish where a literal phrase exists: aphorisms ("wire it or delete it"), rhetorical fragments for effect, personified code ("the plan holds it"), figurative verbs ("rides along", "stands on"), stock framing phrases. "A dial worth turning" becomes "a parameter worth varying".
- **Whole sentences.** Restore dropped articles, verbless fragments, symbol-speak, and abbreviations that make the reader decode. "Parser rejects bad date → exit 2, no write" becomes "The parser rejects a bad date, exits with code 2, and writes nothing." Spell out arrows and abbreviations.
