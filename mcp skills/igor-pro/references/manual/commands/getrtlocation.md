---
description: "GetRTLocation is used for profiling Igor procedures. You will typically not call GetRTLocation directly but instead will use it through FunctionProfiling.ipf…"
slug: /commands/getrtlocation
---

<div className="command-signature">

## <strong>GetRTLocation</strong> (<em>sleepMS</em>) {#getrtlocation}

</div>

GetRTLocation is used for profiling Igor procedures.

You will typically not call GetRTLocation directly but instead will use it through FunctionProfiling.ipf which you can access using this include statement:


```igor
#include <FunctionProfiling>
```

GetRTLocation is called from an Igor preemptive thread to monitor the main thread. It returns a code that identifies the current location in the procedure files corresponding to the procedure line that is executing in the main thread.

### *Parameters* {#parameters}
*sleepMs* is the number of milliseconds to sleep the preemptive thread after fetching a value. *sleepMs* must be between 0.001 and 100.

### *Details* {#details}
The result from GetRTLocation is passed to [GetRTLocInfo](/igorpro/commands/getrtlocinfo.md) to determine the location in the procedures. This samples the main thread only and the location becomes meaningless after any procedure editing.

### *See Also* {#see-also}
[GetRTLocInfo](/igorpro/commands/getrtlocinfo.md)