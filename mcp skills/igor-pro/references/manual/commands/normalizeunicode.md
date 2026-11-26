---
description: "The NormalizeUnicode function normalizes the UTF-8-encoded text in sourceTextStr using the specified normalization form."
slug: /commands/normalizeunicode
---

<div className="command-signature">

## <strong>NormalizeUnicode</strong> (<em>sourceTextStr</em>, <em>normalizationForm</em>[, <em>options</em>]) {#normalizeunicode}

</div>

The NormalizeUnicode function normalizes the UTF-8-encoded text in *sourceTextStr* using the specified normalization form. The output text encoding is UTF-8.

NormalizeUnicode was added in Igor Pro 7.00. Most users will have no need for this function and can ignore it.

As explained under Details, in Unicode there are sometimes multiple ways to spell what appears visually to be the same word. This can cause problems when comparing text. Two strings that appear to represent the same word and which you consider equivalent may be spelled differently, causing a comparison operation to indicate that they are unequal. The NormalizeUnicode function converts *sourceTextStr* to a normalized form, which aides comparison.

### *Parameters* {#parameters}
*sourceTextStr* is the text that you want to normalize. It must be encoded as UTF-8.

*normalizationForm* specifies the normalization form to use. These forms are described at [http://unicode.org/reports/tr15/#Norm_Forms](http://unicode.org/reports/tr15/#Norm_Forms). The allowed values are:


|  |  |
| --- | --- |
| 0: | NFD (Canonical Decomposition) |
| 1: | NFC (Canonical Decomposition, followed by Canonical Composition) |
| 2: | NFKD (Compatibility Decomposition) |
| 3: | NFKC (Compatibility Decomposition, followed by Canonical Composition) |


|  |  |
| --- | --- |
| *options* is a bitwise parameter, with the bits defined as follows: |  |
| Bit 0: | If cleared, in the event of an error, a null string is returned and an error is generated. Use this if you want to abort procedure execution if an error occurs. |
|  | If set, in the event of an error, a null string is returned but no error is generated. Use this if you want to detect and handle an error yourself. You can test for null using strlen as shown in [String Variable Text Encoding Error Example](/igorpro/igor-basics/text-encodings.md#string-variable-text-encoding-error-example). |


|  |
| --- |
| All other bits are reserved and must be cleared. |

### *Details* {#details}
The Unicode standard specifies that some sequences of code points represent essentially the same character. There are two types of equivalence: canonical equivalence and compatibility.

Sequences of code points defined as canonically equivalent are assumed to have the same appearance and meaning when printed or displayed. For example, the code point U+006E (LATIN SMALL LETTER N) followed by U+0303 (COMBINING TILDE) is defined by Unicode to be canonically equivalent to the single code point U+00F1 (LATIN SMALL LETTER N WITH TILDE). The former is called "decomposed" while the later is called "precomposed".

Sequences that are defined as compatible are assumed to have possibly distinct appearances, but the same meaning in some contexts. Thus, for example, the code point U+FB00 (LATIN SMALL LIGATURE FF) is defined to be compatible, but not canonically equivalent, to the sequence U+0066 U+0066 (two Latin "f" letters). Sequences that are canonically equivalent are also compatible, but the opposite is not necessarily true.

Text searching and sorting routines in Igor do not do any form of Unicode normalization. As a consequence, searching for the precomposed form of small letter n with tilde (U+00F1) in a string that contains the decomposed form (U+006E U+0303) will not result in a match. To get the desired result, you would need to first pass both the target string and the string to be searched through NormalizeUnicode using the same value for the *normalizationForm* parameter.

### *Example* {#example}

```igor
Function TestNormalization()
	String precomposed = "Ni" + "\u00F1" + "o"
	String decomposed = "Ni" + "\u006E\u0303" + "o"
	String precomposedTarget = "\u00F1"
	String decomposedTarget = "\u006E\u0303"
	Variable foundPos
	
	// SUCCESSFUL TESTS
	// Searching the precomposed string for the precomposed target is successful.
	foundPos = strsearch(precomposed, precomposedTarget, 0)
	Print foundPos					// Prints 2
	
	// Likewise, searching the decomposed string for the decomposed target is successful.
	foundPos = strsearch(decomposed, decomposedTarget, 0)
	Print foundPos					// Prints 2
	
	// UNSUCCESSFUL TESTS
	// Searching the precomposed string for the decomposed target fails.
	foundPos = strsearch(precomposed, decomposedTarget, 0)
	Print foundPos					// Prints -1
	
	// Likewise, searching the decomposed string for the precomposed target fails.
	foundPos = strsearch(decomposed, precomposedTarget, 0)
	Print foundPos					// Prints -1
	
	// USING NormalizeUnicode() FUNCTION
	Variable normForm = 2	// Could use 0-3 and the results would be the same.
									
	String precomposedNorm = NormalizeUnicode(precomposed, normForm)
	String decomposedNorm = NormalizeUnicode(decomposed, normForm)
	String precomposedTargetNorm = NormalizeUnicode(precomposedTarget, normForm)
	String decomposedTargetNorm = NormalizeUnicode(decomposedTarget, normForm)
	
	// Now, searching either precomposedNorm or decomposedNorm for either
	// precomposedTargetNorm or decomposedTargetNorm will give a match.
	Print strsearch(precomposedNorm, precomposedTargetNorm, 0)		// Prints 2
	Print strsearch(decomposedNorm, precomposedTargetNorm, 0)		// Prints 2
	Print strsearch(precomposedNorm, decomposedTargetNorm, 0)		// Prints 2
	Print strsearch(decomposedNorm, decomposedTargetNorm, 0)		// Prints 2
End
```

### *See Also* {#see-also}
[Text Encodings](/igorpro/igor-basics/text-encodings.md), [String Variable Text Encoding Error Example](/igorpro/igor-basics/text-encodings.md#string-variable-text-encoding-error-example)

[http://en.wikipedia.org/wiki/Unicode_equivalence](http://en.wikipedia.org/wiki/Unicode_equivalence)

[http://unicode.org/reports/tr15/#Norm_Forms](http://unicode.org/reports/tr15/#Norm_Forms)