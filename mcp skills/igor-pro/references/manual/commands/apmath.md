---
description: "The APMath operation provides arbitrary precision calculation of basic mathematical expressions."
slug: /commands/apmath
---

<div className="command-signature">

## <strong>APMath</strong>  [/EX=<em>exDigits</em> /N=<em>numDigits</em> /V/Z] <em>destStr</em> = <em>Expression</em> {#apmath}

</div>

The APMath operation provides arbitrary precision calculation of basic mathematical expressions. It converts the final result into the assigned string *destStr*, which can then be printed or used to represent a value (at the given precision) in another APMath operation.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *destStr* | Specifies a destination string for the assignment expression. If *destStr*  is not an existing variable, it is created by the operation. When executing in a function, *destStr*  will be a local variable if it does not already exist. |
| *Expression* | Algebraic expression containing constants, local, global, and reference variables or strings, as well as wave elements together with the following operators: |
|  |<table class="nested-table"><tbody><tr><td>**Operator**</td><td>**Precedence**</td></tr><tr><td>^</td><td>Highest</td></tr><tr><td>\*&nbsp;&nbsp;/</td><td>...</td></tr><tr><td>+&nbsp;&nbsp;\-</td><td>Lowest</td></tr></tbody></table>

### *Operators* {#operators}
Supported operators are:


|  |  |
| --- | --- |
| + | scalar addition |
| \- | scalar subtraction |
| \* | scalar multiplication |
| / | scalar division |
| ^ | exponentiation |

### *APMath Functions With Scalar Parameters* {#apmath-functions-with-scalar-parameters}
The following functions are supported for arbitrary precision math on scalar parameters:

|  |  |
| --- | --- |
| sqrt(*x*) | square root of *x* |
| cbrt(*x*) | cube root of *x* |
| pi | does not require parentheses |
| sin(*x*) | sine of *x* |
| cos(*x*) | cosine of *x* |
| tan(*x*) | tangent of *x* |
| asin(*x*) | inverse sine of *x* |
| acos(*x*) | inverse cosine of *x* |
| atan(*x*) | inverse tangent of *x* |
| atan2(*y*,*x*) | inverse tangent of *y*/*x* |
| log(*x*) | logarithm of *x* |
| log10(*x*) | logarithm based 10 of *x* |
| exp(*x*) | exponential function e^*x* |
| pow(*x*,*n*) | *x*  to the power *n* (*n* not necessarily integer) |
| sinh(*x*) | hyperbolic sine of *x* |
| cosh(*x*) | hyperbolic cosine of *x* |
| tanh(*x*) | hyperbolic tangent of *x* |
| asinh(*x*) | inverse hyperbolic sine of *x* |
| acosh(*x*) | inverse hyperbolic cosine of *x* |
| atanh(*x*) | inverse hyperbolic tangent of *x* |
| ceil(*x*) | Returns the smallest integer larger than *x* |
| comp(*x*,*y*) | Returns 0 for *x* == *y*, 1 if *x* > *y*  and -1 if *y* > *x* |
| factorial(*n*) | factorial of integer *n* |
| floor(*x*) | Returns the greatest integer smaller than *x* |
| gcd(*x*,*y*) | Returns the greatest common divisor of *x*  and *y* |
| lcd(*x*,*y*) | Returns the lowest common denominator of *x*  and *y* (given by *x*\**y*/gcd(*x*,*y*) |
| sgn(*x*) | Returns the sign of *x*  or zero if *x* == 0 |
| binomial(*n*,*k*) | Returns the the binomial function for integers *n* and *k* |
| Bernoulli(*n*) | Returns the Bernoulli number Bn (with Bn(1)=-1/2) |
| Stirling2(*n*,*k*) | Returns the Stirling number of the second kind |

### *APMath Functions With Wave Parameters* {#apmath-functions-with-wave-parameters}
The following functions are supported for arbitrary precision math on waves.

These restrictions apply to all of these APMath functions on waves:

1.	The parameter *w* must be a simple wave reference. It cannot be a data folder path to a wave or a $ expression pointing to a wave.
2.	The wave can be a real numeric wave or a text wave containing arbitrary precision numbers in string form.
3.	Complex waves are not allowed.
4.	64-bit integer waves are not allowed.
5.	The functions return an error if the wave contains NaNs or INFs.
6.	Multidimensional waves are treated as 1D.


|  |  |
| --- | --- |
| kurtosis(w) | Returns the kurtosis of the entire wave *w*. See [WaveStats](/igorpro/commands/wavestats.md) for a discussion of kurtosis. The kurtosis function was added in Igor Pro 8.00. |
| mean(w) | Returns the mean of the entire wave *w*. The mean function was added in Igor Pro 8.00. |
| skew(w) | Returns the skewness of the entire wave *w*. See [WaveStats](/igorpro/commands/wavestats.md) for a discussion of skewness. The skew function was added in Igor Pro 8.00. |
| sum(*w*) | Returns the sum of the entire wave *w*. The sum function was added in Igor Pro 8.00. |
| variance(w) | Returns the variance of the entire wave *w*. See [WaveStats](/igorpro/commands/wavestats.md) for a discussion of variance. The variance function was added in Igor Pro 8.00. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/EX = *exDigits*</span> | Specifies the number of extra digits added to the precision digits (/N) for intermediate steps in the calculation. |
| <span class="table-cell-nowrap">/N = *numDigits*</span> | Specifies the precision of the final result. To add digits to the intermediate computation steps, use /EX. |
| <span class="table-cell-nowrap">/V</span> | Verbose mode; prints the result in the history in addition to performing the assignment. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
By default, all arbitrary precision math calculations are performed with *numDigits* =50 and *exDigits* =6, which yields a final result using at least 56 decimal places. Because none of the built-in variable types can express numbers with such high accuracy, the arbitrary precision numbers must be stored as strings. The operation automatically converts between strings and constants. It evaluates all of the numerical functions listed above using the specified accuracy. If you need functions that are not supported by this operation, you may have to precompute them and store the results in a local variable.

The operation stores the result in *destStr*, which may or may not exist prior to execution. When you execute the operation from the command line, *destStr*  becomes a global string in the current data folder if it does not already exist. If it exists, then the result of the operation overwrites its value (as with any normal string assignment). In a user function, *destStr*  can be a local string, an SVAR, or a string passed by reference. If *destStr*  is not one of these then the operation creates a local string by that name.

Arbitrary precision math calculations are much slower (by a factor of about 300) than equivalent floating point calculations. Execution time is a function of the number of digits, so you should use the /N flag to limit the evaluation to the minimum number of required digits.

### *Output Variables* {#output-variables}
In Igor Pro 8.00 or later, the APMath operation returns information in the following variables:


|  |  |
| --- | --- |
| V_Flag | Set to 0 if the operation succeeded or to a non-zero error code. |
| V_value | Set to a double-precision representation of the output string. |

### *Examples* {#examples}
Evaluate pi to 50 digits:


```igor
APMath/V aa = pi
```

Evaluate ratios of large factorials:


```igor
APMath/V aa = factorial(500)/factorial(499)
```

Evaluate ratios of large exponentials:


```igor
APMath/V aa = exp(-1000)/exp(-1001)
```

Division of mixed size values:


```igor
APMath/V aa = 1-sgn(1-(1-0.00000000000000000001234)/(1-0.000000000000000000012345)))
```

you'll get a different result trying to evaluate this using double precision.

Difference between built-in pi and the arbitrary precision pi:


```igor
Variable/G biPi = pi
APMath/V aa = biPi-pi
```

Precision control:


```igor
Function test()
   APMath aa = pi                // Assign 50 digit pi to the string aa.
   APMath/V bb = aa              // Create local string bb equal to aa.
   APMath/V bb = aa-pi           // Subtract arb. prec. pi from aa.
                                 // note the default exDigits=6.
   APMath/V/N=50/ex=0 bb = aa-pi // setting exDigits=0.
End
```

Numerical recreation:


```igor
APMath/V/N=16  aa = 111111111^2
```

The solution for the sum of three cubes problem for the number 42:


```igor
APMath/V aa = pow((-80538738812075974),3)+pow(80435758145817515,3)+pow(12602123297335631,3)
```