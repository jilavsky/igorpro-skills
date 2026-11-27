# Importing SAS data into Irena

Not needed for data reduced by Indra 4 in the same experiment: those are already in
`root:USAXS:`, `root:SAXS:`, `root:WAXS:`. Use import for external files.

Always open the import panel first. It creates the globals in `root:Packages:ImportData:`:
```igor
IR3I_ImportDataMain()          // panel IR3I_ImportData
NewPath/O/Q ImportDataPath, "Z:Users:jan:Data:project:"     // folder with the files
```
Destinations (tested):
- NXcanSAS → `root:ImportedSAS:<file>:<entry title>:` with `r_ q_ s_ w_<entry>`.
- ASCII → `root:ImportedData:SAXS:<file>:` with `R_ Q_ S_<file>`.

## A. NXcanSAS (.h5 / .hdf / .nxs). Simplest, recommended. **Tested, works.**

Call the reader directly, once per file:
```igor
// NEXUS_NXcanSASDataReader(pathName, fileName, Read1D, Read2D, UseFileNameAsFolder,
//                          UseSasEntryNameAsFolder, UseTitleNameAsFolder,
//                          InclSasInstrument, InclSasSample, InclSasNote)
NEXUS_NXcanSASDataReader("ImportDataPath", "sample1.h5", 1, 0, 1, 0, 0, 1, 1, 1)
KillDataFolder/Z root:Packages:NexusImportTMP      // cleanup, as the panel does
```
`Abort "Import of the data failed"` means the file is not readable NXcanSAS.

## B. ASCII (2–4 columns: Q, I, [uncertainty], [dQ])

**Tested, works** with the two settings marked REQUIRED below (without them the import fails or raises
a blocking DoAlert). Set the format and options, fill the file list, select files, import:
```igor
String/G   root:Packages:ImportData:DataPathName = "Y:...:Example Data:"   // REQUIRED: same folder as ImportDataPath, else the file list stays empty
String/G   root:Packages:ImportData:DataFormatType = "ASCII SAXS/SANS"
String/G   root:Packages:ImportData:DataExtension = "dat"      // or "txt", "csv"
Variable/G root:Packages:ImportData:AutomaticallyOverwrite = 1  // else an overwrite DoAlert blocks you
Variable/G root:Packages:ImportData:UseFileNameAsFolder = 1
Variable/G root:Packages:ImportData:UseQRSNames = 1
// column assignment (1 = this column is ...). Default APS/Irena files: col1=Q, col2=I, col3=uncertainty
Variable/G root:Packages:ImportData:Col1Qvec = 1
Variable/G root:Packages:ImportData:Col2Int  = 1
Variable/G root:Packages:ImportData:Col3Err  = 1
Variable/G root:Packages:ImportData:QvectInA = 1      // or QvectInA=0, QvectInNM=1 for 1/nm (converted to 1/A, verified)
Variable/G root:Packages:ImportData:FoundNWaves = 3   // REQUIRED: number of columns in the file. Normally set by the panel's
                                                      // "Test" button; 0 → "Import waves problem" DoAlert + Abort (blocks)
IR3I_UpdateListOfFilesInWvs()     // fills root:Packages:ImportData:WaveOfFiles
// select files: set WaveOfSelections[i]=1 for the wanted rows (match names in WaveOfFiles)
root:Packages:ImportData:WaveOfSelections = 0
root:Packages:ImportData:WaveOfSelections[0,1] = 1   // rows found with FindValue/TEXT="name.dat"/TXOP=4 root:Packages:ImportData:WaveOfFiles
IR3I_ImportSelectedData()
```
Check the file's header first (column order, Q units are often stated: `q[nm-1]`).

Traps that open dialogs (avoid them):
- No uncertainty column and neither `CreateSQRTErrors` nor `CreatePercentErrors` set → may warn.
  If the file has no errors, set `CreatePercentErrors=1` and `PercentErrorsToUse=5` (or ask the user).
- `SlitSmearData=1` with `SlitLength=0` → DoPrompt for slit length. Set `SlitLength` first.
- `AutomaticallyOverwrite=0` and the data already exist → DoAlert.
- Do not press the panel's "Select data path" button: it opens a folder dialog. Use `NewPath`.

## Verify
`DataFolderDir(1, root:ImportedData:SAXS)` lists the new folders. Plot one quickly:
`Display/N=CheckImport r_name vs q_name; ModifyGraph/W=CheckImport log=1`, then capture the window.
