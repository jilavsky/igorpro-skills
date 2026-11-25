---
name: igor-pro
description: Everything for Igor Pro 10 work - entry point plus on-demand references. Use whenever the user mentions Igor, Igor Pro, .ipf procedures, waves, data folders, experiments (.pxp), graphs, control panels, or Python inside Igor. Covers - writing or debugging Igor procedure code; WAVE/NVAR/SVAR/DFREF reference syntax, free waves and the $ operator; NewPanel and control layout (Button, SetVariable, CheckBox, PopupMenu, ListBox, TitleBox) in the Irena/Indra style; the igorpro Python module (igorpro.wave, igorpro.folder, igorpro.fn); Igor Pro 10 changes and breaking compile errors; looking up the exact name, flags and URL of any built-in operation or function; and driving a running Igor through the Igor__ tools. References are in {skill_dir}/references and are read on demand.
---

# Igor Pro 10

This skill is a router. Read **only** the reference file(s) that match the task, using `read_file`
on the path shown (relative to this skill's folder). Do not read them all.

| If the task involves... | Read |
|---|---|
| Functions that take/return waves, data folders, NVAR/SVAR, free waves, `$`, DFREF | `references/wave-dfref.md` |
| `NewPanel` and controls (Button, SetVariable, ListBox, TitleBox, ...) | `references/panel.md` |
| Python inside Igor (`igorpro` module, `Python`, `PythonFile`, NumPy <-> wave) | `references/python.md` |
| Anything that changed in Igor 10, or code that worked in Igor 8/9 but fails or differs | `references/10-changes.md` |
| Checking a command's name, flags, or output variables | `Igor__get_help` first; otherwise `references/commands/index.md` |

Writing any new Igor function that touches waves or data folders: read `references/wave-dfref.md`
first - that is where generated code most often goes wrong.

## Working rules (Igor tools)

- Operations (`Display`, `Make`, `Label`...) -> `Igor__execute_command`. Functions with a return
  value -> `Igor__call_function`. Do not wrap commands in `Execute`.
- After creating or editing a graph or panel, verify it with `Igor__capture_window`.
- After editing a procedure file, run `Igor__compile_procedures` and fix errors before
  reporting success.
- Unsure of an operation's flags, or a built-in returns a runtime error: `Igor__get_help` first,
  do not guess repeatedly.
- Use `Make/O` and a named window (`Display/N=name`) so commands can be re-run safely.
- Inside user functions always declare `WAVE`/`NVAR`/`SVAR` references.
- Igor identifiers are case-insensitive; MatrixOP cannot use p, q, r, s point addressing.
