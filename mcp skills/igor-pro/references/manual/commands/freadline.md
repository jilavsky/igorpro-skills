---
description: "The FReadLine operation reads bytes from a file into the named string variable."
slug: /commands/freadline
---

<div className="command-signature">

## <strong>FReadLine</strong>  [/N=<em>n</em> /ENCG=<em>textEncoding</em> /T=<em>termcharStr</em> ] <em>refNum</em>, <em>stringVarName</em> {#freadline}

</div>

The FReadLine operation reads bytes from a file into the named string variable. The read starts at the current file position and continues until a terminator character is read, the end of the file is reached, or the maximum number of bytes is read.

### *Parameters* {#parameters}
*refNum* is a file reference number from the Open operation used to create the file.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N = *n*</span> | Specifies the maximum number of bytes to read. |
|  | FReadLine can read lines text of length up to about 2 billion bytes. |
| <span class="table-cell-nowrap">/ENCG = *textEncoding*</span> |  |
| <span class="table-cell-nowrap">/ENCG = {*textEncoding, tecOptions [,mapErrorMode]*}</span> |  |
|  | Specifies the text encoding of the plain text file being loaded. |
|  | This flag was added in Igor Pro 9.00. |
|  | See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of accepted values for *textEncoding*. The 32-bit Unicode text encodings UTF-32BE and UTF-32LE are currently not supported. |
|  | If you omit /ENCG, *textEncoding* defaults to binary (255) and does no text encoding conversion but does look for and skip a UTF-8 byte order mark. |
|  | For most purposes the default values for *tecOptions* (3) and *mapErrorMode* (1) are fine and you can use /ENCG=*textEncoding* instead of /ENCG={*textEncoding , tecOptions [,mapErrorMode]*}. |
|  | *tecOptions* is an optional bitwise parameter that controls text encoding conversion. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | *tecOptions* is defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>If cleared, the presence of null bytes causes FReadLine to consider the text invalid in all byte-oriented text encodings.</td></tr><tr><td></td><td>If set (default), null bytes are allowed in byte-oriented text encodings.</td></tr><tr><td>Bit&nbsp;1:</td><td>If cleared FReadLine does not validate text if the specified text encoding is UTF-8.</td></tr><tr><td></td><td>If set (default), FReadLine validates text even if the text encoding is UTF-8.</td></tr><tr><td>Bit&nbsp;2:</td><td>If cleared (default) FReadLine validates the text in the specified text encoding except that validation for UTF-8 is skipped if bit 1 is cleared.</td></tr><tr><td></td><td>If set, FReadLine assumes that the text is valid in the specified text encoding and does not validate it. Setting this bit makes FReadLine slightly faster but it is usually inconsequential.</td></tr></tbody></table>
|  | *mapErrorMode* determines what happens if an input character cannot be mapped to UTF-8 because it is not valid in the input text encoding. *mapErrorMode* is one of these values: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>FReadLine generates an error.</td></tr><tr><td>2:</td><td>Return a substitute character for the unmappable character. The substitute character for Unicode is the Unicode replacement character, � (U+FFFD). For most non-Unicode text encodings it is either control-Z or a question mark.</td></tr><tr><td>3:</td><td>Skip unmappable input character.</td></tr><tr><td>4:</td><td>Return an escape sequence representing the unmappable code point.</td></tr></tbody></table>
|  | If mapErrorMode is 2, 3 or 4, FReadLine does not return an error in the event of an unmappable character. |
|  | See the discussion of *mapErrorMode* and the examples for [ConvertTextEncoding](/igorpro/commands/converttextencoding.md) for further discussion. |
|  | See ***FReadLine and Text Encodings*** below for further discussion. |
| <span class="table-cell-nowrap">/T = *termcharStr*</span> |  |
|  | Specifies the terminator character. |
|  |<table class="nested-table"><tbody><tr><td>/T=(num2char(13))</td><td>Specifies carriage return (CR, ASCII code 13).</td></tr><tr><td>/T=(num2char(10))</td><td>Specifies linefeed (LF, ASCII code 10).</td></tr><tr><td>/T=&quot;;&quot;</td><td>Specifies the terminator as a semicolon.</td></tr><tr><td>/T=&quot;&quot;</td><td>Specifies the terminator as null (ASCII code 0).</td></tr></tbody></table>
|  | See ***Details*** for the default behavior of FReadLine regarding the terminator. |

### *Details* {#details}
If /N is omitted, there is no maximum number of bytes to read. When reading lines of text from a normal text file, you will not need to use /N. It may be of use in specialized cases, such as reading text embedded in a binary file.

FReadLine can read lines text of length up to about 2 billion bytes.

If /T is omitted, FReadLine will terminate on any of the following: CR, LF, CRLF, LFCR. (Most Macintosh files use CR. Most Windows files use CRLF. Most UNIX files use LF. LFCR is an invalid terminator but some buggy programs generate files that use it.) FReadLine reads whichever of these appears in the file, terminates the read, and returns just a CR in the output string. This default behavior transparently handles files that use CR, LF, CRLF or LFCR as the terminator and will be suitable for most cases.

If you use the /T flag, then FReadLine will terminate on the specified character only and will return the specified character in the output string.

Once you have read all of the bytes in the file, FReadLine will return zero bytes via *stringVarName* . The example below illustrates testing for this.

### *FReadLine and Text Encodings* {#freadline-and-text-encodings}
For background information on text encodings, see [Text Encodings](/igorpro/igor-basics/text-encodings.md).

In Igor Pro 9.00 and later, you can specify the text encoding of the file you are reading using the /ENCG flag.

If you omit /ENCG, FReadLine treats the data as binary and does no text encoding conversion. However, it does skip a UTF-8 byte order mark at the start of the file if present. Treating the data as binary works if the data you are loading is pure ASCII or is valid UTF-8 text.

If you specify a text encoding using /ENCG, the FReadLine converts the text from the text encoding you specify into UTF-8 for internal storage. See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of accepted values for *textEncoding*. The 32-bit Unicode text encodings UTF-32BE and UTF-32LE are currently not supported.

In general it is not possible to accurately determine the text encoding of a plain text file programmatically so you need to know it *a priori*.

If the text is Unicode and includes a byte order mark then you can programmatically determine the text encoding by examining the byte order mark. You can do this using FBinRead to examine the first bytes of the file:

|  |  |  |
| --- | --- | --- |
| 0xEF, 0xBB, 0xBF | UTF-8 byte order mark | *textEncoding*=1 |
| 0xFE, 0xFF | UTF-16BE byte order mark | *textEncoding*=100 |
| 0xFF, 0xFE | UTF-16LE byte order mark | *textEncoding*=101 |

If the file starts with a pattern other than these then you will need *a priori* knowledge or will need to make an assumption about the text encoding.

### *FReadLine and Byte Order Marks* {#freadline-and-byte-order-marks}
For background information on byte order marks, see [Byte Order Marks](/igorpro/igor-basics/text-encodings.md#byte-order-marks).

If you want to check for the presence of a byte order mark, use [FBinRead](/igorpro/commands/fbinread.md) instead of FReadLine.

The default text encoding, used if you omit /ENCG, is binary (255). In this case, FReadLine does no text encoding conversion. However, it does look for a UTF-8 byte order mark and skips it if present.

If you specify UTF-8 or UTF-16 as the text encoding using the /ENCG flag, and if the file data begins with a byte order mark, then FReadLine skips it.

### *Example* {#example}

```igor
Function PrintAllLinesInFile()
	Variable refNum
	Open/R refNum as ""	// Display dialog
	if (refNum == 0)
		return -1		// User canceled
	endif

	Variable lineNumber, len
	String buffer
	lineNumber = 0
	do
		FReadLine refNum, buffer
		len = strlen(buffer)
		if (len == 0)
			break		// No more lines to be read
		endif
		Printf "Line number  %d: %s", lineNumber, buffer
		if (CmpStr(buffer[len-1],"\r") != 0)	// Last line has no CR ?
			Printf "\r"
		endif
	lineNumber += 1
	while (1)

	Close refNum
	return 0
End
```

### *See Also* {#see-also}
[Open](/igorpro/commands/open.md), [FBinRead](/igorpro/commands/fbinread.md)

### *Demos* {#demos}
[Open Load File Demo](#igor-pxp/Examples/Programming/Load__File__Demo.pxp)