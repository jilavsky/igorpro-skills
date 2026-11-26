---
description: "The MarkPerfTestTime operation is used in conjunction with SetIgorOption DebugTimer for performance testing of user-defined functions."
slug: /commands/markperftesttime
---

<div className="command-signature">

## <strong>MarkPerfTestTime</strong>  <em>idval</em> {#markperftesttime}

</div>

The MarkPerfTestTime operation is used in conjunction with `SetIgorOption DebugTimer` for performance testing of user-defined functions. When used between:

```igor
SetIgorOption DebugTimer, Start
```
and 

```igor
SetIgorOption DebugTimer, Stop
```

MarkPerfTestTime stores the ID value and the time of the call in a buffer. When `SetIgorOption DebugTimer, Stop` is called the contents of the buffer are dumped to a pair of waves: W_DebugTimerIDs will contain the ID values and W_DebugTimerVals will contain the corresponding times of the calls relative to the very first call. The timings use the same high precision mechanism as the StartMSTimer and StopMSTimer calls.

By default, `SetIgorOption DebugTimer, Start` allocates a buffer for up to 10000 entries. You can allocate a different sized buffer using `SetIgorOption DebugTimer, Start=bufsize`.

### *See Also* {#see-also}
[SetIgorOption](/igorpro/commands/setigoroption.md), [StartMSTimer](/igorpro/commands/startmstimer.md), [StopMSTimer](/igorpro/commands/stopmstimer.md)

Additional documentation is provided in an example experiment, PerformanceTesting.pxp, and a WaveMetrics procedure file, PerformanceTestReport.ipf.

### *Demos* {#demos}
[Open Performance Testing Demo](#igor-pxp/Examples/Testing/PerformanceTesting.pxp)