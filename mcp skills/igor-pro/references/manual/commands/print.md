---
description: "The Print operation prints the evaluated expressions in the history area."
slug: /commands/print
---

<div className="command-signature">

## <strong>Print</strong>  [/C/D/F/LEN/S/SR] <em>expression</em>  [, <em>expression</em> ]... {#print}

</div>

The Print operation prints the evaluated expressions in the history area.

### *Parameters* {#parameters}
An expression can be a wave, a numeric expression (e.g., 3*Pi/4), a string expression (e.g., "Today is " + date()), or an individual structure element or an entire structure variable.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Evaluates all numeric expressions as complex. |
| <span class="table-cell-nowrap">/D</span> | Prints a greater number of digits. |
| <span class="table-cell-nowrap">/F</span> | Prints numeric wave data (1D and 2D waves only) using "nice," easily readable formatting. |
| <span class="table-cell-nowrap">/LEN = *len*</span> | Sets the string break length to *len* number of bytes. The default is 200, and *len* is clipped to between 50 and 2500. |
| <span class="table-cell-nowrap">/S</span> | Obsolete. Numeric results are printed with a moderate number of digits whether you use /S or not. To print more digits, use /D. |
| <span class="table-cell-nowrap">/SR</span> | Prints a wave subrange for expressions that start as "*waveName*[". Without /SR, such an expression is taken as the start of a numeric expression such as wave[3]-wave[2]. (You can still use *wave*[*pnt*] but only if it does not start the numeric expression.) |
|  | Wave subrange printing is not done with /F. |
|  | You can specify a single row or column using [*r*] syntax. For example, to print column 4 of a matrix, use: |
|  | <code class="igor">Print mymat[][4]</code> |

### *Details* {#details}
Numeric expressions are always evaluated in double precision. The /D flag just controls the number of digits displayed.

Print determines if an expression is real, complex or string from the first symbol in the expression. Usually this works fine, but occasionally Print guesses wrong and you may have to rearrange your expression. For example:


```igor
Print 1+cmplx(1,2)
```

will give an error because the first symbol, "1", is real but the expression should be complex. Changing this to


```igor
Print cmplx(1,2)+1
```

will work.

Printing numeric or string expressions involving structure elements must not start with the structure element. Instead an appropriate numeric or string literal must appear first so that Igor can determine what kind of expression to compile. For example rather than


```igor
Print astruct.astring + "hello"
```

use


```igor
Print "" + astruct.astring + "hello"
```

Print breaks long strings into multiple lines. If there are no natural breaks (carriage returns or semicolons) within a default length, then it breaks the string arbitrarily.

The default line length is 200 bytes. You can override this using the /LEN flag. The maximum number of bytes that can be printed on a line in the history area is 2510.  (Igor allows up to 10 more characters than the /LEN value if a natural break in those 10 characters is found).

When printing waves, you can use either formatted (set by /F) or unformatted (default) methods. Unformatted output is in an executable syntax for each printed line: wave={}.

:::note
Executing lines printed from floating point waves will not exactly reproduce the source data due to roundoff or insufficient digits in the printed output.
:::

Printing formatted wave data gives easily (human) readable output, and works best for small 1D and 2D waves. If the data are too large or in an unsupported format (3D or greater, or the wave is text), then the output will be unformatted. Formatting is done using spaces, so the output will look best in a fixed-width font.

Printed wave data, both formatted and unformatted, are limited to no more than 100 lines of output. When the line limit is exceeded, a warning message will be printed at the end of the truncated output. For text waves, output is limited to 200 bytes of each string element, and there is no warning when a string is truncated.

### *Printing from Threads* {#printing-from-threads}
Printing text into the history area can be slow and is not threadsafe. Consequently, when text is printed into the history from a thread (see [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)), the printed lines are not printed directly to the history area. Instead, they are stored in a queue to be printed later. The actual print happens when you call [DoUpdate](/igorpro/commands/doupdate.md) or when the main thread prints to the history. Printing to the history can occur if you call the [Print](/igorpro/commands/print.md) or [printf](/igorpro/commands/printf.md) operations, or if you invoke an operation that itself prints results into the history, such as [CurveFit](/igorpro/commands/curvefit.md).

In Igor Pro 9 and before, limits were placed on the number of lines that would print from the thread queue and the total number of lines that could be stored in the queue. In Igor Pro 10 the limits were removed. We assume that most uses of Print or [printf](/igorpro/commands/printf.md) in a thread are for debugging, so problems caused by large volumes of output are tolerable. Most operations that print results to the history include a /Q flag that prevents that printing.

If you are troubled by runaway output to the history area in threaded code, you can use a [SetIgorOption](/igorpro/commands/setigoroption.md) keyword to limit the number of lines that can be stored in the queue:


```igor
SetIgorOption ThreadPrintingLimit=limit
```

Replace *limit* with a number giving the desired limit. By default, the limit is set to -1, which means it is unlimited. Setting *limit* to zero suppresses output to the history from threads. To query the current value of the limit, replace *limit* with "?". The value can then be read from the global variable V_flag.

You may still get more lines printed than the limit: every time the main thread prints into the history, the current contents of the queue are printed to the history and the queue is emptied. Calling DoUpdate will also cause the queue to be printed to the history, freeing the queue to accept a new batch of lines.

### *See Also* {#see-also}
[printf](/igorpro/commands/printf.md)

[PrintGraphs](/igorpro/commands/printgraphs.md), [PrintTable](/igorpro/commands/printtable.md), [PrintLayout](/igorpro/commands/printlayout.md), [PrintNotebook](/igorpro/commands/printnotebook.md)