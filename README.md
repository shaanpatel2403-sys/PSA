# Spine crosswords

Eight freeform crosswords for neurosurgery and orthopaedic trainees, 154 entries in total.
No word is repeated between puzzles.

| Puzzle | Grid | Entries |
| --- | --- | --- |
| Trials & eponyms | 15×15 | 24 |
| Cervical spine | 15×14 | 23 |
| Lumbar degenerative | 15×15 | 16 |
| Deformity & alignment | 15×15 | 20 |
| Trauma & cord injury | 15×15 | 16 |
| Tumour & infection | 15×15 | 18 |
| Instrumentation | 15×15 | 18 |
| Paediatric & dysraphism | 15×15 | 19 |

Everything lives in `index.html`. No build step, no dependencies, no server-side anything.

## Publish it

Upload the contents of this folder to a repository, then Settings → Pages → Source:
*Deploy from a branch* → Branch `main`, folder `/ (root)`. Live within a minute or two.

As a subfolder of a repository you already publish, it appears at
`https://<user>.github.io/<repo>/spine-crosswords/` with no settings change needed.

`.nojekyll` is a zero-byte file telling Pages to serve the files untouched. Nothing here
actually needs it, so don't worry if it goes missing in transit.

## Playing

Switch puzzle with the tabs. Click a square or a clue to begin, then type.

| Key | Does |
| --- | --- |
| Space | Switch between the across and down word through the current square |
| Tab / Shift-Tab | Next or previous clue |
| Arrow keys | Move freely around the grid |
| Backspace | Delete, then step back |

`Check` marks wrong letters red without erasing them. `Reveal letter` and `Reveal word` fill in
amber, so it stays visible later what was given away. `Show answers` fills the grid and displays
the answer beside each clue; switching back restores whatever had been typed.

The column of bars beside the grid is that puzzle's entries stacked top to bottom, filling as
each is completed.

## Notes

Progress is stored per puzzle in the browser's local storage, so closing the tab loses nothing.
Storage is keyed to the address the file is served from, so a local copy and the published copy
keep separate progress.

Where a square starts both an across and a down word it carries a single number, which therefore
appears in both clue lists. That is standard crossword convention, not a numbering error.

The only external request is the Google Fonts stylesheet for IBM Plex. Offline, the page falls
back to system fonts and nothing else changes; delete the three `<link>` tags in `<head>` to make
it fully self-contained.

Light and dark themes both ship, following the operating system setting.

## Editing or adding puzzles

`PUZZLES` at the top of the `<script>` block is an array, one object per puzzle:

- `id` — the local storage key, so keep it unique
- `name` — the tab label
- `n` — entry count, shown on the tab
- `rows` — strings of equal length; a letter is a filled square, `.` is empty
- `clues` — keyed by the answer word

Grids need not be square or the same size as each other. Numbering, entry detection, clue
ordering, the progress rail and the cell borders are all derived from `rows` when the puzzle
loads, so nothing else needs editing.

Three rules the existing clues all obey, worth keeping if you add more:

1. **No self-giveaway.** The answer, or a stem of it, must not appear inside any word of its own
   clue. `DISCITIS` cannot be clued with "spreading into the disc".
2. **No naming a neighbour.** A clue must not contain another answer from the same grid, unless
   it does so through an explicit numbered reference such as "the route named at 6 Across".
3. **No acronym expansion.** For an acronym answer, the initials of the clue's words must not
   spell it. `SINS` cannot be clued "Spinal Instability Neoplastic Score".

Every word readable in `rows` — in either direction — must have a key in `clues`, including any
word formed accidentally by two crossing entries.
