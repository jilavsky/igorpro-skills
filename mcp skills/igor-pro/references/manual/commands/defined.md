---
description: "The defined function returns 1 if the symbol is defined 0 if the symbol is not defined."
slug: /commands/defined
---

<div className="command-signature">

## <strong>defined</strong> (<em>symbol</em>) {#defined}

</div>

The defined function returns 1 if the symbol is defined 0 if the symbol is not defined.

*symbol* is a symbol possibly created by a #define statement or by [SetIgorOption](/igorpro/commands/setigoroption.md) poundDefine=symbol.

*symbol* is a name, not a string. However you can use $ to convert a string expression to a name.

### *Details* {#details}
The defined function can be used in three ways:

Outside of a procedure using a #if statement

Inside a procedure using a #if statement

Inside a procedure using an if statement

For example:


```igor
#define DEBUG

#if defined(DEBUG)      // Outside of a function with #if
	Constant kSomeConstant = 100
#else
	Constant kSomeConstant = 50
#endif

Function Test1()        // Inside a function with #if
	#if defined(DEBUG)
		Print "Debugging"
	#else
		Print "Not debugging"
	#endif
End

Function Test1()        // Inside a function with if
	if (defined(DEBUG))
		Print "Debugging"
	else
		Print "Not debugging"
	endif
End
```

In these examples, we could have just as well used #ifdef instead of the defined function. For logical combinations of conditions however, only defined will do:


```igor
#if (defined(SYMBOL1) && defined(SYMBOL2)
	. . .
#endif
```

When used in a procedure window, defined(*symbol* ) returns 1 if *symbol* is defined at the time the line is compiled. In a given procedure file, only the following symbols are visible:

Symbols defined earlier in that procedure file \*

Symbols defined in the built-in procedure window †

Predefined symbols (see [Predefined Global Symbols](/igorpro/programming/programming.md#predefined-global-symbols))

Symbols defined by [SetIgorOption](/igorpro/commands/setigoroption.md) poundDefine=symbol

\* When used in the body of a procedure, as opposed to outside of a procedure, a symbol defined anywhere in a given procedure window is visible. However, to avoid depending on this confusing exception, you should define all symbols before they are referenced in a procedure file.

† Symbols defined in the built-in procedure window are not available to independent modules.

When the defined function is used from the command line, only symbols defined in the built-in procedure window, predefined symbols, and symbols defined using SetIgorOption are visible.

### *See Also* {#see-also}
[#define](/igorpro/programming/keywords/other-programming-keywords.md#define), [Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation), [Predefined Global Symbols](/igorpro/programming/programming.md#predefined-global-symbols)