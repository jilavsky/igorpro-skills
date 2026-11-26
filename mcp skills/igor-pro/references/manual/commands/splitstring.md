---
description: "The SplitString operation uses the regular expression regExprStr,to split str,into subpatterns. See Subpatterns for details."
slug: /commands/splitstring
---

<div className="command-signature">

## <strong>SplitString</strong>  /E=<em>regExprStr</em> <em>str</em> , <em>substring1</em> [, <em>substring2</em>, ... <em>substringN</em>] {#splitstring}

</div>

The SplitString operation uses the regular expression *regExprStr*,to split *str*,into subpatterns. See [Subpatterns](/igorpro/programming/programming-techniques.md#subpatterns) for details. Each matched subpattern is returned sequentially in the corresponding substring parameter.

### *Parameters* {#parameters}
*str*,is the input string to be split into subpatterns.

The *substring1*...*substringN*,output parameters must be the names of existing string variables if you need to use the matched subpatterns. The first matched subpattern is returned in *substring1*, the second in *substring2*, etc.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/E = *regExprStr*</span> | Specifies the Perl-compatible regular expression string containing subpattern definition(s). |

### *Details* {#details}
*regExprStr*,is a regular expression with successive subpattern definitions, such as shown in the examples. (Subpatterns are regular expressions within parentheses.)

For unmatched subpatterns, the corresponding substring is set to "". If you specify more substring parameters than subpatterns, the extra parameters are also set to "".

The number of matched subpatterns is returned in V_flag.

The part of *str*,that matches *regExprStr*,(often all of *str* ) is stored in S_value.

### *Examples* {#examples}

```igor
// Split the output of the date() function:
Print date()
  Mon, May 2, 2005

String expr="([[:alpha:]]+), ([[:alpha:]]+) ([[:digit:]]+), ([[:digit:]]+)"
String dayOfWeek, monthName, dayNumStr, yearStr
SplitString/E=(expr) date(), dayOfWeek, monthName, dayNumStr, yearStr
Print V_flag
  4
Print dayOfWeek
  Mon
Print monthName
  May
Print dayNumStr
  2
Print yearStr
  2005
Print S_value
  Mon, May 2, 2005

// Get the part of str that matches regExprStr
SplitString/E=",.*," "stuff in front,second value,stuff at end"
Print S_value
  ,second value,
```

### *See Also* {#see-also}
[Regular Expressions](/igorpro/programming/programming-techniques.md#regular-expressions), [Subpatterns](/igorpro/programming/programming-techniques.md#subpatterns)

[sscanf](/igorpro/commands/sscanf.md), [Grep](/igorpro/commands/grep.md), [strsearch](/igorpro/commands/strsearch.md), [str2num](/igorpro/commands/str2num.md), [RemoveEnding](/igorpro/commands/removeending.md), [TrimString](/igorpro/commands/trimstring.md)