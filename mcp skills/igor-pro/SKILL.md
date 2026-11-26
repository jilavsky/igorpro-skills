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
| Writing or fixing any `Function` - operations vs functions, flags, control flow, strings, math traps | `references/syntax.md` |
| Graphs - `Display`, `AppendToGraph`, `ModifyGraph`, `Label`, `SetAxis`, axes, traces, error bars, legends, images | `references/graphs.md` |
| `NewPanel` and controls (Button, SetVariable, ListBox, TitleBox, ...) | `references/panel.md` |
| Python inside Igor (`igorpro` module, `Python`, `PythonFile`, NumPy <-> wave) | `references/python.md` |
| Anything that changed in Igor 10, or code that worked in Igor 8/9 but fails or differs | `references/10-changes.md` |
| Checking a command's name, flags, or output variables | `Igor__get_help`, or `read_file` `references/manual/commands/<name-lowercase>.md`; to find a name, `references/commands/index.md` |
| A topic not covered above (curve fitting, image processing, tables, notebooks, HDF5, data import, ...) | `search_text` in `references/manual/` (full Igor Pro 10 manual, Markdown) and read the matching section |

Writing any new Igor function that touches waves or data folders: read `references/wave-dfref.md`
first - that is where generated code most often goes wrong.

## Working rules (Igor tools)

- Operations (`Display`, `Make`, `Label`...) -> `Igor__execute_command`. Functions with a return
  value -> `Igor__call_function`. Do not wrap commands in `Execute`.
- After creating or editing a graph or panel, verify it with `Igor__capture_window`.
- After editing a procedure file, run `Igor__compile_procedures` and fix errors before
  reporting success.
- Unsure of an operation's flags, or a built-in returns a runtime error: `Igor__get_help` or the
  local page `references/manual/commands/<name-lowercase>.md` first - do not guess repeatedly.
- Use `Make/O` and a named window (`Display/N=name`) so commands can be re-run safely.
- Inside user functions always declare `WAVE`/`NVAR`/`SVAR` references.
- Igor identifiers are case-insensitive; MatrixOP cannot use p, q, r, s point addressing.

## Must-know Igor syntax (read even if you read nothing else)

- **Graph axes are named by position: `left`, `bottom`, `right`, `top`** (or a free-axis name).
  There is no `x` or `y` axis: `Label/W=G1 bottom "Q"`, `ModifyGraph/W=G1 log(left)=1`,
  `SetAxis/W=G1 bottom 0.001,0.5`. Check with `AxisList("G1")`.
- XY plot: `Display/N=G1/K=1 yW vs xW` (Y first, then `vs` X). Trace name = Y wave name.
- `ModifyGraph keyword(name)=value`; without `(name)` it applies to all traces/axes. Always add
  `/W=graphName` in code.
- Operations (`Make`, `WaveStats`, `CurveFit` ...) have no parentheses and cannot be used in an
  expression; results come back in `V_`/`S_`/`W_` outputs (`WaveStats/Q w; Variable m = V_avg`).
- Flag values that are variables/expressions need parentheses: `Make/O/D/N=(n) w`.
- `Make` defaults to single precision - use `/D`.
- In `w = ...` assignments `x` is the destination wave's own scaling, not an X wave; for XY data
  index the X wave: `yW = f(xW[p])`.
- `log` is base 10 (`ln` is natural); modulo is `mod(a,b)`; NaN test is `numtype(v)==2`;
  string compare is `CmpStr(a,b)==0`; `num2str` keeps 5 digits (use `num2str(v,"%.15g")`).
- Blocks end with keywords: `endif`, `endfor`, `while(...)`, `endswitch`, `End` - no braces.
