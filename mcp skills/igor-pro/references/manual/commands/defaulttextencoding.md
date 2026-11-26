---
description: "The DefaultTextEncoding operation programmatically changes the default text encoding and experiment text encoding override settings."
slug: /commands/defaulttextencoding
---

<div className="command-signature">

## <strong>DefaultTextEncoding</strong>  [<em>encoding</em>=<em>textEncoding</em> , <em>overrideDefault</em>=<em>override</em> ] {#defaulttextencoding}

</div>

The DefaultTextEncoding operation programmatically changes the default text encoding and experiment text encoding override settings. These settings, which are discussed under [The Default Text Encoding](/igorpro/igor-basics/text-encodings.md#the-default-text-encoding), are also accessible via the Misc->Text Encoding->Default Text Encoding menu.

DefaultTextEncoding is rarely needed because typically you will change the default text encoding manually using the menu, if at all.

The DefaultTextEncoding operation was added in Igor Pro 7.00.

### *Parameters* {#parameters}
All parameters are optional. If none are specified, no action is taken, but the output variables are still set.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">encoding = *textEncoding*</span> | *textEncoding* specifies the new default text encoding. See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of codes. |
|  | Pass 0 to set the default text encoding to the equivalent of selecting "Western" from the Default Text Encoding submenu. |
|  | The value 255, corresponding to the binary text encoding type, is treated as an invalid value for the *textEncoding*  parameter. |
| <span class="table-cell-nowrap">overrideDefault = *override*</span> | Turns overriding of the experiment's text encoding off or on. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Turns override off</td></tr><tr><td>1:</td><td>Turns override on</td></tr></tbody></table>

### *Details* {#details}
The default text encoding affects Igor's behavior when opening a file whose text encoding is unknown. See [The Default Text Encoding](/igorpro/igor-basics/text-encodings.md#the-default-text-encoding) for details.

The experiment text encoding affects how files are treated during experiment loading only. The override setting allows you to override the experiment text encoding stored in the experiment. Normally you will not need to do this. See [The Default Text Encoding](/igorpro/igor-basics/text-encodings.md#the-default-text-encoding) for further discussion.

You may occasionally find it necessary to change the default text encoding because an Igor operation lacks a /ENCG flag that allows you to specify the text encoding and instead uses the current default text encoding. In such cases it is a good idea to save the original default text encoding, change it as necessary, and then change it back to the original text encoding. The example below demonstrates this technique.

### *Output Variables* {#output-variables}
DefaultTextEncoding sets the following output variables to indicate the settings that are in effect *after*  the command executes:


|  |  |
| --- | --- |
| V_defaultTextEncoding | A text encoding code. |
| V_overrideExperiment | A value of zero means the setting is off, nonzero means the setting is on. |

### *Example* {#example}

```igor
Function DemoDefaultTextEncoding()
	// Store the original default text encoding
	DefaultTextEncoding
	Variable originalTextEncoding = V_defaultTextEncoding

	// Set new default text encoding
	DefaultTextEncoding encoding = 3		// 3 = Windows-1252

	// [ Do something that depends on the default text encoding ]

	// Restore the original default text encoding
	DefaultTextEncoding encoding = originalTextEncoding
End
```

### *See Also* {#see-also}
[The Default Text Encoding](/igorpro/igor-basics/text-encodings.md#the-default-text-encoding), [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes)