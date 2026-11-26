---
description: "The PlayMovieAction operation is used to extract frames from a movie file."
slug: /commands/playmovieaction
---

<div className="command-signature">

## <strong>PlayMovieAction</strong>  [/A/Z] <em>keyword</em>  [=<em>value</em> ] [, <em>keyword</em>  [=<em>value</em> ]] {#playmovieaction}

</div>

The PlayMovieAction operation is used to extract frames from a movie file.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Uses alternate deprecated technology, AVI instead of MMF. |
| <span class="table-cell-nowrap">/Z</span> | Errors do not stop procedure execution. Use V_Flag to see if an error occurred. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| extract | Extracts current frame into an 8-bit RGB image wave named M_MovieFrame. (ok to combine with frame=*f* ). |
| <span class="table-cell-nowrap">extract = *e*</span> | Extracts *e* frames into a single multframe wave named M_MovieChunk. This will have 3 planes for RGB and will have *e* chunks. |
|  | e=1 is the same as plain extract. |
|  | For e>1, the current time is automatically updated. |
| <span class="table-cell-nowrap">frame = *f*</span> | Moves to specified movie frame. |
| getID | Returns top movie ID number in V_Value. Do not use in same call with getTime. |
| getTime | Reads current movie time into variable V_value (in seconds). |
| gotoBeginning | Goes to beginning of movie. |
| gotoEnd | Goes to end of movie. |
| kill | Closes open movie. |
| <span class="table-cell-nowrap">loop = *mode*</span> | The loop extraction method keyword was added in Igor Pro 8.00. It is no longer supported and is ignored. |
| <span class="table-cell-nowrap">open = *fullPath*</span> | Opens the specifed movie file to enable frame extraction. V_Flag is set to zero if no error occurred and V_Value is set to the file reference number. |
| <span class="table-cell-nowrap">ref = *refNum*</span> | The ref keyword is used with all PlayMovieAction commands after using the open keyword to access a movie file. *refNum* must be the file reference number returned in V_Value in the open step. |
|  | The ref keyword is needed only if multiple files or windows are open. You can also use setFrontMovie to set the active movie. |
| <span class="table-cell-nowrap">setFrontMovie = *id*</span> |  |
|  | Sets the movie with given *id* as the active movie file. |
|  | Do not use setFrontMovie and getID in the same call to PlayMovieAction. |
| start | Obsolete. Movie windows are no longer supported in Igor itself. |
| <span class="table-cell-nowrap">step = *s*</span> | Moves by *s*  frames into movie (0 is same as 1, negative values move backwards). |
| stop | Obsolete. Movie windows are no longer supported in Igor itself. |

### *Details* {#details}
Operations are performed in the following order: kill, gotoBeginning, gotoEnd, frame, step, getTime, extract. kill overrides all other parameters.

If you want to extract a grayscale image, you can convert the RGB image into grayscale using the ImageTransform command like so:


```igor
PlayMovieAction extract
ImageTransform rgb2gray M_MovieFrame
NewImage M_RGB2Gray
```

When you are finished extracting frames, use the kill keyword to close the file.

To get a full path for use with the open keyword, use the [PathInfo](/igorpro/commands/pathinfo.md) or [Open](/igorpro/commands/open.md) /D/R commands.

### *Examples* {#examples}
These commands show how to determine the number of frames in a simple movie:


```igor
PlayMovieAction open = <full path to movie file>
PlayMovieAction gotoEnd, getTime
Variable tEnd = V_Value
PlayMovieAction step=-1, getTime
Print "frames = ", tEnd/(tEnd-V_value)
PlayMovieAction kill
```

### *See Also* {#see-also}
[Movies](/igorpro/advanced-topics.md#movies), [PlayMovie](/igorpro/commands/playmovie.md), [Displaying an Open File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-an-open-file-dialog)