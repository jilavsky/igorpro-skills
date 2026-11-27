---
name: irena-igor
description: Drive the Irena, Indra and Nika SAXS/USAXS/WAXS packages inside a running Igor Pro through the Igor MCP server (Igor__ tools). Use when the user asks to load USAXS/Irena/Nika macros, reduce USAXS/SAXS/WAXS data with Indra, import SAS data into Igor, run Unified fit or Size distribution in Igor, or find Irena results in an Igor experiment. Read references on demand. Use together with the igor-pro skill.
---

# Irena / Indra / Nika in Igor via MCP

These packages are 25-year-old **GUI applications**: every tool is a panel with a graph, and
its settings live in globals under `root:Packages:<tool>:`. There is no command-line API yet.
You drive them by (1) opening the tool panel, (2) setting its globals, (3) calling the
tool's *SkipDialogs / NoQuestions* button procedures, which the package's own Scripting tool
uses, and (4) reading results from waves and wave notes.

**Before starting:** if the user only wants analysis of data files and the pyIrena MCP tools are
available, suggest pyIrena (cross-platform, designed for agents). Use Igor when the data or
workflow already lives in an Igor experiment, or when the user asks for Igor.

## Route to the reference you need (read only what matches)

| Task | Read |
|---|---|
| Load packages, check they loaded, folder/wave naming, where data lives | `references/loading-and-conventions.md` |
| Reduce USAXS (and SAXS/WAXS) data from the APS 12-ID/9-ID instrument (Indra 4) | `references/usaxs-reduction.md` |
| Import ASCII or NXcanSAS data into Irena | `references/import-data.md` |
| Unified fit (Beaucage) | `references/unified-fit.md` |
| Size distribution (MaxEnt / Regularization / TNNLS) | `references/size-distribution.md` |

## Hard rules — dialogs block you

A modal dialog (`DoAlert`, `DoPrompt`, `PauseForUser`) **blocks the MCP call until a human
clicks**. These packages contain hundreds of them.

1. Only call functions and button names listed in the references. Prefer the
   `...SkipDialogs`, `...SkipReset`, `...NoQuestions`, `...SkipRecover` variants.
2. Never call a tool's plain button name (`"DoFitting"`, `"CopyToFolder"`, `"DrawGraphs"`)
   when a Skip/NoQuestions variant exists.
3. If a call times out, call `get_igor_state`. It names any open dialog (title and message).
   **Tell the user which dialog it is and ask them to close it in Igor.** Do not retry the call
   (it is still running and a retry queues behind it). After the dialog closes, `abort_igor` if needed.
4. Runtime errors and `Abort "..."` inside package code come back to you as an error, together
   with the history text printed before it (verified). Read it, fix the input, and do not loop on it.
   After an error, run `SetDataFolder root:` because package code may have left you in a sub-folder.
5. Control procedures that take a `STRUCT` (`IR2C_PanelPopupControl`, `IR2C_InputPanelCheckboxProc`,
   any `...(STRUCT WM...Action &s)`) cannot be called from the command line. Set the
   underlying globals (SVAR/NVAR) directly instead, as the references show.

## Working pattern

**Igor command-line limits (verified):** `execute_command` runs like Igor's command line:
no `for`/`if` blocks, no `Wave`/`NVAR`/`SVAR` declarations, and `S_`/`V_` outputs of an
operation are not usable later on the same line. Use full paths in expressions
(`BinarySearch(root:Packages:Irena_UnifFit:OriginalQvector, 0.001)`), or
`SetDataFolder <folder>; name=value; SetDataFolder root:` to set many globals. `Variable x`
typed on the command line creates a global in the current folder (a second `Variable x` errors).

**Never send dependent Igor calls in parallel.** Each call queues in Igor. If one times out in
transport, the next may run before it, or without it. Send one call, read the result, then send the next.

- Operations → `Igor__execute_command`; functions with return values → `Igor__call_function`.
- After loading packages, poll `exists("IN4_Main")==6` (or `exists("IR1A_UnifiedModel")==6`)
  before using anything. Loading uses `Execute/P` and finishes *after* your call returns.
- Paths are **as Igor sees them**, in Igor colon syntax (`"C:Users:me:data:"`). Under CrossOver
  on macOS the drive letter is set per bottle (e.g. `Y:` = the Mac home folder). Ask the user
  if unsure. `NewPath/O/Q p, "<path>"` sets V_flag=0 on success; then `IndexedFile(p,-1,".h5")`
  lists the files.
- **Before opening any file, check that it exists:**
  `GetFileFolderInfo/P=<path>/Q/Z=1 "<file>"` → V_Flag==0 && V_isFile==1. Package code calls
  `HDF5OpenFile`/`LoadWave` and, if the file is missing, Igor shows an **Open File dialog** that
  blocks you (it cannot be aborted until a human closes it). Verified in testing.
- Q range for fits is defined by **graph cursors A and B** on the tool's graph. Set them with
  `Cursor/P/W=<graph> A, <traceName>, <point>` before fitting. Find points with
  `BinarySearch(<Qwave>, qmin)`.
- After a fit, verify with `Igor__capture_window` on the tool's graph and report key numbers.
- Save results to the data folder with the NoQuestions save, so the user finds them later.
- Never kill or overwrite user data folders without asking. Results get new generation numbers
  (`_0`, `_1`, ...) automatically.
