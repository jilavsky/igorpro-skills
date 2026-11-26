---
description: "\\+ produces the sum of two numbers or waves. It can also be used to concatenate strings."
slug: /programming/operators/operator-reference
---

<!-- IgorOperator -->
## + {#plus}

\+ produces the sum of two numbers or waves.

It can also be used to concatenate strings.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## - {#minus}

\- produces the difference of two numbers or waves.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## \* {#multiply}

\* produces the product of two numbers or waves.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## / {#divide}

/ produces the quotient of two numbers or waves.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## ^ {#exponent}

^ Raises a number or wave to a power.

For example, `wave1 = wave2^3` sets wave1 equal to the cube of wave2. In an expression a^b, if result is used in a real expression, *a* must not be negative if *b* is not an integer. If result is used in a complex expression, *a* and *b* may be any combination of negative, fractional, and complex numbers.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## ! {#logical-negation}

! is the logical negation operator.

The number zero is considered false and any nonzero number is considered true. ! changes 0 (false) to 1 (true) and any nonzero number (true) to 0 (false).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## && {#logical-and}

&& is the logical AND operator.

Evaluates the truth or falseness of a pair of expressions; returns true only if both are true.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## \|\| {#logical-or}

\|\| is the logical OR operator.

Evaluates the truth or falseness of a pair of expressions; returns true if either one is true.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## & {#bitwise-and}

& is the bitwise AND operator.

Produces the bitwise AND of its two operands after converting them to integers. See also [Using Bitwise Operators](/igorpro/programming/programming.md#using-bitwise-operators).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## \| {#bitwise-or}
\| (vertical bar) is the bitwise OR operator.

Produces the bitwise OR of its two operands after converting them to integers. See also Using Bitwise Operators.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## %^ {#bitwise-xor}

%^ is the bitwise exclusive OR operator.

Produces the bitwise exclusive OR of its two operands after converting them to integers. See also [Using Bitwise Operators](/igorpro/programming/programming.md#using-bitwise-operators).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## ~ {#bitwise-complement}

~ is the bitwise COMPLEMENT operator. It produces the bitwise COMPLEMENT of its single operand after converting it to integer. See also [Using Bitwise Operators](/igorpro/programming/programming.md#using-bitwise-operators).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## ? : {#conditional}

? : is the conditional operator, which is a shorthand form of an if-else-endif statement. It is of the form: 

```
<numeric expression> ? <TRUE> : <FALSE>  
```

When the numeric expression is nonzero, it evaluates the TRUE part, otherwise it evaluates the FALSE part. The ":" character must always be separated with spaces from the two adjacent parts.

> Before Igor 10.04, the TRUE and FALSE parts had to be numeric; for strings, you had to use the [SelectString](/igorpro/commands/selectstring.md) function.
>
> In Igor 10.04 and later, the TRUE and FALSE parts can also be string expressions (when the result is expected to be a string expression).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

### *Examples* {#examples}

Replace zero values with blanks:

```igor
Wave w = wave0
w = w[p]==0 ? NaN : w[p]
```

### *See Also* {#see-also}
[SelectNumber](/igorpro/commands/selectnumber.md), [SelectString](/igorpro/commands/selectstring.md), [If-Else-Endif Statements](/igorpro/programming/programming.md#if-else-endif-statements)

<!-- IgorOperator -->
## == {#equals-equals}

== takes a left hand operand and a right hand operand, both of which are scalar numbers. It returns true (1) if the operands are equal or false (0) if they are not.

Comparison operators do not work with NaN parameters. Use [numtype](/igorpro/commands/numtype.md) to test if a value is NaN.

Comparison operators can be useful in synthesizing waves. See [Example: Comparison Operators and Wave Synthesis](/igorpro/igor-basics/waves.md#example-comparison-operators-and-wave-synthesis).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## != {#not-equals}

!= takes a left hand operand and a right hand operand, both of which are scalar numbers. It returns true (1) if the operands are not equal or false (0) if they are equal.

Comparison operators do not work with NaN parameters. Use [numtype](/igorpro/commands/numtype.md) to test if a value is NaN.

Comparison operators can be useful in synthesizing waves. See [Example: Comparison Operators and Wave Synthesis](/igorpro/igor-basics/waves.md#example-comparison-operators-and-wave-synthesis).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## \>= {#greater-equals}

\>= takes a left hand operand and a right hand operand, both of which are scalar numbers. It returns true (1) if the left operand is greater than or equal to the right operand or false (0) otherwise.

Comparison operators can be useful in synthesizing waves. See [Example: Comparison Operators and Wave Synthesis](/igorpro/igor-basics/waves.md#example-comparison-operators-and-wave-synthesis).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## \> {#greater}

\> takes a left hand operand and a right hand operand, both of which are scalar numbers. It returns true (1) if the left operand is greater than the right operand or false (0) otherwise.

Comparison operators can be useful in synthesizing waves. See [Example: Comparison Operators and Wave Synthesis](/igorpro/igor-basics/waves.md#example-comparison-operators-and-wave-synthesis).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## <= {#less-equals}

<= takes a left hand operand and a right hand operand, both of which are scalar numbers. It returns true (1) if the left operand is less than or equal to the right operand or false (0) otherwise.

The comparison operators can be useful in synthesizing waves. See [Example: Comparison Operators and Wave Synthesis](/igorpro/igor-basics/waves.md#example-comparison-operators-and-wave-synthesis).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

<!-- IgorOperator -->
## < {#less}

< takes a left hand operand and a right hand operand, both of which are scalar numbers. It returns true (1) if the left operand is less than the right operand or false (0) otherwise.

Comparison operators can be useful in synthesizing waves. See [Example: Comparison Operators and Wave Synthesis](/igorpro/igor-basics/waves.md#example-comparison-operators-and-wave-synthesis).

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

### *See Also* {#less-see-also}
[Operators](/igorpro/programming/commands.md#operators), [Assignment Operators](/igorpro/programming/commands.md#assignment-operators), [Waveform Arithmetic and Assignment](/igorpro/igor-basics/waves.md#waveform-arithmetic-and-assignment), [Example: Comparison Operators and Wave Synthesis](/igorpro/igor-basics/waves.md#example-comparison-operators-and-wave-synthesis)

<!-- IgorOperator -->
## \+\+ {#increment}

\+\+ increments its operand. It works on both local (Igor Pro 7 or later) and global variables (Igor Pro 10.03 and later) in user-defined functions.

\+\+ may appear before its operand in which case it is called a pre-increment operator and returns the value of the operand after it is incremented.

\+\+ may also appear after its operand in which case it is called a post-increment operator and returns the value of the operand before it is incremented.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

### *Examples* {#increment-examples}

```igor
Function Test()
	Variable operand
	operand = 1
	Variable result = ++operand	// result = 2, operand = 2
	operand = 1
	Variable result = operand++	// result = 1, operand = 2
End
```

<!-- IgorOperator -->
## \-\- {#decrement}

\-\- decrements its operand. It works on both local (Igor Pro 7 or later) and global variables (Igor Pro 10.03 and later) in user-defined functions.

\-\- may appear before its operand in which case it is called a pre-decrement operator and returns the value of the operand after it is decremented.

\-\- may also appear after its operand in which case it is called a post-decrement operator and returns the value of the operand before it is decremented.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

### *Examples* {#decrement-examples}

```igor
Function Test()
	Variable operand
	operand = 1
	Variable result = --operand	// result = 0, operand = 0
	operand = 1
	Variable result = operand--	// result = 1, operand = 0
End
```

<!-- IgorOperator -->
## << {#left-shift}

<< is the bitwise left shift operator. It returns the value of its lefthand operand shifted left by the number of bits specified by its righthand operand. It requires Igor Pro 7 or later.
<< converts its lefthand operand to an integer by truncation before doing the shifting.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

### *Examples* {#left-shift-examples}

```igor
Function Test()
	Variable val = 2
	Variable result = val << 1	// result = 4
End
```

<!-- IgorOperator -->
## \>\> {#right-shift}
\>\> is the bitwise right shift operator. It returns the value of its lefthand operand shifted right by the number of bits specified by its righthand operand. It requires Igor Pro 7 or later.
\>\> converts its lefthand operand to an integer by truncation before doing the shifting.

See [Operators](/igorpro/programming/commands.md#operators) for a list of all operators in order of precedence.

### *Examples* {#right-shift-examples}

```igor
Function Test()
	Variable val = 2
	Variable result = val >> 1	// result = 1
End
```