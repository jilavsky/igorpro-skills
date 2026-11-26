---
description: "See The WMFitInfoStruct Structure for further explanation of WMFitInfoStruct."
slug: /programming/structures/wmfitinfostruct
---

## WMFitInfoStruct {#wmfitinfostruct}

See [The WMFitInfoStruct Structure](/igorpro/analysis/curve-fitting.md#the-wmfitinfostruct-structure) for further explanation of WMFitInfoStruct.


```igor
Structure WMFitInfoStruct
   char IterStarted     // Nonzero on the first call of an iteration
   char DoingDestWave   // Nonzero when called to evaluate autodest wave
   char StopNow         // Fit function sets this to nonzero to
                        // indicate that a problem has occurred
                        // and fitting should stop
   Int32 IterNumber     // Number of iterations completed
   Int32 ParamPerturbed // See The WMFitInfoStruct Structure for details
EndStructure
```