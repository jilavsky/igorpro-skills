---
description: "The AdoptFiles operation adopts external files and waves into the current experiment."
slug: /commands/adoptfiles
---

<div className="command-signature">

## <strong>AdoptFiles</strong>  [ <em>flags</em> ] {#adoptfiles}

</div>

The AdoptFiles operation adopts external files and waves into the current experiment.

When the experiment is next saved, the files and waves are saved in the experiment file for a packed experiment or in the experiment folder for an unpacked experiment. References to the external files are eliminated.

AdoptFiles cannot be called from a function except via [Execute](/igorpro/commands/execute.md)/P.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Adopts all external notebooks and user procedure files and all waves in the experiment. WaveMetrics Procedure files are not adopted. /A is equivalent to /NB/UP/DF. |
| <span class="table-cell-nowrap">/DF</span> | Adopt all waves saved external to the experiment. |
| <span class="table-cell-nowrap">/DF = *dataFolderPathStr*</span> | Adopt all waves saved external to the experiment that are in the specified data folder. |
| <span class="table-cell-nowrap">/I</span> | Shows the [Adopt All](/igorpro/igor-basics/experiments-files-and-folders.md#adopt-all) dialog and adopts what the user selects there. |
| <span class="table-cell-nowrap">/NB</span> | Adopts all external notebook files. |
| <span class="table-cell-nowrap">/UP</span> | Adopts all external user procedure files. |
| <span class="table-cell-nowrap">/W = *winTitleOrName*</span> | Adopts the specified notebook or procedure file. /W was added in Igor Pro 7.02. |
|  | *winTitleOrName* is a name, not a string, so you construct /W like this: |
|  | <code class="igor">/W=$"New Polar Graph.ipf"</code> |
|  | or: |
|  | <code class="igor">/W=Notebook0</code> |
|  | When working with independent modules, *winTitleOrName* is a procedure window title followed by a space and, in brackets, an independent module name. See [Independent Modules](/igorpro/advanced-topics.md#independent-modules) for details. |
| <span class="table-cell-nowrap">/WP</span> | Adopts all WaveMetrics Procedure procedure files. |
| <span class="table-cell-nowrap">/WV = *wave*</span> | Adopts only the specified wave. |

### *Details* {#details}
Only files and waves saved external to the current experiment are adopted. See [References to Files and Folders](/igorpro/igor-basics/experiments-files-and-folders.md#references-to-files-and-folders) for a discussion of such standalone files.

The number of objects actually adopted is returned in V_Flag.

To adopt just one wave, use:


```igor
AdoptFiles/WV=wave
```

To adopt just one notebook or procedure window use AdoptFiles/W=*winTitleOrName*.

### *Command Line and Macro Examples* {#command-line-and-macro-examples}

```igor
// Using AdoptFiles from the command line or from a macro
AdoptFiles/I                              // Show the Adopt All dialog.
AdoptFiles/A/WP                           // Adopt everything that can be adopted.
AdoptFiles/DF/NB/UP/WP                    // Adopt everything that can be adopted.
AdoptFiles/DF=root:subfolder              // Adopt any externally saved waves in root:subfolder.
AdoptFiles/W=$"Proc0.ipf"                 // Adopt Proc0.ipf if it is saved externally.
AdoptFiles/WV=GetWavesDataFolder(wave0,2) // Adopt wave0 if it is saved externally.
```

### *Function Examples* {#function-examples}

```igor
// Using AdoptFiles from a user-defined function - you must use Execute/P
Execute/P "AdoptFiles/A"                           // Schedule adoption of all user files and waves
Execute/P "AdoptFiles/WV="+GetWavesDataFolder(w,2) // Schedule adoption of wave w
```

### *See Also* {#see-also}
[Adopt All](/igorpro/igor-basics/experiments-files-and-folders.md#adopt-all),  [Adopting Notebook and Procedure Files](/igorpro/igor-basics/experiments-files-and-folders.md#adopting-notebook-and-procedure-files), [Avoiding Shared Igor Binary Wave Files](/igorpro/igor-basics/experiments-files-and-folders.md#avoiding-shared-igor-binary-wave-files), [Operation Queue](/igorpro/advanced-topics.md#operation-queue).