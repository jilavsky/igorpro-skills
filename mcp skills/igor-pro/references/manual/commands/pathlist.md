---
description: "The PathList function returns a string containing a list of symbolic paths selected based on the matchStr parameter."
slug: /commands/pathlist
---

<div className="command-signature">

## <strong>PathList</strong> (<em>matchStr</em>, <em>separatorStr</em>, <em>optionsStr</em>) {#pathlist}

</div>

The PathList function returns a string containing a list of symbolic paths selected based on the *matchStr* parameter.

### *Details* {#details}
For a path name to appear in the output string, it must match *matchStr*. *separatorStr* is appended to each path name as the output string is generated.

PathList works like the WaveList function, except that the *optionsStr* parameter is reserved for future use. Pass "" for it.

### *Examples* {#examples}
When a new experiment is created there is only one path:


```igor
Print PathList("*",";","")
```

Prints the following in the history area:


```
Igor;
```

### *See Also* {#see-also}
[WaveList](/igorpro/commands/wavelist.md) for an explanation of the *matchStr* and *separatorStr* parameters and for examples.