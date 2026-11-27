# Loading packages and data conventions

## Loading

The boot procedures live in the user's *Igor Procedures* folder, so these loader functions
exist as soon as Igor starts, provided the packages are installed. Check first:
`exists("LoadUSAXS")==6` (6 = user function exists).

| Want | Call (Igor__call_function or execute_command) | Notes |
|---|---|---|
| Indra + Irena + Nika (everything) | `LoadUSAXS()` | Indra's loader #includes Irena and Nika. Menu item text: "Macros → Load USAXS". |
| Irena only | `LoadIrenaSASMacros()` | Menu "Macros → Load Irena SAS Macros"; builds menu "SAS". |
| Nika only | `LoadNika2DSASMacros()` | Builds menu "SAS 2D". |

The loaders use `Execute/P` (INSERTINCLUDE + COMPILEPROCEDURES), so the code is not available
*inside* the same call. In testing (2026-11) it was compiled by the next MCP call. Verify with:
- Indra: `exists("IN4_Main")==6`
- Irena: `exists("IR1A_UnifiedModel")==6`
- Nika: `exists("NI1A_Convert2Dto1DMainPanel")==6`

If compile errors appear, report them to the user. Do not try to edit package code.

Loaded already? The same `exists()` checks tell you. Loading twice is harmless.

## Where data lives

| Data | Folder | Wave names | Tool data-type switch |
|---|---|---|---|
| USAXS reduced by Indra | `root:USAXS:<sample>:` | `SMR_Int, SMR_Qvec, SMR_Error` (slit smeared); `DSM_Int, DSM_Qvec, DSM_Error` (desmeared); raw `R_Int, R_Qvec, R_error`; merged data may use `M_SMR_*`, `M_DSM_*` | `UseIndra2Data=1, UseQRSdata=0` |
| SAXS from Indra 4 / Nika | `root:SAXS:<sample>:` | `r_<sample>, q_<sample>, s_<sample>` (Intensity, Q, uncertainty) | `UseQRSdata=1, UseIndra2Data=0` |
| WAXS from Indra 4 / Nika | `root:WAXS:<sample>:` | `R_/Q_/S_<sample>` | `UseQRSdata=1` |
| Imported ASCII (Irena import) | `root:ImportedData:SAXS:<file>:` (or `:WAXS:`) | `R_<file>, Q_<file>, S_<file>` | `UseQRSdata=1` |
| Imported NXcanSAS | `root:ImportedSAS:<file>:<entry>:` | `r_<entry>, q_<entry>, s_<entry>, w_<entry>` (w = dQ) | `UseQRSdata=1` |

- Units: Q in 1/Å, calibrated intensity in cm²/cm³ (1/cm).
- Metadata is stored in **wave notes** as `key=value;` lists. Read with
  `note(<wave>)` and `StringByKey("key", note(<wave>), "=", ";")`. For slit-smeared USAXS data
  look for the slit length in the note of `SMR_Int`.
- Igor names are case-insensitive. Folder names with special characters need quoting:
  `root:USAXS:'my sample':`. Use `PossiblyQuoteName()` when you build paths.

Listing what is in the experiment:
- Sub-folders: `DataFolderDir(1, root:USAXS)` returns `FOLDERS:a,b,c;`.
- Waves in a folder: `WaveList("*", ";", "")` after `SetDataFolder`; restore with `SetDataFolder root:`.

## Where results go

Irena saves results **into the data folder** as new waves with a generation suffix
(`_0`, `_1`, ...; each save makes the next number):
- Unified fit: `UnifiedFitIntensity_N`, `UnifiedFitQvector_N` (+ local-level waves if asked).
  Fit parameters are in the wave note of `UnifiedFitIntensity_N`.
- Size distribution: `SizesVolumeDistribution_N`, `SizesDistDiameter_N`,
  `SizesFitIntensity_N`, `SizesVolumeDistErrors_N`. Parameters are in the wave notes.
- The highest N is the latest result.

## Package globals (for orientation)

| Tool | Globals folder | Main panel / graph |
|---|---|---|
| Indra 4 reduction | `root:Packages:Indra4:` | `IN4_DataReductionPanel` |
| Unified fit | `root:Packages:Irena_UnifFit:` | `IR1A_ControlPanel` / `IR1_LogLogPlotU` |
| Size distribution | `root:Packages:Sizes:` | `IR1R_SizesInputPanel` / `IR1R_SizesInputGraph` |
| Import | `root:Packages:ImportData:` | `IR3I_ImportData` |
| Scripting tool | `root:Packages:Irena:ScriptingTool:` | `IR2S_ScriptingToolPnl` |
