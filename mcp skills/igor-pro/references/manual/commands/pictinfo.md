---
description: "The PICTInfo function returns a string containing a semicolon-separated list of information about the named picture."
slug: /commands/pictinfo
---

<div className="command-signature">

## <strong>PICTInfo</strong> (<em>pictNameStr</em>) {#pictinfo}

</div>

The PICTInfo function returns a string containing a semicolon-separated list of information about the named picture. If the named picture does not exist, then "" is returned. Valid picture names can be found in the Pictures dialog.

### *Details* {#details}
The string contains six pieces of information, each prefaced by a keyword and colon and terminated with a semicolon.


| Keyword | Information Following Keyword |
| --- | --- |
| TYPE | One of the following types: |
|  |<table class="nested-table"><tbody><tr><td></td><td>DIB</td></tr><tr><td></td><td>Encapsulated PostScript</td></tr><tr><td></td><td>Enhanced metafile</td></tr><tr><td></td><td>JPEG</td></tr><tr><td></td><td>PDF</td></tr><tr><td></td><td>PNG</td></tr><tr><td></td><td>SVG</td></tr><tr><td></td><td>TIFF</td></tr><tr><td></td><td>Windows bitmap</td></tr><tr><td></td><td>Windows metafile</td></tr><tr><td></td><td>Unknown type</td></tr></tbody></table>
| BYTES | Amount of memory used by the picture. |
| WIDTH | Width of the picture in pixels. |
| HEIGHT | Height of the picture in pixels. |
| PHYSWIDTH | Physical width of the picture in points. |
| PHYSHEIGHT | Physical height of the picture in points. |



### *Examples* {#examples}

```igor
Print PICTInfo("PICT_0")
```

will print the following in the history area:


```
TYPE:PICT;BYTES:55734;WIDTH:468;HEIGHT:340;PHYSWIDTH:468;PHYSHEIGHT:340;
```

### *See Also* {#see-also}
The [ImageLoad](/igorpro/commands/imageload.md) operation for loading PICT and other image file types into waves, and the [PICTList](/igorpro/commands/pictlist.md) function.

[Pictures](/igorpro/graphing/making-figures/graphics.md#pictures), [Pictures Dialog](/igorpro/user-interface/dialog-help.md#pictures-dialog), [StringFromList](/igorpro/commands/stringfromlist.md)