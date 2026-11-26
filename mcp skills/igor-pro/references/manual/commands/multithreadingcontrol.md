---
description: "The MultiThreadingControl operation allows you to control how automatic multithreading works with those IGOR operations that support it."
slug: /commands/multithreadingcontrol
---

<div className="command-signature">

## <strong>MultiThreadingControl</strong>  <em>keyword</em> [=<em>value</em>] {#multithreadingcontrol}

</div>

The MultiThreadingControl operation allows you to control how automatic multithreading works with those IGOR operations that support it. Automatic multithreading is described below under ***Details*** .

For most purposes you will not need to use this operation.

The MultiThreadingControl operation was added in Igor Pro 7.00.

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| getMode | Writes the current mode value into the variable V_autoMultiThread. |
| getThresholds | Creates the wave W_MultiThreadingArraySizes in the current data folder. See ***Automatic Multithreading Thresholds*** below for details. |
| <span class="table-cell-nowrap">setMode = *m*</span> | Sets the mode for automatic multithreading. The mode controls the circumstances in which automatic multithreading is enabled. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Disables automatic multithreading unconditionally.</td></tr><tr><td>*m*&nbsp;=1:</td><td>Enables automatic multithreading based on operation-specific thresholds for operations called from the main thread only. This is the default setting.</td></tr><tr><td>*m*&nbsp;=4:</td><td>Enables automatic multithreading based on operation-specific thresholds for operations called from the main thread and from user-created explicit threads.</td></tr><tr><td>*m*&nbsp;=8:</td><td>Enables automatic multithreading unconditionally - regardless of thresholds or the type of the calling thread.</td></tr></tbody></table>
|  | You cannot combine modes by ORing. The only valid values for *m* are those shown above. |
| <span class="table-cell-nowrap">setThresholds = *tWave*</span> | Sets the thresholds for automatic multithreading. See ***Automatic Multithreading Thresholds*** below for details. |

### *Details* {#details}
Some IGOR operations and functions have internal code that can execute calculations in parallel using multiple threads. These operations are marked as "Automatically Multithreaded" in the Command Help pane of the Igor Help Browser.

Running on multiple threads reduces the time required for number-crunching tasks on multi-processor machines when the benefit of using multiple processors exceeds the overhead of running in multiple threads. This is usually the case only for large-scale jobs.

By default Igor uses automatic multithreading in operations that support it when the number of calculations exceeds a threshold value. This is called "automatic multithreading" to distinguish it from the explicit multithreading that you can instruct Igor to do. Explicit multithreading is described under [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking). You don't need to do anything to benefit from automatic multithreading.

By default automatic multithreading is enabled for operations called from the main thread and disabled for operations called from explicit threads that you create (mode=1). You can change this using the setMode keyword described above.

The state of automatic multithreading is not saved with the experiment. It is initialized to mode=1 with default thresholds every time you start IGOR.

### *Automatic Multithreading Thresholds* {#automatic-multithreading-thresholds}
Executing these commands:

```igor
MultiThreadingControl getThresholds
Edit W_MultiThreadingArraySizes.ld
```

creates a wave named W_MultiThreadingArraySizes and displays it in a table. This shows you the current threshold for each operation that supports automatic multithreading. The wave includes dimension labels so you can see which row represents which operation's threshold.

The meaning of a given threshold value depends on the operation. For most operations the threshold is in terms of the number of points in the input wave. For some operations the threshold depends on the complexity of the calculation. For example, the threshold for the CurveFit operation takes the complexity of the fitting function into account.

You can change the threshold for a given operation by setting the data for the appropriate row of W_MultiThreadingArraySizes and passing it back to the MultiThreadingControl operation using the setThresholds keyword. For example:


```igor
W_MultiThreadingArraySizes[%ICA]=5000			// Set the ICA threshold
MultiThreadingControl setThresholds=W_MultiThreadingArraySizes	// Apply
```

You should not change any aspect of the wave other than the threshold values.

### *Multithreading and Roundoff Error* {#multithreading-and-roundoff-error}
Every floating point operation can potentially lead to roundoff error. Normally, if you run the exact same code on the exact same data, you get the exact same roundoff error and the exact same result.

This is not necessarily the case with multithreaded calculations. Because the partitioning of work among threads depends on circumstances, such as how many threads are free, different calculation runs on the same data may partition work differently. This can lead to differences in roundoff error and therefore differences in results.

You can obtain reproducibility at the expense of performance by turning off automatic multithreading:


```igor
MultiThreadingControl setMode=0
```

Although this produces reproducibility, it does not necessarily reduce the size of roundoff error.

### *Examples* {#examples}

```igor
MultiThreadingControl setMode=0	// Disable automatic multithreading
MultiThreadingControl setMode=8	// Always multithread regardless of wave size
```

### *See Also* {#see-also}
[Automatic Parallel Processing With TBB](/igorpro/advanced-topics.md#automatic-parallel-processing-with-tbb)

[Automatic Parallel Processing with MultiThread](/igorpro/advanced-topics.md#automatic-parallel-processing-with-multithread)

[ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)