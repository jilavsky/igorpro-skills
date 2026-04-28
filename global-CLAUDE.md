# Global Claude Code Instructions — Jan Ilavsky

## Identity and context
I am a scientist at Argonne National Laboratory working on small-angle X-ray
scattering (SAXS/USAXS). My primary programming language for data analysis
is Igor Pro 10 (64-bit only). I also work in Python for pipeline/automation.
I use macOS and Windows.

## Igor Pro — always apply these rules

### Version and environment
- Igor Pro 10, 64-bit only. Never suggest 32-bit XOP patterns.
- Target `#pragma IgorVersion=9.04` or higher unless told otherwise.
- Always include at the top of new .ipf files:
  ```igor
  #pragma TextEncoding = "UTF-8"
  #pragma rtGlobals=3
  #pragma DefaultTab={3,20,4}
  #pragma IgorVersion=9.04
  ```

### Wave and data folder references — critical rules
- NEVER use a wave name directly inside a function without a WAVE declaration.
- ALWAYS use `WAVE/Z` when a wave may not exist, then check `WaveExists()`.
- ALWAYS save and restore the current data folder: `DFREF saveDF = GetDataFolderDFR()` ... `SetDataFolder saveDF`.
- NEVER build a path mid-expression: build the full string first, then apply `$` once.
  - WRONG: `WAVE w = root:myData:$name`
  - CORRECT: `WAVE w = $("root:myData:" + name)` or `WAVE w = dfr:$name`
- Use `DFREF` parameters in functions rather than string paths wherever possible.
- Use `Make/FREE` for temporary waves inside functions.

### Compiler rules (Igor 10 breaking changes)
- Unreachable code before `case` labels in `switch`/`strswitch` is a compile ERROR.
- `#pragma independentModule=ProcGlobal` is a compile ERROR in Igor 10.
- `ExperimentModified` is NOT triggered by same-value assignments in Igor 10.

### Panel and GUI code — critical rules
- ALWAYS call `PauseUpdate` as the first line of any panel-building function.
- ALWAYS use a running `yPos` variable — never hardcode every y coordinate independently.
- ALWAYS calculate panel height before `NewPanel` by summing control heights + gaps.
  - Title area: ~45px. Each control row: ~22-25px. Section subtitle: ~28px. Bottom margin: ~30px.
  - Add 10% headroom. Better to have a slightly tall panel than clipped controls.
- Standard control heights: Button=20-22px, CheckBox=14px, SetVariable=18-23px, PopupMenu=21px.
- Standard gaps: between controls=5px, between sections=12px.
- Left margin: 5px. Panel width: 430px (single-column) or 640px (two-column).
- Title style: `font="Times New Roman"`, `fstyle=3`, `fColor=(0,0,52224)`, `frame=0`.
- Decorative line below title: `TitleBox FakeLine1, title=" ", labelBack=(0,0,52224), size={width,3}`.
- GetHelp button: always red `fColor=(65535,32768,32768)`, size=80×15, top-right corner.
- Primary action button: green `fColor=(32768,65535,49386)`, size ~200×22.
- See skill: `/igor-panel` for full geometry reference and worked example.

### Command lookup
When unsure of a command's exact syntax, flags, or output variables:
- Fetch: `https://docs.wavemetrics.com/igorpro/commands/<commandname-lowercase>`
- Full index: https://docs.wavemetrics.com/igorpro/commands
- Do NOT guess flag syntax — fetch the doc page instead.

### General Igor style
- Use `Function` not `Macro` for all new code.
- Package globals go in `root:Packages:<PackageName>:`.
- Use `Static Function` for internal helpers to avoid name collisions.
- Use `#pragma moduleName` to namespace modules.
- Prefer `DFREF` parameters over `SetDataFolder` + string paths in function signatures.
- Use `Printf` not `Print` for formatted output.
- Always check panel version numbers with `IR1_UpdatePanelVersionNumber` pattern.

## Python
- Python 3.x. Use numpy, scipy, h5py for data work.
- For Igor↔Python bridge: use `igorpro` module (Igor 10 only).
  - `igorpro.fn.<functionname>()` to call Igor functions from Python.
  - `wave.asarray()` to convert Igor wave to numpy array.

## General coding preferences
- Prefer explicit over implicit — name things clearly.
- Add `help={"..."}` strings to all panel controls.
- Comments in English.
- When generating a new .ipf file, always include a version history block at the top.
