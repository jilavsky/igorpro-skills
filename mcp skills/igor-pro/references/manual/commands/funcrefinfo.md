---
description: "The FuncRefInfo function returns information about a FUNCREF. funcRef is a function reference variable declared by a FUNCREF statement in a user-defined…"
slug: /commands/funcrefinfo
---

<div className="command-signature">

## <strong>FuncRefInfo</strong> (<em>funcRef</em>) {#funcrefinfo}

</div>

The FuncRefInfo function returns information about a FUNCREF.

### *Parameters* {#parameters}
*funcRef* is a function reference variable declared by a FUNCREF statement in a user-defined function.

### *Details* {#details}
FuncRefInfo returns a semicolon-separated keyword/value string containing the following information:


| Keyword | Information |
| --- | --- |
| NAME | The name of the reference function or "" if the FUNCREF variable has not been assigned to point to a function. |
| ISPROTO | 0 if the FUNCREF variable has been assigned to point to a function. |
|  | 1 if it has not been assigned and therefore still points to the prototype function. |
| ISXFUNC | 0 if it points to a user-defined function. |
|  | 1 if the FUNCREF points to an external function. |

### *See Also* {#see-also}
[Function References](/igorpro/programming/programming.md#function-references), [FUNCREF](/igorpro/programming/keywords/object-reference-keywords.md#funcref)