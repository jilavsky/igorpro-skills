---
description: "TagWaveRef is a very specialized function that is only valid when called from within the text of a tag as part of a \\{} dynamic text escape sequence."
slug: /commands/tagwaveref
---

<div className="command-signature">

## <strong>TagWaveRef</strong> () {#tagwaveref}

</div>

TagWaveRef is a very specialized function that is only valid when called from within the text of a tag as part of a \\{} dynamic text escape sequence. It returns a wave reference to the wave that the tag is on and helps you to display information about the tagged wave. It is often used in conjunction with the [TagVal](/igorpro/commands/tagval.md)() function. You can pass the result of TagWaveRef to any function that takes a Wave parameter.

### *Examples* {#examples}

```igor
// Show the name of the data folder containing the tagged wave.
Tag wave0, 0,"\\ON is in \\{\"%s\",GetWavesDataFolder(TagWaveRef(),0)}"
```

### *See Also* {#see-also}
[Tag](/igorpro/commands/tag.md), [TagVal](/igorpro/commands/tagval.md)