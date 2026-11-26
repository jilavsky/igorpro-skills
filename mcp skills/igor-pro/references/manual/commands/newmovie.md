---
description: "The NewMovie operation opens a movie file in preparation for adding frames."
slug: /commands/newmovie
---

<div className="command-signature">

## <strong>NewMovie</strong>  [<em>flags</em>] [<em>as</em> <em>fileNameStr</em> ] {#newmovie}

</div>

The NewMovie operation opens a movie file in preparation for adding frames.

NewMovie creates MP4 movies. Prior to Igor Pro 8, it created AVI movies. That older technology is still available using the /A flag, but it is deprecated and may not be available in future operating systems.

### *Parameters* {#parameters}
The file to be opened is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | NewMovie/A creates movie files using the deprecated AVI technology. |
| <span class="table-cell-nowrap">/CF = *factor*</span> | Specifies a compression factor relative to the theoretical uncompressed value. The default compression factor of 200 is used if you omit /CF. /CF was added in Igor Pro 8.00. It is ignored if you use the /A flag. |
| <span class="table-cell-nowrap">/CTYP = *typeStr*</span> | Specifies the compression codec to use. |
|  | *typeStr can* be "WMV3" to create .wmv files or "mp4v" to create MP4 files (default). |
| <span class="table-cell-nowrap">/F = *frameRate*</span> | Frames per second between 1 and 60. *frameRate* defaults to 30. |
| <span class="table-cell-nowrap">/I</span> | Obsolete. |
| <span class="table-cell-nowrap">/L[ = *flatten* ]</span> | Obsolete. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing file, if any. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/PICT = *pictName*</span> | Uses the specified picture (see [Pictures](/igorpro/graphing/making-figures/graphics.md#pictures)) rather than the top graph. |
| <span class="table-cell-nowrap">/S = *soundWave*</span> | Adding a sound track is not currently supported. If you would like this feature, let us know |
| <span class="table-cell-nowrap">/Z</span> | No error reporting; an error is indicated by nonzero value of the output variable V_flag. If the user clicks the cancel button in the Save File dialog, V_flag is set to -1. |

### *Details* {#details}
If either the path or the file name is omitted then NewMovie displays a Save File dialog to let you create a movie file. If both are present, NewMovie creates the file automatically.

If you use /P=*pathName* , note that it is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:" or "C:\\Folder1\\". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details.

There can be only one open movie at a time.

The target window at the time you invoke NewMovie must be a graph, page layout or Gizmo plot unless the /PICT flag is present. The window size should remain constant while adding frames to the movie. The window and optional sound wave are used to determine the size and sound properties only; they do not specify the first frame.

In Igor 7 or later, the target window at the time you call NewMovie is remembered and is used by AddMovieFrame even if it is not the top window when you call AddMovieFrame.

The /PICT flag allows you to create a movie from a page layout in conjunction with the SavePICT/P=\_PictGallery\_ method. See [SavePICT](/igorpro/commands/savepict.md). This allows creation of a movie from a source other than a graph, page layout or Gizmo window, but is rarely needed.

### *See Also* {#see-also}
[Movies](/igorpro/advanced-topics.md#movies), [AddMovieFrame](/igorpro/commands/addmovieframe.md), [AddMovieAudio](/igorpro/commands/addmovieaudio.md), [CloseMovie](/igorpro/commands/closemovie.md), [PlayMovie](/igorpro/commands/playmovie.md), [PlayMovieAction](/igorpro/commands/playmovieaction.md), [SavePICT](/igorpro/commands/savepict.md)