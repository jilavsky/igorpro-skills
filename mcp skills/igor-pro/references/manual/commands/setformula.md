---
description: "The SetFormula operation binds the named wave, numeric or string variable to the expression or, if the expression is \"\", unbinds it from any previous…"
slug: /commands/setformula
---

<div className="command-signature">

## <strong>SetFormula</strong>  <em>waveOrVariableName</em>, <em>expressionStr</em> {#setformula}

</div>

The SetFormula operation binds the named wave, numeric or string variable to the expression or, if the expression is "", unbinds it from any previous expression. In user functions, SetFormula must be used to create dependencies.

### *Parameters* {#parameters}
*expressionStr*  is a string containing a numeric or string expression, depending on the type of the bound object.

Pass an empty string ("") for *expressionStr*  to clear any previous dependency expression associated with the wave or variable.

### *Details* {#details}
The dependent object (the wave or variable) will depend on the objects referenced in the string expression. The expression will be reevaluated any time an object referred to in the expression is modified.

Besides being set from a string expression this differs from just typing:


```igor
name := expression
```

in that syntax errors in *expressionStr*  are not reported and are not fatal. You just end up with a dependency assignment that is marked as needing to be recompiled. The recompilation will be attempted every time an object is created or when the procedure window is recompiled.

Use the Object Status dialog in the Misc menu to check up on dependent objects.

### *Examples* {#examples}
This command makes the variable v_sally dependent on the user-defined function anotherFunction, waves wave_fred and wave_sue, and the system variable K2:


```igor
SetFormula v_sally, "anotherFunction(wave_fred[1]) + wave_sue[0] + K2"
```

This is equivalent to:


```igor
v_sally := anotherFunction(wave_fred[1]) + wave_sue[0] + K2
```

except that no error will be generated for the SetFormula if, for instance, wave_fred does not exist.

A string variable dependency can be created by a command such as:


```igor
SetFormula myStringVar, "note(wave_joe)"
```

observe that *expressionStr*  is a string *containing*  a string expression, and that:


```igor
SetFormula myStringVar,note(wave_joe)
```

is not the same thing. In this case the note of *wave_joe* would contain the expression that *myStringVar* would depend on! Also, *wave_joe* would have to exist for Igor to understand the statement.

### *See Also* {#see-also}
[Dependencies](/igorpro/programming/dependencies.md)

[GetFormula](/igorpro/commands/getformula.md)