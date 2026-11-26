---
description: "The SelectNumber function returns one of val1, val2, or (optionally) val3 based on the value of whichOne."
slug: /commands/selectnumber
---

<div className="command-signature">

## <strong>SelectNumber</strong> (<em>whichOne</em>, <em>val1</em>, <em>val2</em> [, <em>val3</em>]) {#selectnumber}

</div>

The SelectNumber function returns one of *val1*, *val2*, or (optionally) *val3* based on the value of *whichOne* .

SelectNumber(*whichOne*, *val1*, *val2* ) returns *val1* if whichOne is zero, else it returns *val2*.

SelectNumber(*whichOne*, *val1*, *val2* , *val3* ) returns *val1* if *whichOne* is negative, *val2* if *whichOne* is zero, or *val3* if *whichOne* is positive.

### *Details* {#details}
SelectNumber works with complex (or real)*val1*, *val2*, and *val3* when the result is assigned to a complex wave or variable. (Print expects a real result, see the "causes error" example, below).

If *whichOne* is NaN, then NaN  is returned.

*WhichOne* must always be a real value.

Unlike the ? : conditional operator, SelectNumber always evaluates all of the numeric expression parameters *val1*, *val2*, ...

SelectNumber works in a macro, whereas the conditional operator does not.

### *Examples* {#examples}

```igor
Print SelectNumber(0,1,2)                   // prints 1
Print SelectNumber(0,1,2,3)                 // prints 2
wv= SelectNumber(numtype(wv[p])==2,wv[p],0) // replaces NaN's with zeros

// chooses among complex values
Variable/C cx= SelectNumber(negZeroPos,cmplx(-1,-1),0,cmplx(1,1))

// causes error because Print expects a real value (not complex)
Print SelectNumber(negZeroPos,cmplx(-1,-1),0,cmplx(1,1))

// The real function expects a complex result
Print real(SelectNumber(negZeroPos,cmplx(-1,-1),0,cmplx(1,1)))
```

### *See Also* {#see-also}
[SelectString](/igorpro/commands/selectstring.md), [limit](/igorpro/commands/limit.md), [Operator Reference[? :]](/igorpro/programming/operators/operator-reference.md#conditional)

[Waveform Arithmetic and Assignment](/igorpro/igor-basics/waves.md#waveform-arithmetic-and-assignment)