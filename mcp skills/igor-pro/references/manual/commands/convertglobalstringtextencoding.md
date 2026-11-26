---
description: "The ConvertGlobalStringTextEncoding operation converts the contents of the specified global string variables or the contents of all global string variables in…"
slug: /commands/convertglobalstringtextencoding
---

<div className="command-signature">

## <strong>ConvertGlobalStringTextEncoding</strong>  [<em>flags</em> ] <em>originalTextEncoding</em>, <em>newTextEncoding</em> , [<em>string</em> , <em>string</em>, ...] {#convertglobalstringtextencoding}

</div>

The ConvertGlobalStringTextEncoding operation converts the contents of the specified global string variables or the contents of all global string variables in the data folder specified with the /DF flag from one text encoding to another.

The ConvertGlobalStringTextEncoding operation was added in Igor Pro 7.00.

By default, the contents of global string variables containing control characters (codes less than 32) other than carriage return (13), linefeed (10), and tab (9) are *not* converted. To convert the contents of global string variables containing control characters, you must include the /SKIP=0 flag.

Also by default, in Igor Pro 9.00 or later, when converting to UTF-8, strings that are already valid as UTF-8 are skipped.

In Igor Pro 7 or later, the contents of all global string variables are assumed to be encoded as UTF-8. You should convert the text encoding of a global string variable if, for example, you have global string variables in experiments created prior to Igor 7 and they contain non-ASCII characters. For those strings to be displayed and interpreted correctly, their contents need to be converted to UTF-8.

Most users will have no need to worry about the text encoding of Igor global string variables since most global string variables do not contain non-ASCII text. You should not use this operation unless you have a thorough understanding of text encoding issues or are instructed to use it by someone who has a thorough understanding.

See [String Variable Text Encodings](/igorpro/igor-basics/text-encodings.md#string-variable-text-encodings) for essential background information.

ConvertGlobalStringTextEncoding can work on a list of specific global string variables or on all of the global string variables in a data folder (/DF flag). When working on a data folder, it can work on just the data folder itself or recursively on sub-data folders as well.

Conversion does not change the characters that make up text - it merely changes the numeric codes used to represent those characters.

### *Parameters* {#parameters}
*originalTextEncoding*  specifies the original (current) text encoding used by the specified global string variables. See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of codes.

*newTextEncoding*  specifies the output text encoding. See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of codes.

*string* , *string* , ... is a list of the targeted global string variables. Only the name of string variables, not a path specification plus the name, is allowed. Therefore, the string variables must be in the current data folder. The list is optional and must be omitted if you use the /DF flag. Using both the /DF flag and a list of string variables is treated as an error. Use of local string variables in this list is also an error. Use [ConvertTextEncoding](/igorpro/commands/converttextencoding.md) to convert local string variables.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CONV = {*errorMode* [, *diagnosticsFlags* ]}</span> |  |
|  | *errorMode*  determines how ConvertGlobalStringTextEncoding behaves if the conversion cannot be done because the text cannot be mapped to the specified text encoding. This will occur if the text contains characters that cannot be represented in the specified text encoding or if the value of *originalTextEncoding* is wrong. |
|  | *errorMode*  takes one of these values: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Generate error. ConvertGlobalStringTextEncoding returns an error to Igor.</td></tr><tr><td>2:</td><td>Use a substitute character for any unmappable characters. The substitute character for Unicode is the Unicode replacement character, � (U+FFFD). For most non-Unicode text encodings it is either control-Z or a question mark.</td></tr><tr><td>3:</td><td>Skip unmappable input characters. Any unmappable characters will be missing in the output.</td></tr><tr><td>4:</td><td>Use escape sequences representing any unmappable characters or invalid source text.</td></tr><tr><td></td><td>If the source text is valid in the source text encoding but cannot be represented in the destination text encoding, unmappable characters are replaced with \uXXXX where XXXX specifies the UTF-16 code point of the unmappable character in hexadecimal.</td></tr><tr><td></td><td>If the conversion cannot be done because the source text is not valid in the source text encoding, invalid bytes are replaced with \xXX where XX specifies the value of the invalid byte in hexadecimal.</td></tr></tbody></table>
|  | *diagnosticsFlags*  is an optional bitwise parameter defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Emit diagnostic message if text conversion succeeds.</td></tr><tr><td>Bit&nbsp;1:</td><td>Emit diagnostic message if text conversion fails.</td></tr><tr><td>Bit&nbsp;2:</td><td>Emit diagnostic message if text conversion is skipped.</td></tr><tr><td>Bit&nbsp;3:</td><td>Emit summary diagnostic message.</td></tr></tbody></table>
|  | All other bits are reserved for future use. |
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | *diagnosticsFlags*  defaults to 2 (bit 1 set) if the /DF flag is not present and to 10 (bits 1 and 3 set) if the /DF flag is present. |
|  | Text conversion may be skipped because the global string variable's contents are detected as being binary or because *newTextEncoding*  is the same as *originalTextEncoding*. |
| <span class="table-cell-nowrap">/DF = {*dfr*, *recurse*, *excludedDFR* }</span> |  |
|  | *dfr*  is a reference to a data folder. ConvertGlobalStringTextEncoding operates on all global string variables in the specified data folder. If *dfr*  is null ($"") ConvertGlobalStringTextEncoding acts as if /DF was omitted. If the /DF flag is used, the optional string list parameter must not be used. |
|  | If *recurse* is 1, ConvertGlobalStringTextEncoding works recursively on all sub-data folders. Otherwise it affects only the data folder referenced by *dfr*. |
|  | *excludedDFR*  is an optional reference to a data folder to be skipped by ConvertGlobalStringTextEncoding. For example, this command converts the string data for all global string variables in all data folders except for root:Packages and its sub-data folders: |
|  | <code class="igor">ConvertGlobalStringTextEncoding /DF={root:,1,root:Packages} 4, 1</code> |
|  | If *excludedDFR* is null ($"") ConvertGlobalStringTextEncoding acts as if *excludedDFR* was omitted and no data folders are excluded. |
| <span class="table-cell-nowrap">/SKIP = *skip*</span> | Skips conversion of a string variable as follows: |
|  |<table class="nested-table"><tbody><tr><td>*skip*=0:</td><td>Do not skip conversion.</td></tr><tr><td>*skip*=1:</td><td>Skip conversion of strings containing binary data.</td></tr><tr><td>*skip*=2:</td><td>When converting to UTF-8, skip conversion of strings that are already valid as UTF-8. This includes strings that contain only ASCII characters.</td></tr><tr><td>*skip*=3:</td><td>Skips both strings containing binary data and, when converting to UTF-8, strings that are already valid as UTF-8. This is the default behavior if /SKIP is omitted.</td></tr><tr><td></td><td>/SKIP=2 and /SKIP=3 require Igor Pro 9.00 or later.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents procedure execution from aborting if ConvertGlobalStringTextEncoding generates an error. Use /Z or the equivalent, /Z=1, if you want to handle errors in your procedures rather than having execution abort. |
|  | /Z does not suppress invalid parameter errors. It suppresses only errors in doing text encoding conversion. |

### *Details* {#details}
For general background information on text encodings, see [Text Encodings](/igorpro/igor-basics/text-encodings.md).

For background information on string variable text encodings, see [String Variable Text Encodings](/igorpro/igor-basics/text-encodings.md#string-variable-text-encodings).

### *Using ConvertGlobalStringTextEncoding* {#using-convertglobalstringtextencoding}
ConvertGlobalStringTextEncoding is used to change the numeric codes representing the text - i.e., to convert the content to a different text encoding. Its main use is to convert Igor Pro 6 global string variables from whatever text encoding they use to UTF-8. UTF-8 is a form of Unicode which is more modern but is not backward compatible with Igor Pro 6. Igor Pro 7 and later assume that string variables are encoded as UTF-8.

For example, if you have global string variables from Igor Pro 6 that are encoded in Japanese (Shift JIS), you should convert them to UTF-8. Otherwise you will get errors or garbled text when you print or display the strings. This also applies to western text containing non-ASCII characters encoded as MacRoman or Windows-1252.

If you have an Igor 6 experiment containing non-ASCII string variables encoded as, for example, MacRoman, and you add some non-ASCII string variables in Igor 7 or later, you now have a mix of MacRoman and UTF-8 non-ASCII string variables. In Igor 9 or later, when you are converting to UTF-8, by default ConvertGlobalStringTextEncoding skips conversion of strings that are already valid as UTF-8. This allows you to convert the MacRoman string variables to UTF-8 without messing up the string variables that are already UTF-8.

### *Output Variables* {#output-variables}
The ConvertGlobalStringTextEncoding operation returns information in the following variables:

|  |  |
| --- | --- |
| *V_numConversionsSucceeded* | Set to the number of successful text conversions. |
| *V_numConversionsFailed* | Set to the number of unsuccessful text conversions. |
| *V_numConversionsSkipped* | Set to the number of skipped text conversions. Text conversion may be skipped if the string variable contains binary data and the /SKIP=0 flag is not used.<br>Text conversion is skipped by default if the string variable contains binary data. Text conversion is also skipped by default if *newTextEncoding* is 1 (UTF-8) and the string variable is already valid as UTF-8. See the /SKIP flag for details. |

### *Examples* {#examples}

```igor
// In the following examples 1 means UTF-8, 4 means Shift JIS.

// Convert specific strings' content from Shift JIS to UTF-8
ConvertGlobalStringTextEncoding 4, 1, string0, string1

// Convert all strings' content from Shift JIS to UTF-8
ConvertGlobalStringTextEncoding /DF={root:,1} 4, 1

// Same as before but exclude the root:Packages data folder
ConvertGlobalStringTextEncoding /DF={root:,1,root:Packages} 4, 1

// Convert all strings' content from Shift JIS to UTF-8 except strings containing binary data
ConvertGlobalStringTextEncoding /DF={root:,1}/SKIP=0 4, 1
```

### *See Also* {#see-also}
[Text Encodings](/igorpro/igor-basics/text-encodings.md), [String Variable Text Encodings](/igorpro/igor-basics/text-encodings.md#string-variable-text-encodings), [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes)

[ConvertTextEncoding](/igorpro/commands/converttextencoding.md), [SetWaveTextEncoding](/igorpro/commands/setwavetextencoding.md)