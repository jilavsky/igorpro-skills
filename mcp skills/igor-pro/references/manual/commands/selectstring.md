---
description: "The SelectString function returns one of str1, str2, or (optionally) str3 based on the value of whichOne."
slug: /commands/selectstring
---

<div className="command-signature">

## <strong>SelectString</strong> (<em>whichOne</em> , <em>str1</em>, <em>str2</em>  [, <em>str3</em> ]) {#selectstring}

</div>

The SelectString function returns one of *str1*, *str2*, or (optionally) *str3* based on the value of *whichOne*.

SelectString(*whichOne*, *str1*, *str2* ) returns *str1* if whichOne is zero, else it returns *str2*.

SelectString(*whichOne*, *str1*, *str2* , *str3*) returns *str1* if *whichOne* is negative, *str2* if *whichOne* is zero, or *str3* if *whichOne* is positive.

### *Details* {#details}
If *whichOne* is NaN, then ""  is returned.

*WhichOne* must always be a real value.

Unlike the ? : conditional operator, SelectString always evaluates all of the string expression parameters *str1*, *str2*, ...

SelectString works in a macro, whereas the conditional operator does not.

### *Examples* {#examples}

```igor
Print SelectString(0,"hello","there")           // prints "hello"
Print SelectString(1,"hello","there")           // prints "there"
Print SelectString(-3,"hello","there","jack")   // prints "hello"
Print SelectString(0,"hello","there","jack")    // prints "there"
Print SelectString(100,"hello","there","jack")  // prints "jack"
```

### *See Also* {#see-also}
[SelectNumber](/igorpro/commands/selectnumber.md), [Working With Strings[String Expressions]](/igorpro/programming/commands.md#string-expressions), [Operator Reference[? :]](/igorpro/programming/operators/operator-reference.md#conditional).