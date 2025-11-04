# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository uses [hashcards](https://github.com/eudoxia0/hashcards), a plain text-based spaced repetition system. Flashcards are stored as markdown files, and an SQLite database (`hashcards.db`) tracks review progress and scheduling.

## Flashcard Format

Cards are stored in markdown files at the repository root. Each file becomes a "deck" (the filename without extension is the deck name).

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
- Custom macros can be defined in `macros.tex` at the repository root

### Images
Use standard markdown image syntax: `![alt](images/diagram.png)`

Image paths are relative to the repository root, not the individual markdown file.

## File Organization

- **Deck files**: Markdown files in the decks directory (e.g., `Geography.md`, `Birthdays.md`)
- **Database**: `hashcards.db` stores card performance data and review scheduling
- **Macros**: Optional `macros.tex` for LaTeX definitions
- **Images**: Store in an `images/` directory at the root

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
