---
description: "The AddMovieFrame operation adds the top graph, page layout, Gizmo Window, or the specified picture to the currently open movie."
slug: /commands/addmovieframe
---

<div className="command-signature">

## <strong>AddMovieFrame</strong>  [/PICT=<em>pictName</em> ] {#addmovieframe}

</div>

The AddMovieFrame operation adds the top graph, page layout, Gizmo Window, or the specified picture to the currently open movie.

Support for page layout and Gizmo windows was added in Igor Pro 7.00.

When you write a procedure to generate a movie, you need to call the [DoUpdate](/igorpro/commands/doupdate.md) operation after all modifications to the target window and before calling AddMovieFrame. This allows Igor to process any changes you have made to the window.

In Igor 7 or later, the target window at the time you call NewMovie is remembered and is used by AddMovieFrame even if it is not the top window when you call AddMovieFrame.

If the /PICT flag is provided, then the specified picture from the picture gallery (see [Pictures](/igorpro/graphing/making-figures/graphics.md#pictures)) is used in place of the target window.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Suppresses error reporting. If you use /Z, check the V_Flag output variable to see if the operation succeeded. |

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| V_Flag | Set to 0 if the operation succeeded or to a non-zero error code. |
|  | V_Flag is set only if you use the /Z flag. |

### *See Also* {#see-also}
[Movies](/igorpro/advanced-topics.md#movies), [NewMovie](/igorpro/commands/newmovie.md), [AddMovieAudio](/igorpro/commands/addmovieaudio.md)