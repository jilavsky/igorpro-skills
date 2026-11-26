---
description: "The CloseMovie operation closes the currently open movie. You must close a movie before you can play it."
slug: /commands/closemovie
---

<div className="command-signature">

## <strong>CloseMovie</strong> {#closemovie}

</div>

The CloseMovie operation closes the currently open movie. You must close a movie before you can play it.

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
[Movies](/igorpro/advanced-topics.md#movies), [NewMovie](/igorpro/commands/newmovie.md)