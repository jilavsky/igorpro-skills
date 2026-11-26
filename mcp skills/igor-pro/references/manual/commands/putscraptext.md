---
description: "The PutScrapText operation places textStr on the Clipboard (aka \"scrap\"). This text will be used when the user subsequently selects Paste from the Edit menu."
slug: /commands/putscraptext
---

<div className="command-signature">

## <strong>PutScrapText</strong>  <em>textStr</em> {#putscraptext}

</div>

The PutScrapText operation places *textStr*  on the Clipboard (aka "scrap"). This text will be used when the user subsequently selects Paste from the Edit menu.

### *Details* {#details}
All contents of the Clipboard (including pictures) are cleared before the text is placed there.

### *Examples* {#examples}

```igor
// Put two lines of text into the Clipboard
	String text = "This is the first line.\rAnd this is the second."
	PutScrapText text

// Empty the Clipboard
	PutScrapText ""
```

### *See Also* {#see-also}
[GetScrapText](/igorpro/commands/getscraptext.md), [SavePICT](/igorpro/commands/savepict.md)