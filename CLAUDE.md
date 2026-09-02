# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository uses [hashcards](https://github.com/eudoxia0/hashcards), a plain text-based spaced repetition system. Flashcards are stored as markdown files, and an SQLite database (`decks/hashcards.db`) tracks review progress and scheduling.

## Flashcard Format

Cards are stored in markdown files under the `decks/` directory. Each file becomes a "deck" (the filename without extension is the deck name).

### Question-Answer Cards
```markdown
Q: What is the capital of France?
A: Paris
```

Both questions and answers can span multiple lines for longer content. However,
ideally answers should be three words or fewer.

### Cloze Deletion Cards
```markdown
C: [Paris] is the capital of [France].
```

Cloze cards use square brackets `[...]` to mark the parts that will be hidden during review.

Cloze cards are great for any question that is bidirectional, because you will
be presented to review each hidden section on their own. For this reason any
question that can be written succinctly and clearly using the Cloze style should
be preferred.

### LaTeX Support
- Inline math: `$...$`
- Display math: `$$...$$`
- Custom macros can be defined in `macros.tex` in the collection directory (`decks/`)

### Images
Use standard markdown image syntax: `![alt](images/diagram.png)`

Image paths are relative to the collection directory (`decks/`), not the individual markdown file.

## File Organization

- **Deck files**: Markdown files in the decks directory (e.g., `Geography.md`, `Birthdays.md`)
- **Database**: `decks/hashcards.db` stores card performance data and review scheduling
- **Macros**: Optional `macros.tex` for LaTeX definitions
- **Images**: Store in an `images/` directory inside `decks/`

## Running hashcards

`decks/` is the collection directory. Run every `hashcards` command from inside
it, or pass it as the `DIRECTORY` argument. Running from the repository root
instead silently creates a second, empty `hashcards.db` there.

`hashcards.db` is gitignored and does **not** travel with git. It is copied by
hand between machines. The NAS working copy is the store of record.

Only `drill` writes to the database. `due`, `check`, `stats` and `export` are
read-only.

Do not drill in two places at once. There is no way to merge two diverged
databases: `review_id` and `session_id` are sequential integers, so independent
writers collide. Before copying one database over another, confirm the source is
a strict superset of the destination.

## Working with Cards

### Creating New Cards
1. Add cards to existing deck files, or create a new `.md` file for a new deck
2. Use either Q&A format or cloze format depending on the content
3. Separate cards with blank lines for readability
4. Cards are identified by hashing their content (content-addressable)

### Editing Cards
- Modifying card content creates a new card (due to content hashing)
- The old card's review history becomes orphaned
- Be mindful when editing to preserve learning progress
