---
description: "The SavePICT operation creates a picture file representing the top graph, table or layout."
slug: /commands/savepict
---

<div className="command-signature">

## <strong>SavePICT</strong>  [<em>flags</em>] [<em>as</em> <em>fileNameStr</em> ] {#savepict}

</div>

The SavePICT operation creates a picture file representing the top graph, table or layout. The picture file can be opened by many word processing, drawing, and page layout programs.

### *Parameters* {#parameters}
The file to be written is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

If you omit *fileNameStr* but include /P=*pathName*, SavePICT writes the file using a default file name. The default file name is the window name followed by an extension, such as ".png", ".emf" or ".svg", that depends on the graphic format being exported.

If you specify the file name as "Clipboard", and do *not* specify a /P=*pathName*, Igor copies the picture to the Clipboard, rather than to a file. EPS is a file-only format and cannot be stored in the clipboard.

If you specify the file name as "\_string\_" the output will be saved into a string variable named S_Value, which is used with the [ListBox](/igorpro/user-interface/controls.md#listbox) binary bitmap display mode.

If you use the special name \_PictGallery\_ with the /P flag, then the picture will be stored in Igor's picture gallery (see [Pictures](/igorpro/graphing/making-figures/graphics.md#pictures)) with the name you provide via *fileNameStr*. This feature was added in support of making movies using the /PICT flag with NewMovie.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *dpi*</span> | Controls image resolution in dots-per-inch (*dpi* ). The legal values for *dpi* are n*72 where n can be from 1 to 8. At the time of this writing, the actual dpi is not used. Igor calculates n from your value of *dpi* and then multiplies n by your computer's screen resolution. This is because bitmap images that are not an integer multiple of the screen resolution look quite bad. |
|  | Also see the /RES flag. |
| <span class="table-cell-nowrap">/C = *c*</span> | Specifies color mode. |
|  |<table class="nested-table"><tbody><tr><td>*c*&nbsp;=0:</td><td>Black and white.</td></tr><tr><td>*c*&nbsp;=1:</td><td>RGB color (default).</td></tr><tr><td>*c*&nbsp;=2:</td><td>CMYK color (EPS and native TIFF only).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/D = *d*</span> | Obsolete in Igor Pro 7 or later. |
| <span class="table-cell-nowrap">/E = *e*</span> | Sets graphics format used when exporting a graphic. See details below. |
| <span class="table-cell-nowrap">/EF = *e*</span> | Sets font embedding. |
|  |<table class="nested-table"><tbody><tr><td>*e*&nbsp;=&nbsp;0:</td><td>No font embedding. Not honored in Igor Pro 7 or later.</td></tr><tr><td>*e*&nbsp;=&nbsp;1:</td><td>Embed nonstandard fonts.</td></tr><tr><td>*e*&nbsp;=&nbsp;2:</td><td>Embed all fonts.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/I</span> | Specifies that /W coordinates are in inches. |
| <span class="table-cell-nowrap">/M</span> | Specifies that /W coordinates are in centimeters. |
| <span class="table-cell-nowrap">/N = *winSpec*</span> | /N is antiquated but still supported. Use /WIN. |
| <span class="table-cell-nowrap">/O</span> | Overwrites file if it exists. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Saves file into folder specified by *pathName*, which is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/PGR = (*firstPage, lastPage* )</span> |  |
|  | Controls which pages in a multi-page layout are saved. |
|  | *firstPage* and *lastPage* are one-based page numbers. All pages from *firstPage* to *lastPage* are saved if the file format supports it. |
|  | The special value 0 refers to the current page and -1 refers to the last page in the layout. |
|  | Currently only the PDF formats support saving multiple pages. Other file formats save only *firstPage* and ignore the value of *lastPage*. |
|  | /PGR was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/PICT = *pict*</span> | Saves specified named picture rather than the target window. Native format of the picture is used and all format flags are ignored. |
| <span class="table-cell-nowrap">/PLL = *p*</span> | Specifies Postscript language level when used in conjunction with EPS export. |
|  |<table class="nested-table"><tbody><tr><td>*p*&nbsp;=1:</td><td>For very old Postscript printers.</td></tr><tr><td>*p*&nbsp;=2:</td><td>For all other uses (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q = *q*</span> | Sets quality factor (0.0 is lowest, 1.0 is highest). Default is dependent on individual format. Used only by lossy formats such as JPEG. |
| <span class="table-cell-nowrap">/R = *resID*</span> | Obsolete in Igor Pro 7 or later. |
| <span class="table-cell-nowrap">/RES = *dpi*</span> | Controls the resolution of image formats in dots-per-inch. Unlike the similar /B flag, the value for /RES is the actual output resolution and is useful when your publisher demands a specific resolution. |
| <span class="table-cell-nowrap">/S</span> | Suppresses the preview that is normally included with an EPS file. |
|  | Obsolete in Igor Pro 7 or later. |
| <span class="table-cell-nowrap">/SNAP = *s*</span> | Saves a snapshot (screen dump) of a graph or panel window or subwindow. |
|  |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=1:</td><td>Include all controls in capture.</td></tr><tr><td>*s*&nbsp;=2:</td><td>Capture only graph area content, not including control bars or panel subwindows.</td></tr></tbody></table>
|  | Snapshot mode is available only for graphs and panels and only for bitmap export formats PNG, JPEG, and TIFF at screen resolution. |
|  | SNAP=2 only applies to graph windows and subwindows specified with /WIN. |
|  | When using /W to specify the size of a graph, the capture is sized to fit within the specified rectangle while maintaining the window aspect ratio. Coordinates used with /W are in pixels. |
| <span class="table-cell-nowrap">/T = *t*</span> | Obsolete QuickTime export type. Not supported in Igor Pro 7 or later. |
| <span class="table-cell-nowrap">/TRAN[ = 1 *or* 0]</span> |  |
|  | Makes white background areas transparent using an RGBA type PNG when used with native PNG export of graphs or page layouts. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Specifies the size of the picture when exporting a graph. If /W is omitted, the size is taken from the graph window. |
|  | When exporting a page layout, specifies the part of the page to export. Only objects that fall completely within the specified area are exported. If /W is omitted, the area of the layout containing objects is exported. |
|  | When exporting a page layout in Igor Pro 7.00 or later, you can specify /W=(0,0,0,0) to use the full page size. |
|  | Coordinates for /W are in points unless /I or /M are specified before /W. |
| <span class="table-cell-nowrap">/WIN = *winSpec*</span> | Saves the named window or subwindow. *winSpec* can be just a window name, or a window name following by a '#' character and the name of the subwindow, as in /WIN=Panel0#G0. |
| <span class="table-cell-nowrap">/Z</span> | Prevents errors from being fatal. V_flag is set to zero if no error, else nonzero if error. |

### *Details* {#details}
SavePICT sets the variable V_flag to 0 if the operation succeeds or to a nonzero error code if it fails.

If you specify a path using the /P=*pathName* flag, then Igor saves the file in the folder identified by the path. Note that *pathName* is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:" or "C:\\Folder1\\". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details. Otherwise, with no path specified, Igor presents a standard save dialog to let you specify where the file is to be saved.

The graphics formats, specified via /E, are as follows:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">*e* = -9:</span> | SVG file. |
| <span class="table-cell-nowrap">*e* = -8:</span> | Igor PDF file. |
| <span class="table-cell-nowrap">*e* = -7:</span> | TIFF file. Lossless but larger file than PNG; best for text, graph traces, and simple images with sharp edges. The default resolution is 72 dpi. Specify the resolution with the /B or /RES flag. Use for cross-platform compatibility. |
| <span class="table-cell-nowrap">*e* = -6:</span> | JPEG file. Lossy compression; best used for grayscale and color images with smooth tones. The /Q flag specifies compression quality and the /B or /RES flag sets the resolution. Use for cross-platform compatibility. PNG is a better choice for scientific graphics. |
| <span class="table-cell-nowrap">*e* = -5:</span> | PNG (Portable Network Graphics) file. Lossless compression; best for text, graph traces, and simple images with sharp edges. The default resolution is 72 dpi. Specify the resolution with the /B or /RES flag. Use for cross-platform compatibility. |
| <span class="table-cell-nowrap">*e* = -4:</span> | Device-independent bitmap file (DIB). The default resolution is 4x screen resolution. Specify the resolution with the /B or /RES flag. |
| <span class="table-cell-nowrap">*e* = -3:</span> | Encapsulated PostScript (EPS) file. |
|  | Use /S to suppress the screen preview if exporting to Latex. |
| <span class="table-cell-nowrap">*e* = -2:</span> | High-resolution Enhanced Metafile (EMF). |
| <span class="table-cell-nowrap">*e* = -1:</span> | Obsolete (was PostScript-enhanced metafile). |
| <span class="table-cell-nowrap">*e* = 0:</span> | Obsolete (was PostScript-enhanced metafile). |
| <span class="table-cell-nowrap">*e* > = 1:</span> | High-resolution Enhanced Metafile (EMF). |

### *See Also* {#see-also}
The [ImageSave](/igorpro/commands/imagesave.md) operation for saving waves as PICTs and other image file formats.

[LoadPICT](/igorpro/commands/loadpict.md)

See [Exporting Graphics (Windows)](/igorpro/graphing/making-figures/graphics.md#exporting-graphics-windows) for a description of the /E=*e* modes and when to use which mode.