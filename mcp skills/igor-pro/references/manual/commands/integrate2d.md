---
description: "The Integrate2D operation calculates a two-dimensional numeric integral of a real-valued user-defined function or a wave."
slug: /commands/integrate2d
---

<div className="command-signature">

## <strong>Integrate2D</strong>  [/Q /Z=<em>zFlag</em> /OPTS=<em>options</em>] [ <em>keyword</em> = <em>value</em> ...] {#integrate2d}

</div>

The Integrate2D operation calculates a two-dimensional numeric integral of a real-valued user-defined function or a wave. The result of the operation is stored in the variable V_value and the variable V_Flag is set to zero if there are no errors.

This operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/OPTS = *op*</span> | Sets the integration options. By default, both the x and the y integrations are performed using the adaptive trapezoidal method. |
|  | *op* is a bitwise parameter that you set to select the x and y integration methods. Set one bit for x and one bit for y: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Trapezoidal in Y (1)</td></tr><tr><td>Bit&nbsp;1:</td><td>Romberg in Y (2)</td></tr><tr><td>Bit&nbsp;2:</td><td>Gaussian Quadrature in Y (4)</td></tr><tr><td>Bit&nbsp;3:</td><td>Trapezoidal in X (8)</td></tr><tr><td>Bit&nbsp;4:</td><td>Romberg in X (16)</td></tr><tr><td>Bit&nbsp;5:</td><td>Gaussian Quadrature in X (32)</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |

Using these constants you can specify, for example, Romberg integration in the Y direction and Gaussian Quadrature in the X direction using /OPTS=(2 \| 32).

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | Suppress printing to the history area. |
| <span class="table-cell-nowrap">/Z = *zFlag*</span> | Set *zFlag* to 1 to suppress error reporting. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">epsilon = *ep*</span> | Specifies the convergence parameter. By default *ep* =1e-5. Smaller values lead to more accurate integration result but the tradeoff is longer computation time. |
| <span class="table-cell-nowrap">Integrand = *uF*</span> | Specifies the user-defined function to be integrated. See ***The Integrand Function*** below for details. |
| <span class="table-cell-nowrap">innerLowerLimit = *y1*</span> |  |
|  | Specifies the lower limit of the inner integral if this limit is fixed, i.e., if it is not a function of x. See the innerLowerFunc keyword if you need to specify a function for this limit. |
| <span class="table-cell-nowrap">innerUpperLimit = *y2*</span> |  |
|  | Specifies the upper limit of the inner integral if this limit is fixed, i.e., if it is not a function of x. See the innerUpperFunc keyword if you need to specify a function for this limit. |
| <span class="table-cell-nowrap">innerLowerFunc = *y1Func*</span> |  |
|  | Specifies a user-defined function for the lower limit of the inner integral. See ***The Limit Functions*** below. |
| <span class="table-cell-nowrap">innerUpperFunc = *y2Func*</span> |  |
|  | Specifies a user-defined function for the upper limits of the inner integral. See ***The Limit Functions*** below. |
| <span class="table-cell-nowrap">outerLowerLimit = *x1*</span> |  |
|  | Specifies the lower limit of the outer integral. |
| <span class="table-cell-nowrap">outerUpperLimit = *x2*</span> |  |
|  | Specifies the upper limit of the outer integral. |
| <span class="table-cell-nowrap">paramWave = *pWave*</span> |  |
|  | Specifies a wave to be passed to the various user-defined functions as the pWave parameter. The wave may contain any number of values that you might need to evaluate the integrand or the integration limits. |
|  | If you omit paramWave then the pWave parameter to the functions will be NULL. |
| <span class="table-cell-nowrap">srcWave = *mWave*</span> |  |
|  | If you need to perform 2D integration of some data, you can specify the data directly instead of providing a user-defined function that returns interpolated data. *mWave* must be a 2D wave. Higher dimensional waves are accepted but only the first layer of the wave is used in the integration. |

### *The Integrand Function* {#the-integrand-function}
Integrate2D computes the general two-dimensional integral of a user-defined integrand function which you specify using the integrand keyword. The integrand function has this form:


```igor
Function integrandFunc(pWave,inX,inY)
	Wave/Z pWave
	Variable inX,inY
	
	... do something
	return result
End
```

The function can have any name - integrandFunc is just an example. The function must take the parameters shown and must return a real numeric result. Returning a NaN terminates the integration.

pWave is a parameter wave that you specify using the *paramWave* keyword. The operation passes this wave on every call to the integrand function. If you omit *paramWave* when invoking Integrate2D then pWave will be NULL.

### *The Limit Functions* {#the-limit-functions}
The limit functions provide lower and/or upper limits of integration for the inner integral if they are functions of x rather than fixed values. You specify a limit function using the innerLowerFunc and/or innerUpperFunc keywords. The form of the limit function is:


```igor
Function limitFunction(pWave,inX)
	Wave/Z pWave
	Variable inX
			
		... do something
	return result
End
```

### *Details* {#details}
The operation computes the general two-dimensional integral of the form

$$
\displaystyle I=\int_{x 1}^{x 2} d x \int_{y 1(x)}^{y 2(x)} f(x, y) d y .
$$

Here y1 and y2 are in general functions of x but could also be simple constants, and f(x,y) is real valued function. The integral is evaluated by considering the "outer" integral

$$
\displaystyle I=\int_{x 1}^{x 2} G(x) d x,
$$

where G(x) is the "inner" integral

$$
\displaystyle G(x)=\int_{y 1(x)}^{y 2(x)} f(x, y) d y .
$$

The operation allows you to specify different algorithms for integrating the inner and outer integrals. The simplest integration algorithm is the Trapezoidal method. You can typically improve on the accuracy of the calculation using Romberg integration and the performance of Gaussian quadrature depends significantly on the nature of the integrand.

### *Example 1: Integrating a 2D function over fixed limits* {#example-1-integrating-a-2d-function-over-fixed-limits}
Suppose we wanted to check the normalization of the built-in two-dimensional Gauss function. The user-defined function would be:


```igor
Function myIntegrand1(pWave,inX,inY)
	Wave/Z pWave
	Variable inX,inY
	return Gauss(inX,50,10,inY,50,10)
End
```

To perform the integration, execute:


```igor
Integrate2D outerLowerLimit=0, outerUpperLimit=100, innerLowerLimit=0, innerUpperLimit=100, integrand=myIntegrand1 
Print/D V_Value
```

### *Example 2: Integrating a 2D function using function limits* {#example-2-integrating-a-2d-function-using-function-limits}
In this example we compute the volume of a sphere of radius 1. To do so we use symmetry and integrate the volume in one octant only. The limits of integration are [0,1] in the x direction and [0,sqrt(1-x^2)] in the y direction. In this case we need to define two user-defined functions: one for the integrand and one for the upper limit of the inner integral:


```igor
Function myIntegrand2(pWave,inX,inY)
	Wave/Z pWave
	Variable inx,iny
	Variable r2=inX^2+inY^2
	if(r2>=1)
		return 0
	else
		return sqrt(1-r2)
	endif
End

Function y2Func(pWave,inX)
	Wave/Z pWave
	Variable inX
	return sqrt(1-inX^2)
End
```

To perform the integration, execute:


```igor
Integrate2D outerLowerLimit=0, outerUpperLimit=1, innerLowerLimit=0, innerUpperFunc=y2Func, integrand=myIntegrand2 
Print/D 4*pi/3 -8*V_Value 	// Calculation error
```

Note that the integrand function tests that r2 does not exceed 1. This is because the sqrt function would return a NaN if r2>1 which can happen due to floating point rounding errors. Returning a NaN terminates the integration.

### *Example 3: Integrating a 2D wave using fixed limits* {#example-3-integrating-a-2d-wave-using-fixed-limits}
In this example we compute the volume between the surface defined by the wave my2DWave and the plane z=0 with integration limits [0,1] in the x-direction and [0,2] in the y-direction. For simplicity we set the wave's value to be a constant (pi).


```igor
Make/O/N=(5,9) my2DWave=pi
SetScale/P x 0,0.3,"", my2DWave 
SetScale/P y 0,0.4,"", my2DWave
Integrate2D outerLowerLimit=0,outerupperLimit=1,innerlowerLimit=0,innerUpperLimit=2,srcWave=my2DWave 
Print/D 2*pi-V_Value	// Calculation error
```

### *See Also* {#see-also}
[Integrate](/igorpro/commands/integrate.md), [Differentiate](/igorpro/commands/differentiate.md), [Integrate1D](/igorpro/commands/integrate1d.md), [area](/igorpro/commands/area.md), [areaXY](/igorpro/commands/areaxy.md)