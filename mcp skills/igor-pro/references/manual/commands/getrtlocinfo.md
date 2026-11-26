---
description: "GetRTLocInfo is used for profiling Igor procedures. You will typically not call GetRTLocInfo directly but instead will use it through FunctionProfiling.ipf…"
slug: /commands/getrtlocinfo
---

<div className="command-signature">

## <strong>GetRTLocInfo</strong> (<em>code</em>) {#getrtlocinfo}

</div>

GetRTLocInfo is used for profiling Igor procedures.

You will typically not call GetRTLocInfo directly but instead will use it through FunctionProfiling.ipf which you can access using this include statement:


```igor
#include <FunctionProfiling>
```

GetRTLocation is called from an Igor preemptive thread to monitor the main thread. It returns a key/value string containing information about the procedure location associated with code or "" if the location could not be found.

### *Parameters* {#parameters}
*code* is the result from a very recent call to [GetRTLocation](/igorpro/commands/getrtlocation.md).

### *Details* {#details}
The format of the result string is:


```
"PROCNAME:name;LINE:line;FUNCNAME:name;"
```

As of Igor Pro 7.03, if the code is in an independent module other than ProcGlobal then this appears at the beginning of the result string:


```
IMNAME:imName;
```

The line number is padded with zeros to facilitate sorting.

### *See Also* {#see-also}
[GetRTLocation](/igorpro/commands/getrtlocation.md)