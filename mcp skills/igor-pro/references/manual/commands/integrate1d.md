---
description: "The Integrate1D function performs numerical integration of a user function between the specified limits (min_x and max_x)."
slug: /commands/integrate1d
---

<div className="command-signature">

## <strong>Integrate1D</strong> (<em>UserFunctionName</em>, <em>min_x</em>, <em>max_x</em> [, <em>options</em> [, <em>count</em> ] [, <em>pWave</em>]]]) {#integrate1d}

</div>

The Integrate1D function performs numerical integration of a user function between the specified limits (*min_x* and *max_x*).

### *Parameters* {#parameters}
*UserFunctionName* must have this format:


```igor
Function UserFunctionName(inX)
	Variable inX
	... do something
	return result
End
```

However, if you supply the optional pWave parameter then it must have this format:


```igor
Function UserFunctionName(pWave, inX)
	Wave pWave
	Variable inX
	... do something
	return result
End
```

*options* is one of the following:

|  |  |
| --- | --- |
| 0: | Trapezoidal integration (default). |
| 1: | Romberg integration. |
| 2: | Gaussian Quadrature integration. |


By default, *options* is 0 and the function performs trapezoidal integration. In this case Igor Pro evaluates the integral iteratively. In each iteration the number of points where Igor Pro evaluates the function increases by a factor of 2. The iterations terminate at convergence to tolerance or when the number of evaluations is 2<sup>23</sup>.

The *count* parameter specifies the number of subintervals in which the integral is evaluated. If you specify 0 or a negative number for count, the function performs an adaptive Gaussian Quadrature integration in which Igor Pro bisects the interval and performs a recursive refining of the integration only in parts of the interval where the integral does not converge to tolerance.

*pWave* is an optional parameter wave that, if present, is passed to your function as the first parameter. It is intended for your private use, to pass one or more values to your function, and is not modified by Igor. The *pWave* parameter was added in Igor Pro 7.00.

### *Details* {#details}
You can integrate complex valued functions using a function with the format:


```igor
Function/C complexUserFunction(inX)
	Variable inX
	Variable/C result
	... do something
	return result
End
```

The syntax used to invoke the function is:


```igor
Variable/C cIntegralResult=Integrate1D(complexUserFunction,min_x,max_x...)
```

You can also use Integrate1D to perform a higher dimensional integrals. For example, consider the function:

```igor
f(x,y) = 2*x + 3*y + x*y
```

In this case, the integral

$$
\displaystyle h=\int d y \int f(x, y) d x
$$

can be performed by establishing two user functions:


```igor
Function do2dIntegration(xmin,xmax,ymin,ymax)
	Variable xmin,xmax,ymin,ymax
	
	Variable/G	globalXmin=xmin
	Variable/G globalXmax=xmax
	Variable/G globalY
			
	return  Integrate1d(userFunction2,ymin,ymax,1)              // Romberg integration
End

Function userFunction1(inX)
	Variable inX
	
	NVAR globalY=globalY
	
	return (3*inX+2*globalY+inX*globalY)
End

Function userFunction2(inY)
	Variable inY
	
	NVAR globalY=globalY
	globalY=inY
	NVAR globalXmin=globalXmin
	NVAR globalXmax=globalXmax
	
	return Integrate1D(userFunction1,globalXmin,globalXmax,1)   // Romberg integration
End
```

This method can be extended to higher dimensions.

If the integration fails to converge or if the integrand diverges, Integrate1D returns NaN. When a function fails to converge it is a good idea to try another integration method or to use a user-defined number of intervals (as specified by the count parameter). Note that the trapezoidal method is prone to convergence problems when the absolute value of the integral is very small.

### *See Also* {#see-also}
[Integrate](/igorpro/commands/integrate.md), [Integrate2D](/igorpro/commands/integrate2d.md), [SumSeries](/igorpro/commands/sumseries.md)

### *Demos* {#demos}
[Open Numerical Integration Demo](#igor-pxp/Examples/Analysis/NumericalIntegrationDemo.pxp)