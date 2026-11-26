---
description: "The WaveTextEncoding function returns the text encoding code for the specified element of a wave. See Wave Text Encodings for background information."
slug: /commands/wavetextencoding
---

<div className="command-signature">

## <strong>WaveTextEncoding</strong> (<em>wave</em>, <em>element</em>, <em>getEffectiveTextEncoding</em>) {#wavetextencoding}

</div>

The WaveTextEncoding function returns the text encoding code for the specified element of a wave. See [Wave Text Encodings](/igorpro/igor-basics/text-encodings.md#wave-text-encodings) for background information.

This function is used to deal with text encoding issues that sometimes arise in when you load pre-Igor Pro 7 experiments. Most users will have no need to use it.

The WaveTextEncoding function was added in Igor Pro 6.30. The *getEffectiveTextEncoding* parameter was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*wave* specifies the wave of interest.

*element* specifies a part of the wave, as follows:


| Value | Meaning |
| --- | --- |
| 1 | Wave name |
| 2 | Wave units |
| 4 | Wave note |
| 8 | Wave dimension labels |
| 16 | Text wave content |

*getEffectiveTextEncoding* determines if WaveTextEncoding returns a raw text encoding code or an effective text encoding code as explained below.

### *Details* {#details}
WaveTextEncoding returns a integer text encoding code. See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for details.

As explained under [Wave Text Encodings](/igorpro/igor-basics/text-encodings.md#wave-text-encodings), each of the wave elements has a corresponding text encoding setting. Because the notion of text encoding settings was added in Igor Pro 6.30, waves created by earlier versions have their text encoding settings set to unknown (0).

The text encoding setting stored for a given element is the "raw" text encoding. If it is unknown, then Igor applies some rules when the wave is accessed to determine an "effective" text encoding for the element being accessed. The rules are explained under [Determining the Text Encoding for Wave Elements](/igorpro/igor-basics/text-encodings.md#determining-the-text-encoding-for-wave-elements).

If *getEffectiveTextEncoding* is non-zero then WaveTextEncoding returns the effective text encoding. If *getEffectiveTextEncoding* is zero it returns the raw text encoding.

### *See Also* {#see-also}
[Wave Text Encodings](/igorpro/igor-basics/text-encodings.md#wave-text-encodings), [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes)