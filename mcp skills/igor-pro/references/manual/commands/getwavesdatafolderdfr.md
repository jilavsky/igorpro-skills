---
description: "The GetWavesDataFolderDFR function returns a data folder reference for the data folder containing the specified wave."
slug: /commands/getwavesdatafolderdfr
---

<div className="command-signature">

## <strong>GetWavesDataFolderDFR</strong> (<em>waveName</em>) {#getwavesdatafolderdfr}

</div>

The GetWavesDataFolderDFR function returns a data folder reference for the data folder containing the specified wave.

GetWavesDataFolderDFR is the same as GetWavesDataFolder except that it returns a data folder reference instead of a string containing a path.

:::caution
If you call GetWavesDataFolderDFR from a preemptive thread with a wave that is in a data folder created by the main thread, the returned reference gives the thread access to that data folder, including waves you did not pass to the thread. While the thread uses the reference, the main thread must not change or kill that data folder or its contents. Doing so can corrupt data or crash Igor. See [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking).
:::

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [Data Folder References](/igorpro/programming/programming.md#data-folder-references)