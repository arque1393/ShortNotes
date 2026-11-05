---
tags: [meta]
---
# How to Use This Vault

## 1. Open it
Obsidian → *Open folder as vault* → select the unzipped `Graph-Mastery-Vault` folder. Open [[00 - Home]].

## 2. Recommended plugins
| Plugin | Type | Why |
|---|---|---|
| **Dataview** | Community | Powers the progress tables in [[Study Tracker]] |
| **Spaced Repetition** | Community | Turns every `Question::Answer` line into a flashcard |
| **Templater** (optional) | Community | Richer templates; core *Templates* also works |
| **Excalidraw** (optional) | Community | Draw your own architecture diagrams |
| Mermaid + LaTeX | Built-in | Diagrams and math render natively |

Core *Templates* plugin: set template folder to `00-Meta/Templates`.

## 3. Note conventions
- **Frontmatter**: `phase` (0–5), `status` (`not-started` → `learning` → `review` → `mastered`), `tags`.
- **Callouts**: `[!summary]` = core idea, `[!tip]` = practical advice, `[!warning]` = pitfall, `[!question]` = think about it.
- **Self-test** section at the bottom of each note = flashcards. Deck tags look like `#flashcards/graph-ml`.
- Links are `[[wikilinks]]` — use the **Graph view** to see how fields connect.

## 4. Study loop (per concept note)
1. **Read** the note (it is a *scaffold*, not a full textbook).
2. **Go deeper** with the "Resources" listed at the bottom.
3. **Write in your own words** under the "My notes" heading — this is where real learning happens.
4. **Do** the exercise / code snippet.
5. **Review** flashcards daily (Spaced Repetition: `Ctrl/Cmd+P → Review flashcards`).
6. Update `status` in frontmatter.

> [!tip] Rule of thumb
> For each phase: ~60% hands-on, 30% reading, 10% writing summaries. Ship the phase project in [[MOC - Projects]] before moving on.

## 5. Weekly rhythm (15–20 h/week)
- Mon–Thu: 1 concept note/day + exercises (≈2 h/day)
- Fri: project work (3 h)
- Sat: paper reading with [[Template - Paper Note]] (3 h)
- Sun: flashcard review + weekly reflection in [[Study Tracker]] (1 h)
