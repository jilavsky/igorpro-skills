# USAXS / SAXS / WAXS reduction with Indra 4 (IN4)

Instrument data layout (APS USAXS): a *sample folder* containing segment folders whose names
end in `_usaxs` (USAXS `.h5`), `_saxs` and `_waxs` (Nika-reduced 2D `.hdf`). Each sample
has one file per segment with matching names. One file is the **blank** (empty holder).

The Indra 4 pipeline is already a chain of non-GUI functions, and its Igor-code path has no
DoAlert/DoPrompt. It reads its settings from `root:Packages:Indra4:` globals and the symbolic
path `Indra4DataPath`.

## Recipe

```igor
// 0. packages loaded (see loading-and-conventions.md)
IN4_Main()                                  // opens panel; creates ALL globals (do not skip)
NewPath/O/Q Indra4DataPath, "Y:Experiments:USAXS_data:2026:2026-10:10_25_ilavsky:Larry:Larry_usaxs:"   // the _usaxs folder (V_flag=0 = OK)
// 1. settings
String/G root:Packages:Indra4:BlankFileName = "Blank_0053.h5"   // exact file name in _usaxs folder
Variable/G root:Packages:Indra4:RecalcNexusData = 0   // 0 = import data already reduced (by Matilda at the beamline) from the files; 1 = reduce from raw
Variable/G root:Packages:Indra4:UseIgorCode = 1
Variable/G root:Packages:Indra4:UsePythonCode = 0     // 1 needs Igor 10 + Python with Matilda
Variable/G root:Packages:Indra4:IncludeUSAXS = 1
Variable/G root:Packages:Indra4:IncludeSAXS = 0       // 1 also reduces matching SAXS .hdf
Variable/G root:Packages:Indra4:IncludeWAXS = 0
Variable/G root:Packages:Indra4:IncludeImage = 0
// 2. run (string list of file names, ';'-separated)
String out = IN4_ProcessSelectedData("CM8_0_0054.h5;CM8_5_0059.h5;")
// returns e.g. "root:USAXS:CM8_0_0054;;root:USAXS:CM8_5_0059;;" (empty items are harmless)
// 3. optional standard graphs
IN4_PlotDataFolders(out)                    // graphs USAXS_R_data, USAXS_SMR_data, USAXS_DSM_data, SAXS_Data, WAXS_data
```

Run step 2 from `Igor__call_function` as `IN4_ProcessSelectedData("...")` (it returns a string),
or put the lines in a small user function. `String/G` and `Variable/G` overwrite existing globals,
which is intended here.

### Listing the files and choosing the blank
`IndexedFile(Indra4DataPath, -1, ".h5")` returns all USAXS files. Names end in a scan number
(`CM8_0_0054.h5`). Blanks are usually named `Blank_NNNN` and are measured before each sample
series: **use the blank with the highest scan number lower than the sample's**, and say so.
If unsure, ask the user. Check each file exists (`GetFileFolderInfo/P=Indra4DataPath/Q/Z=1`)
before running: a missing file opens a blocking Open-File dialog.

### Which mode: import vs recalculate
- `RecalcNexusData=0` (default for agents): imports the reduced data (SMR/DSM, R, blank R) that
  Matilda wrote into the Nexus file at the beamline. Fast (~0.05 s per file). **Tested, works.**
- `RecalcNexusData=1`: re-reduces from raw counts in Igor. As of 2026-11 the Igor code reads only
  the older DDPCA300/mca flyscan layout (12-ID-E). Files from the FX4-based instrument
  (`/entry/flyScan/fx4_range`, `upd_current`, ...) fail with "Loading /entry/flyScan/mca1 ...
  failed" followed by "expected wave name". Use mode 0, or Matilda/pyIrena, for those files.
  (The FX4 port to IN4 is pending, as of 2026-11-26. Remove this note when it lands.)

## What gets created

- `root:USAXS:<sample>:` with `R_Int/R_Qvec/R_error` (raw), `BL_R_Int...` (blank),
  `SMR_Int/SMR_Qvec/SMR_Error` (calibrated slit-smeared), `DSM_Int/DSM_Qvec/DSM_Error` (desmeared).
- With IncludeSAXS/WAXS: `root:SAXS:<sample>:` and `root:WAXS:<sample>:` with `r_/q_/s_` waves.
- Reduced USAXS data are also written back into the Nexus file (`IN4_SaveUSAXSDataInNexus`).
- The blank is cached in `root:Packages:Indra4:BlankData:` and reused while the name matches.

## Known failure modes

- `Abort "Import of data ... failed in IN4_ImportRawUSAXS"`: wrong file name or path.
- `Abort "Failure in peak center fitting in IN4_calculateR_Qvec ..."`: bad or empty scan. Skip
  this sample and report it.
- `Abort "step scan not done yet"`: step-scan data are not supported in IN4; only flyscans.
- If SAXS/WAXS are included, Nika is configured automatically (`NI1_APSConfigureNika`, hidden panel).
- Do not call `IN4_SetupPathAndGetListOfFiles()`: it opens a folder-picker dialog.

## Verify

Waves created per sample (tested): `R_Int R_Qvec R_Error BL_R_Int BL_R_Qvec BL_R_Error SMR_Int
SMR_Qvec SMR_Error SMR_dQ DSM_Int DSM_Qvec DSM_Error DSM_dQ`.

`capture_window` on `USAXS_DSM_data` (the legend colors may not match the traces; this is cosmetic). Check that the curve is smooth and positive, and
note the Q range (`WaveStats/Q DSM_Qvec`). Report the folders created.
