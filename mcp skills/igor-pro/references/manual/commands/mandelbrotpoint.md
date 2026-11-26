---
description: "The MandelbrotPoint function returns a value between 0 and maxIterations based on the Mandelbrot set complex quadratic recurrence relation z[n] = z[n-1]^2 + c…"
slug: /commands/mandelbrotpoint
---

<div className="command-signature">

## <strong>MandelbrotPoint</strong> (<em>x</em>, <em>y</em>, <em>maxIterations</em>, <em>algorithm</em>) {#mandelbrotpoint}

</div>

The MandelbrotPoint function returns a value between 0 and *maxIterations* based on the Mandelbrot set complex quadratic recurrence relation z[n] = z[n-1]^2 + c where x is the real component of c, y is the imaginary component of c and z[0] = 0.

The returned value is the number of iterations the equation was evaluated before |z[n]| > 2 (the escape radius of the Mandelbrot set), or *maxIterations*, whichever is less.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">*algorithm* = 0</span> | The "Escape Time" algorithm returns the integer n which is the number of iterations until \|z[n]\| > 2. |
| <span class="table-cell-nowrap">*algorithm* = 1</span> | The "Renormalized Iteration Count Algorithm" algorithm returns a floating point value which is a refinement of the number of iterations n by adding the quantity: |
|  | <code class="igor">5 - ln(ln(\|z[n+4]\|)) / ln(2)</code> |
|  | (which requires four more iterations of the recurrence relation). The returned value is clipped to *maxIterations*. |

### *Demos* {#demos}
[Open MultiThread Mandelbrot Demo](#igor-pxp/Examples/Programming/MultiThreadMandelbrot.pxp)

### *References* {#references}
[http://en.wikipedia.org/wiki/Mandelbrot_set](http://en.wikipedia.org/wiki/Mandelbrot_set)