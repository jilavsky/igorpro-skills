# Size distribution in Irena (MaxEnt / Regularization / TNNLS)

**Status: not yet tested via MCP.**

Panel `IR1R_SizesInputPanel`, graph `IR1R_SizesInputGraph`. Globals: `root:Packages:Sizes:`.
Recipe follows the Scripting tool (`IR2_ScriptingTool.ipf`, Sizes section).

## Recipe (one data set)

```igor
IR1R_Sizes()                                             // open panel + create globals
// --- select data ---
Variable/G root:Packages:Sizes:UseIndra2Data = 1          // or UseQRSdata = 1
Variable/G root:Packages:Sizes:UseQRSdata    = 0
String/G root:Packages:Sizes:DataFolderName    = "root:USAXS:Sample1_0013:"
String/G root:Packages:Sizes:IntensityWaveName = "DSM_Int"
String/G root:Packages:Sizes:QWavename         = "DSM_Qvec"
String/G root:Packages:Sizes:ErrorWaveName     = "DSM_Error"
// slit-smeared data: SMR_* waves + UseSlitSmearedData=1 + SlitLength
IR1R_GraphIfAllowed("GraphIfAllowedSkipRecover")         // loads data, makes the graph
// --- Q range via cursors ---
Wave Q = root:Packages:Sizes:Q_vecOriginal
Cursor/P/W=IR1R_SizesInputGraph A, IntensityOriginal, BinarySearch(Q, 0.001)
Cursor/P/W=IR1R_SizesInputGraph B, IntensityOriginal, BinarySearch(Q, 0.3)
// --- uncertainties: exactly one of these = 1 ---
Variable/G root:Packages:Sizes:UseUserErrors = 1
Variable/G root:Packages:Sizes:UseSQRTErrors = 0
Variable/G root:Packages:Sizes:UsePercentErrors = 0
IR1R_UpdateErrorWave()
// --- model ---
String/G   root:Packages:Sizes:ShapeType = "Spheroid"
Variable/G root:Packages:Sizes:AspectRatio = 1           // 1 = sphere
Variable/G root:Packages:Sizes:Dmin = 20                  // DIAMETER range [Å] (panel "Minimum/Maximum diameter")
Variable/G root:Packages:Sizes:Dmax = 10000
Variable/G root:Packages:Sizes:numOfPoints = 50
String/G   root:Packages:Sizes:LogDist = "yes"            // log-spaced bins
Variable/G root:Packages:Sizes:ScatteringContrast = 1     // Δρ² in 10^20 cm^-4; 1 = arbitrary volume scale
Variable/G root:Packages:Sizes:Bckg = 0                   // flat background to subtract
// method: exactly one = 1
Variable/G root:Packages:Sizes:UseMaxEnt = 1
Variable/G root:Packages:Sizes:UseRegularization = 0
Variable/G root:Packages:Sizes:UseTNNLS = 0
Variable/G root:Packages:Sizes:FitFailed = 0
IR1R_SizesFitting("DoFittingSkipReset")
// check root:Packages:Sizes:FitFailed
IR1R_saveData("SaveDataNoQuestions")                     // save into the data folder
```
Alternative to `IR1R_SizesFitting`: `IR1R_SizesEstimateErrors()` runs repeated fits to estimate
uncertainties of the distribution (slower).

Notes:
- Choose Dmin ≈ π/Qmax and Dmax ≈ π/Qmin (or smaller) from the cursor Q range. The panel sets
  `Dmin/Dmax`; `Rmin/Rmax` are internal. Verify which one the fit used in the result wave note.
- If MaxEnt does not converge, try `ErrorsMultiplier` > 1, or switch to TNNLS.
- `Bckg` should be the high-Q flat background. Estimate it from the last points or ask the user.
- Other shapes: list in `root:Packages:FormFactorCalc:ListOfFormFactorsSD`. Shape parameters use
  `AspectRatio`, `CylinderLength`, `CoreShell*`, `UserFFpar1..5`.

## Dialog traps

- Plain `IR1R_GraphIfAllowed("...")` without `SkipRecover` → DoPrompt "Previous solutions found".
- `IR1R_saveData` without `"SaveDataNoQuestions"` → DoPrompt for a comment.
- Data waves of unequal length → DoAlert. Check `numpnts` of the three waves first.
- Panel-version mismatch DoAlert on open: if it appears, ask the user to click; it happens once.

## Results

Saved into the data folder: `SizesVolumeDistribution_N`, `SizesDistDiameter_N`,
`SizesFitIntensity_N`, `SizesVolumeDistErrors_N`. Parameters and the method are in the wave notes.
Report the method, the range, the total volume fraction (`root:Packages:Sizes:TotalVolumeFraction`,
valid only with a true contrast), and the mean size. Capture `IR1R_SizesInputGraph`.
