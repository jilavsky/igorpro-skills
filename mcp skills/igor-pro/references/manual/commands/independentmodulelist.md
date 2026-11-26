---
description: "The IndependentModuleList function returns a string containing a list of independent module names separated by listSepStr."
slug: /commands/independentmodulelist
---

<div className="command-signature">

## <strong>IndependentModuleList</strong> (<em>listSepStr</em>) {#independentmodulelist}

</div>

The IndependentModuleList function returns a string containing a list of independent module names separated by *listSepStr*.

Use [StringFromList](/igorpro/commands/stringfromlist.md) to access individual names.

### *Parameters* {#parameters}
*listSepStr* contains the character, usually  ";", to be used to to separate the names in the returned list.

### *Details* {#details}
In Igor 6, only the first byte of *listSepStr* was used. In Igor 7 and later, all bytes are used.

ProcGlobal is not in the returned list, and the order of returned names is not defined.

### *See Also* {#see-also}
[Independent Modules](/igorpro/advanced-topics.md#independent-modules), [GetIndependentModuleName](/igorpro/commands/getindependentmodulename.md), [StringFromList](/igorpro/commands/stringfromlist.md), [FunctionList](/igorpro/commands/functionlist.md)