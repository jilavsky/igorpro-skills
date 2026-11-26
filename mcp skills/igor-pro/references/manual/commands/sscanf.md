---
description: "The sscanf operation is useful for parsing text that contains numeric or string data."
slug: /commands/sscanf
---

<div className="command-signature">

## <strong>sscanf</strong>  <em>scanStr</em>, <em>formatStr</em>, <em>var</em> [, <em>var</em> ] {#sscanf}

</div>

The sscanf operation is useful for parsing text that contains numeric or string data. It is based on the C sscanf function and provides a subset of the features available in C.

Here is a trivial sscanf example.

```igor
Variable v1
sscanf "Value= 1.234", "Value= %f", v1
```

This skips the text "Value=" and the following space and then converts the text "1.234" (or whatever number appeared there) into a number and stores it in the local variable v1.

The sscanf operation sets the variable V_flag to the number of values read. You can use this as an initial check to see if the *scanStr* is consistent with your expectations.

:::note
The sscanf operation is supported in user functions only. It is not available using the command line, using a macro or using the Execute operation.
:::

:::note
The C sscanf function employed was designed to work on 8-bit characters. Igor strings are UTF-8 encoded. Unicode character sequences in strings like "•" will work with the %s format, but not as expected with %c or %[]. %c will pickup only the leading byte of the three-byte UTF-8 sequence 0xE2 0x80 0xA2, and %[] will treat each byte separately, leading to undesirable results. See [UTF8CharLength](/igorpro/commands/utf8charlength.md) and [graphemeLength](/igorpro/commands/graphemelength.md) for details.
:::

### *Parameters* {#parameters}

*scanStr* contains the text to be parsed.

*formatStr* is a format string which describes how the parsing is to be done.

*formatStr* is followed by the names of one or more local numeric or string variables or NVARs (references to global numeric variables) or SVARs (references to global string variables), which are represented by *var* above.

sscanf can handle a maximum of 100 *var* parameters.

### *Details* {#details}
The format string consists of the following:

- Normal text, which is anything other than a percent sign ("%") or white space.
- White space (spaces, tabs, linefeeds, carriage returns).
- A percent ("%") character, which is the start of a conversion specification.

The trivial example illustrates all three of these components.


```igor
Variable v1
sscanf "Value= 1.234", "Value= %f", v1
```

sscanf attempts to match normal text in the format string to the identical normal text in the scan string. In the example, the text "Value=" in the format string skips the identical text in the scan string.

sscanf matches a single white space character in the format string to 0 or more white space characters in the scan string. In the example, the single space skips the single space in the scan string.

When sscanf encounters a percent character in the format string, it attempts to convert the corresponding text in the scan string into a number or string, depending on the conversion character following the percent, and stores the resulting number or string in the corresponding variable in the parameter list. In the example, "%f" tells sscanf to convert the text "1.234" into a number which it stores in the local variable v1.

A conversion specification consists of:

- A percent character ("%").
- An optional "\*", which is a conversion suppression character.
- An optional number, which is a maximum field width.
- A conversion character, which specifies how to interpret text in the scan string.

Don't worry about the suppression character and the maximum width specification for now. They will be explained later.

Igor's sscanf operation supports a subset of the conversion characters supported by the C sscanf operation. The supported conversion characters, which are case-sensitive, are:

|  |  |
| --- | --- |
| d | Converts text representing a decimal number into an integer numeric value. |
| i | Converts text representing a decimal, octal or hexadecimal number into an integer value. If the text starts with "0x" (zero-x), it is interpreted as hexadecimal. Otherwise, if it starts with "0" (zero), it is interpreted as octal. Otherwise it is interpreted as decimal. |
| o | Converts text representing an octal number into an integer numeric value. |
| u | Converts text representing an unsigned decimal number into an integer numeric value. |
| x | Converts text representing a hexadecimal number into an integer numeric value. |
| c | Converts a single character into an integer value which is the ASCII code representing that character. |
| e | Converts text representing a decimal number into a floating point numeric value. |
| f | Same as e. |
| g | Same as e. |
| s | Stores text up to the next white space into a string. |
| [ | Stores text that matches a list of specific characters into a string. The list consists of the characters inside the brackets ("%[abc]"). If the first character is "^", this means to match any character that is not in the list. You can specify a range of characters to match. For example "%[A-Z]" matches all of the upper case letters and "%[A-Za-z]" matches all of the upper and lower case letters. |

Here are some simplified examples to illustrate each of these conversions.


```igor
Variable v1
String s1

// Convert text representing a decimal number to an integer value.
sscanf "1234", "%d", v1

// Convert text representing a decimal, octal, or hex number.
sscanf "1.234", "%i", v1	// Convert from decimal.
sscanf "01234", "%i", v1	// Convert from octal.
sscanf "0x123", "%i", v1	// Convert from hex.

// Convert text representing an octal number.
sscanf "1234", "%o", v1

// Convert text representing an unsigned decimal number.
sscanf "1234", "%u", v1

// Convert text representing a hex number.
sscanf "1FB9", "%x", v1

// Convert a single ASCII character.
sscanf "A", "%c", v1

// Convert text representing a decimal number to an floating point value.
sscanf "1.234", "%e", v1
sscanf "1.234", "%f", v1
sscanf "1.234", "%g", v1

// Copy a string of text up to the first white space.
sscanf "Hello There", "%s", s1

// Copy a string of text matching the specified characters.
sscanf "+4.27", "%[+-]", s1
```

In a C program, you will sometimes see the letters "l" (ell) or "h" between the percent and the conversion character. For example, you may see "%lf" or "%hd". These extra letters are not needed or tolerated by Igor's sscanf operation.

When sscanf matches the format string to the scan string, it reads from the scan string until a character that would be inappropriate for the section of the format string that sscanf is trying to match. In the following example, sscanf stops reading characters to be converted into a number when it hits the first character that is not appropriate for a number.


```igor
Variable v1
String s1, s2
sscanf "1234Volts DC", "%d%s %s", v1, s1, s2
```

sscanf stops matching text for "%d" when it hits "V" and stores the converted number in v1. It stops matching text for the first "%s" when it hits white space and stores the matched text in s1. It then skips the space in the scan string because of the corresponding space in the format string. Finally, it matches the remaining text to the second "%s" and stores the text in s2.

The maximum field width must appear just before the conversion character ("d" in this case).


```igor
Variable v1, v2
sscanf "12349876", "%4d%4d", v1, v2
```

The suppression character ("*") is used in a conversion specification to skip values in the scan string. It parses the value, but sscanf does not store the value in any variable. In the following example, we read one number into local variable v1, skip a colon, and read another number into local variable v2, skip a colon, and read another number into local variable v3.


```igor
Variable v1, v2, v3
sscanf "12:30:45", "%d%*[:]%d%*[:]%d", v1, v2, v3
```

Here "%\*[:]" means "read a colon character but don't store it anywhere". The "\*" character must appear immediately after the percent. Note that there is nothing in the parameter list corresponding to the suppressed strings.

If the text in the scan string is not consistent with the text in the format string, sscanf may not read all of the values that you expected. You can check for this using the V_flag variable, which is set to the number of values read. This kind of inconsistency does not cause sscanf to return an error to Igor, which would cause procedure execution to abort. It is a situation that you can deal with in your procedure code.

The sscanf operation returns the following kinds of errors:

- Out-of-memory.
- The number of parameters implied by *formatStr* does not match the number of parameters in the *var* list.
- *formatStr* calls for a numeric variable but the parameter list expects a string variable.
- *formatStr* calls for a string variable but the parameter list expects a numeric variable.
- *formatStr* includes an unsupported, unknown or incorrectly constructed conversion specification.

The *var* list references a global variable that does not exist.

### *Examples* {#examples}
Here is a simple example to give you the general idea:

```igor
Function SimpleExample()
	Variable v1, valuesRead
	sscanf "Value=1.234", "Value=%g", v1
	valuesRead = V_flag
	if (valuesRead != 1)
		Printf "Error: Expected 1 value, got %d values\r", valuesRead
	else
		Printf "Value read = %g\r", v1
	endif
End
```

For an example that uses sscanf to load data from a text file, see the Load File Demo example experiment in "Igor Pro Folder:Examples:Programming".

### *See Also* {#see-also}
[str2num](/igorpro/commands/str2num.md), [strsearch](/igorpro/commands/strsearch.md), [stringmatch](/igorpro/commands/stringmatch.md), [SplitString](/igorpro/commands/splitstring.md), [UTF8CharLength](/igorpro/commands/utf8charlength.md), [graphemeLength](/igorpro/commands/graphemelength.md)