---
description: "The CmpStr function returns zero if str1 is equal to str2 or non-zero otherwise."
slug: /commands/cmpstr
---

<div className="command-signature">

## <strong>CmpStr</strong> (<em>str1</em>, <em>str2</em> [, <em>flags</em> ]) {#cmpstr}

</div>

The CmpStr function returns zero if *str1* is equal to *str2* or non-zero otherwise.

### *Parameters* {#parameters}
*flags* controls the type of comparison that is done. It defaults to 0 and supports the following values:

|  |  |
| --- | --- |
| 0: | Case-insensitive text comparison |
| 1: | Case-sensitive text comparison |
| 2: | Binary comparison |

Binary comparison (*flags*=2) was added Igor Pro 7.05 and is appropriate if *str1* and *str2* contain binary data, which may contain null bytes (bytes with the value 0), rather than human-readable strings.

### *Details* {#details}
If *flags* is omitted, 0, or 1, CmpStr does a text comparison and returns the following values:

|  |  |
| --- | --- |
| -1: | *str1* is alphabetically before *str2* |
| 0: | *str1* and *str2* are equal |
| 1: | *str1* is alphabetically after *str2* |

The alphabetic order represented by -1 and 1 is valid only for ASCII text. It is not valid for non-ASCII text, such as text containing accented characters.

If *flags* is 2, CmpStr does a binary comparison and returns the following values:

|  |  |
| --- | --- |
| 0: | *str1* and *str2* are equal |
| 1: | *str1* and *str2* are not equal |

Usually strings do not contain null bytes. Text comparison treats a null byte as meaning "end of string". Binary comparison does not treat a null byte specially. The example below illustrates the treatment of null bytes.

### *Example* {#example}

```igor
Function TestCmpStr()
	String str1 = "A" + num2char(0) + "B"   // num2char(0) is a null byte
	Print strlen(str1)                      // Prints 3
	
	String str2 = "A" + num2char(0) + "C"
	Print strlen(str2)                      // Prints 3
	
	Print CmpStr(str1,str2,0)               // Prints 0 meaning "equal"
	Print CmpStr(str1,str2,1)               // Prints 0 meaning "equal"
	Print CmpStr(str1,str2,2)               // Prints 1 meaning "unequal"
End
```

The "Print strlen" statements illustrate that strlen does not treat null as meaning end of string.

The results from CmpStr with *flags* =0 and *flags* =1 illustrate that CmpStr treated null as meaning "end of string" and consequently compared only the first byte of *str1* to the first byte of *str2* . Both are "A" so CmpStr returned 0 meaning "equal".

The result from CmpStr with *flags* =2 illustrates that CmpStr did not treat null as meaning "end of string" and consequently compared all three bytes of *str1* to all three bytes of *str2*. The third bytes do not match so CmpStr returned 1 meaning "unequal".

### *See Also* {#see-also}
[ReplaceString](/igorpro/commands/replacestring.md), [Using Strings](/igorpro/programming/programming-techniques.md#using-strings)