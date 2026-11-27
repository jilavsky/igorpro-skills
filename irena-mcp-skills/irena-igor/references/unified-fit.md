# Unified fit (Beaucage) in Irena

Panel `IR1A_ControlPanel`, graphs `IR1_LogLogPlotU` (I vs Q) and `IR1_IQ4_Q_PlotU`.
Globals: `root:Packages:Irena_UnifFit:`. Recipe follows the Scripting tool (IR2_ScriptingTool.ipf,
`IR2S_FItWithUnifiedFit`).

Status (2026-11 test on sphere data): the recipe runs and fits, **but this tool is not yet
agent-safe**. Every fit where a fitted parameter ends within 2% of a limit raises a blocking DoAlert,
and invalid limits raise another one before the fit. In testing this happened in 3 of 3 fits.
Until the package has agent-mode dialog wrappers, warn the user that they may need to click OK in Igor.

## Recipe (one data set)

```igor
IR1A_UnifiedModel()                                     // open panel + create globals
// --- select data (set SVARs directly; the popup procs need STRUCTs) ---
Variable/G root:Packages:Irena_UnifFit:UseIndra2Data = 1   // USAXS data; use UseQRSdata=1 for r_/q_/s_ data
Variable/G root:Packages:Irena_UnifFit:UseQRSdata    = 0
String/G root:Packages:Irena_UnifFit:DataFolderName    = "root:USAXS:Sample1_0013:"
String/G root:Packages:Irena_UnifFit:IntensityWaveName = "DSM_Int"
String/G root:Packages:Irena_UnifFit:QWavename         = "DSM_Qvec"
String/G root:Packages:Irena_UnifFit:ErrorWaveName     = "DSM_Error"
// slit-smeared USAXS instead: SMR_* waves, UseSMRData=1, SlitLengthUnif=<from note(SMR_Int)>
IR1A_InputPanelButtonProc("DrawGraphsSkipDialogs")      // loads data into OriginalIntensity/OriginalQvector, makes graphs
// --- Q range via cursors ---
Wave Q = root:Packages:Irena_UnifFit:OriginalQvector
Cursor/P/W=IR1_LogLogPlotU A, OriginalIntensity, BinarySearch(Q, 0.001)
Cursor/P/W=IR1_LogLogPlotU B, OriginalIntensity, BinarySearch(Q, 0.2)
// --- model ---
Variable/G root:Packages:Irena_UnifFit:NumberOfLevels = 1
// set starting values + fit flags + limits for each level (see table)
Variable/G root:Packages:Irena_UnifFit:SkipFitControlDialog = 1   // REQUIRED, else PauseForUser blocks
Variable/G root:Packages:Irena_UnifFit:FitFailed = 0
IR1A_InputPanelButtonProc("DoFittingSkipReset")
// check root:Packages:Irena_UnifFit:FitFailed (1 = failed)
IR1A_InputPanelButtonProc("CopyTFolderNoQuestions")     // save results into the data folder
```

Notes:
- `BinarySearch` returns -1 / -2 outside the range. Clip to 0 / `numpnts(Q)-1`.
- Wave names of the data in the panel's internal folder: `OriginalIntensity`, `OriginalQvector`,
  `OriginalError`. The cursors must be on trace `OriginalIntensity`.
- Revert to the parameters before the fit: `IR1A_InputPanelButtonProc("RevertFitting")`.

## Parameters (per level N = 1..5)

| Global | Meaning | Fit flag | Limits |
|---|---|---|---|
| `LevelNG` | Guinier prefactor G | `LevelNFitG` | `LevelNGLowLimit`, `LevelNGHighLimit` |
| `LevelNRg` | Radius of gyration [Å] | `LevelNFitRg` | `LevelNRgLowLimit/HighLimit` |
| `LevelNB` | Power-law prefactor B | `LevelNFitB` | `LevelNBLowLimit/HighLimit` |
| `LevelNP` | Power-law slope P (Porod = 4) | `LevelNFitP` | `LevelNPLowLimit/HighLimit` |
| `LevelNRgCO` | Rg cutoff to level below | `LevelNFitRgCO` | ... |
| `LevelNCorelations`, `LevelNETA`, `LevelNPACK` | correlation (interference) | `LevelNFitETA/PACK` | ... |
| `SASBackground` | flat background | `FitSASBackground` | — |

Errors after a fit: `LevelNRgError`, `LevelNGError`, `LevelNPError`, `LevelNBError`, `SASBackgroundError`.

Setting many globals at once (tested):
`SetDataFolder root:Packages:Irena_UnifFit; NumberOfLevels=1; Level1G=2700; Level1FitG=1; ...; SetDataFolder root:`

Starting values matter: Unified will fail or wander with poor guesses. Estimate them from the data:
- Guinier region (level 1, the smallest structure is at the highest Q): G ≈ I at the Q where the curve
  flattens; Rg ≈ 1/Q at the knee.
- Power law above the knee: P = −slope in log-log; B ≈ I·Q^P in that region.
- Background ≈ the flat I at the highest Q, if present.
- Set limits to roughly 0.1×–10× the start (P: 1–4.5). Fix (fit flag 0) what is not constrained by the data.
- Fit with fewer free parameters first, then free more.
- **Spherical particles / form-factor oscillations:** P floats down to its lower limit and B to ~0
  (both seen in testing). Fix `Level1P=4` (`Level1FitP=0`) and link B to G and Rg
  (`Level1LinkB=1`, `Level1FitB=0`).
- Before fitting, every fitted parameter's start value must lie strictly inside its limits.
  Otherwise "Level N X limits set incorrectly" DoAlert blocks you.

## Dialog traps

- **"One or more limits may have been reached" DoAlert** fires after a fit when a parameter ends
  within 2% of a limit, unless the call comes from the Scripting tool. *It will block you.*
  Prevention: set generous limits, and check that the starting values are not near a limit.
  If it happens, ask the user to click OK in Igor, then widen the limits.
  (`UseNoLimits=1` avoids it but fits without limits. Ask the user before using it.)
- Plain `"DoFitting"` / `"DrawGraphs"` / `"CopyToFolder"` → dialogs. Use the variants above.
- `"CopyMoveLevel"` → DoPrompt. Do not use.

## Results

Saved into the data folder: `UnifiedFitIntensity_N`, `UnifiedFitQvector_N`. Parameters are in
`note(UnifiedFitIntensity_N)`. Report G, Rg, B, P per level with errors, and the background.
Capture `IR1_LogLogPlotU` to show the fit.
