# Igor Pro built-in commands - lookup

All 1060 Igor Pro 10 operations and functions. **You do not need to read all of this.**
Look up one command at a time. The full Igor Pro 10 manual is stored locally in
`references/manual/` (Markdown, from docs.wavemetrics.com), so no network is needed.

## How to use

1. **Know the command name:** `read_file` `references/manual/commands/<name-lowercase>.md` directly
   (e.g. `references/manual/commands/wavestats.md`). It has syntax, every flag, output `V_`/`S_`
   variables, details and examples. `Igor__get_help` returns the same text if Igor is running.
2. **Know what you want to do, not the name:** `read_file` the letter file below that seems likely,
   or `search_text` a keyword in `references/commands/` - every line has a one-line summary.
3. **Need a topic, not a command** (graph styling, curve fitting, data folders, programming rules):
   `search_text` in `references/manual/` and read the matching chapter section, e.g.
   `references/manual/graphing/graphs.md`, `references/manual/programming/programming.md`,
   `references/manual/analysis/curve-fitting.md`.

A large page (ModifyGraph is ~90 KB) is better searched than read whole: `search_text` the
keyword inside that one file, then read around the hit.

Online URL pattern, if ever needed: `https://docs.wavemetrics.com/igorpro/commands/<name-lowercase>`.

## Problematic Igor rules

- Igor names are case-insensitive for identifiers (variables, waves, functions).
- MatrixOP cannot use p, q, r, s point addressing.
- Graph axes are `left`, `bottom`, `right`, `top` - never `x`/`y`. See `references/graphs.md`.

## Letter files (in this folder)

| Letter | File | Commands |
|---|---|---|
| A | `commands-A.md` | 44 |
| B | `commands-B.md` | 25 |
| C | `commands-C.md` | 73 |
| D | `commands-D.md` | 57 |
| E | `commands-E.md` | 25 |
| F | `commands-F.md` | 52 |
| G | `commands-G.md` | 60 |
| H | `commands-H.md` | 43 |
| I | `commands-I.md` | 63 |
| J | `commands-J.md` | 7 |
| K | `commands-K.md` | 12 |
| L | `commands-L.md` | 29 |
| M | `commands-M.md` | 79 |
| N | `commands-N.md` | 33 |
| O | `commands-O.md` | 6 |
| P | `commands-P.md` | 47 |
| Q | `commands-Q.md` | 3 |
| R | `commands-R.md` | 39 |
| S | `commands-S.md` | 265 |
| T | `commands-T.md` | 38 |
| U | `commands-U.md` | 10 |
| V | `commands-V.md` | 7 |
| W | `commands-W.md` | 32 |
| X | `commands-X.md` | 6 |
| Y | `commands-Y.md` | 1 |
| Z | `commands-Z.md` | 4 |
