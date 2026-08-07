# Spine crossword

A 15×15 freeform crossword covering spine surgery trials, pathology, anatomy and eponymous
classifications. Twenty-four entries, aimed at neurosurgery and orthopaedic trainees.

Everything lives in `index.html`. No build step, no dependencies, no server-side anything.

## Publish it

**As a standalone site**

1. Create a new public repository on GitHub.
2. Upload the contents of this folder (`index.html`, `README.md`, `.nojekyll`) to the root.
3. Settings → Pages → Source: *Deploy from a branch* → Branch: `main`, folder: `/ (root)` → Save.
4. Live at `https://<user>.github.io/<repo>/` within a minute or two.

**As a subfolder of a site you already publish**

Drop this whole folder into the existing repository and push. It appears at
`https://<user>.github.io/<repo>/spine-crossword/` — no settings change needed.

`.nojekyll` tells GitHub Pages to serve the files as-is rather than running them through Jekyll.
It is a zero-byte file and is easy to lose when copying between folders; if the page ever 404s
after a push, check that it survived.

## Playing

Click a square or a clue to begin, then type. The cursor advances along the current entry.

| Key | Does |
| --- | --- |
| Space | Switch between the across and down word through the current square |
| Tab / Shift-Tab | Next or previous clue |
| Arrow keys | Move freely around the grid |
| Backspace | Delete, then step back |

`Check` marks wrong letters red without erasing them. `Reveal letter` and `Reveal word` fill in
amber, so it stays visible later what was given away. `Show answers` fills the whole grid and
displays the answer beside each clue; switching back restores whatever had been typed.

The column of bars beside the grid is the twenty-four entries stacked top to bottom, filling in
as each is completed.

## Notes

Progress is written to the browser's local storage, so closing the tab does not lose it. Storage
is keyed to the address the file is served from, which means a locally opened copy and the
published copy keep separate progress, and some browsers restrict storage on `file://` origins
entirely.

The only external request is the Google Fonts stylesheet for IBM Plex. Offline or behind a
restrictive network the page falls back to system fonts and nothing else changes. To make it
genuinely zero-dependency, delete the three `<link>` tags in `<head>`.

Light and dark themes both ship, following the operating system setting.

## Editing the puzzle

Two data structures near the top of the `<script>` block hold everything:

- `ROWS` — fifteen strings of fifteen characters. A letter is a filled square, `.` is empty.
- `CLUES` — an object keyed by the answer word.

Numbering, entry detection, clue ordering, the progress rail and the grid borders are all derived
from `ROWS` at load time, so changing the grid needs no other edits. Every answer in `ROWS` must
have a matching key in `CLUES`.
