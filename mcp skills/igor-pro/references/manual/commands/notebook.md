---
description: "The Notebook operation sets various properties of the named notebook window. Notebook also inserts text and graphics. See Notebooks for general information."
slug: /commands/notebook
---

<div className="command-signature">

## <strong>Notebook</strong>  <em>winName</em>, <em>keyword</em> =<em>value</em> [, <em>keyword</em> =<em>value</em> ]... {#notebook}

</div>

The Notebook operation sets various properties of the named notebook window. Notebook also inserts text and graphics. See [Notebooks](/igorpro/igor-basics/notebooks.md) for general information.

Notebook returns an error if the notebook is open for read-only. Keywords that don't materially change the notebook, including findText, findPicture, selection, visible, magnification, userKillMode, showRuler and rulerUnits, are still permitted. See [Notebook Read/Write Properties](/igorpro/igor-basics/notebooks.md#notebook-read-write-properties) for further information.

### *Parameters* {#parameters}
*winName* is either kwTopWin for the top notebook window, the name of a notebook window or a host-child specification (an hcSpec) such as Panel0#nb0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on host-child specifications.

If *winName* is an hcSpec, the host window or subwindow must be a control panel. Graphs and page layouts are not supported as hosts for notebook subwindows.

The parameters to the Notebook operation are of the form *keyword* =*value* where *keyword* says what to do and *value* is a parameter or list of parameters. Igor limits the parameters that you specify to legal values before applying them to the notebook.

The parameters are classified into related groups of keywords.

### *See Also* {#see-also}
To create or modify a notebook action special character, see [NotebookAction](/igorpro/commands/notebookaction.md).

To create a notebook subwindow in a control panel, see [Notebooks as Subwindows in Control Panels](/igorpro/graphing/making-figures/subwindows.md#notebooks-as-subwindows-in-control-panels).

**Notebook selection parameters**

This section of Notebook relates to ***selecting a range*** of the content of the notebook.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">findPicture = {*graphicNameStr*, *flags* }</span> |  |
|  | Searches for the next picture if you pass "". Sets V_flag to 1 if the picture was found or to 0 if not found. |
|  | *flags* is a bitwise parameter interpreted as follows: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>Show selection after the find.</td></tr></tbody></table>
|  | All other bits are reserved for future use. Set bit 0 by setting *flags* = 1. |
|  | The search is always forward from the end of the current selection to the end of the document. |
| <span class="table-cell-nowrap">findSpecialCharacter = {*specialCharacterNameStr*, *flags* }</span> |  |
|  | Searches for the special character with the specified name or the next special character if you pass "". Selects the special character if it is found. |
|  | Sets V_flag to 1 if the special character was found or to 0 if not. Sets S_name to the name of the found special character or to "" if it was not found. |
|  | *flags* is a bitwise parameter interpreted as follows: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>show selection after the find.</td></tr></tbody></table>
|  | All other bits are reserved for future use. Set bit 0 by setting *flags* = 1. |
|  | If *specialCharacterNameStr* is empty (""), the search proceeds from the end of the current selection to the end of the document. Otherwise the search always covers the entire document. |
| <span class="table-cell-nowrap">findText = {*textToFindStr*, *flags* }</span> |  |
|  | Searches for the specified text. Sets V_flag to 1 if the text was found or to 0 if not found. |
|  | *textToFindStr* is a string expression for the text you want to find. If the text contains a carriage-return, Igor considers only the part of the text before the carriage-return. |
|  | *flags* is a bitwise integer parameter interpreted as follows: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>Show selection after the find.</td></tr><tr><td>bit&nbsp;1:</td><td>Do case-sensitive search.</td></tr><tr><td>bit&nbsp;2:</td><td>Search for whole words.</td></tr><tr><td>bit&nbsp;3:</td><td>Wrap around.</td></tr><tr><td>bit&nbsp;4:</td><td>Search backward.</td></tr></tbody></table>
|  | To set bit 0 and bit 3, use 2<sup>0</sup>+2<sup>3</sup> = 9 for *flags*. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | If you are searching forward, the search starts from the end of the current selection. If you are searching backward, the search starts from the start of the current selection. |
|  | If you specify "" as the text to search for, Igor "finds" the current selection. This displays the current selection using findText={"", 1}. |
| <span class="table-cell-nowrap">selection = {*selStart*, *selEnd* }</span> |  |
|  | *selStart* and *selEnd* are locations within the document. You can specify these locations with the following expressions: |
|  |<table class="nested-table"><tbody><tr><td>(*paragraph*,&nbsp;*pos*&nbsp;)</td><td>*paragraph* and *pos* are numeric expressions.</td></tr><tr><td></td><td>*paragraph* is a paragraph number from 0 to n-1 where n is the number of paragraphs in the document.</td></tr><tr><td></td><td>*pos* is a byte position from 0 to n where n is the number of bytes in the paragraph. Position 0 is to the left of the first character in the paragraph. Position n is to the right of the last character in the paragraph.</td></tr><tr><td>startOfFile</td><td>Start of the document.</td></tr><tr><td>endOfFile</td><td>End of the document.</td></tr><tr><td>startOfParagraph</td><td>Start of current selStart paragraph.</td></tr><tr><td>endOfParagraph</td><td>End of current selStart paragraph.</td></tr><tr><td>startOfNextParagraph</td><td>Start of paragraph after current selStart paragraph.</td></tr><tr><td>endOfNextParagraph</td><td>End of paragraph after current selStart paragraph.</td></tr><tr><td>startOfPrevParagraph</td><td>Start of paragraph before current selStart paragraph.</td></tr><tr><td>endOfPrevParagraph</td><td>End of paragraph before current selStart paragraph.</td></tr><tr><td>endOfChars</td><td>Just before the carriage-return of current selStart paragraph.</td></tr><tr><td>startOfPrevChar</td><td>Start of the character before the character at the current selection start or selection end. This moves the selection start or selection end like pressing the left arrow key.</td></tr><tr><td></td><td>Added in Igor Pro 7.00.</td></tr><tr><td>startOfNextChar</td><td>Start of the character after the character at the current selection start or selection end. This moves the selection start or selection end like pressing the right arrow key.</td></tr><tr><td></td><td>Added in Igor Pro 7.00.</td></tr></tbody></table>
|  | Igor clips the specified locations to legal values. It also sets the V_flag variable to 0 if the selStart location that you specified was valid, to 1 if the start paragraph was out of bounds and to 2 if the start position was out of bounds. You can use the startOfNextParagraph keyword to step through the document one paragraph at a time. When V_flag is nonzero, you are at the end of the document. |
|  | The terms next and prev are relative to the paragraph containing the start of the selected text before the selection keyword was invoked. |
|  | The selection keyword just sets the selection. If you also want to scroll the selected text into view you must also use the findText keyword as shown in the examples. |

### *Selection  Examples* {#selection-examples}

```igor
// select all text in notebook
Notebook Notebook1 selection={startOfFile, endOfFile}	
// move selection to the start of the notebook and display the selection
Notebook Notebook1 selection={startOfFile,startOfFile}, findText={"",1}
// move selection to the end of the notebook and display the selection
Notebook Notebook1 selection={endOfFile,endOfFile}, findText={"",1}
// select all of paragraph 3
Notebook Notebook1 selection={(3,0), (4,0)}
// select all of paragraph 3 and display the selection
Notebook Notebook1 selection={(3,0), (4,0)}, findText={"",1}
// select all of current paragraph except for trailing CR, if any
Notebook Notebook1 selection={startOfParagraph, endOfChars}
// select the first occurrence of "Hello" in the document and display the selection
Notebook Notebook1 selection={startOfFile,startOfFile}, findText={"Hello",1}
// select the first picture in the document
Notebook Notebook1 selection={startOfFile,startOfFile}, findPicture={"",1}
```

### *See Also* {#notebook-see-also}
The [GetSelection](/igorpro/commands/getselection.md) operation to "copy" the notebook text selection.

**Notebook text property parameters**

This section of Notebook relates to ***setting the text properties*** of the current selection in the notebook.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">font = "*fontName*"</span> | "*fontName*" contains the name of the font. Use "default" to specify the paragraph's ruler font. |
|  | If you specify an unavailable font, it does nothing. This is so that, when you share procedures with a colleague, using a font that the colleague does not have will not cause your procedures to fail. The downside of this behavior is that if you misspell a font name you will get no error message. |
| <span class="table-cell-nowrap">fSize = *fontSize*</span> | Text size from 3 to 32000 points. |
|  | Use -1 to specify the paragraph's ruler size. |
| <span class="table-cell-nowrap">fStyle = *fontStyle*</span> | A binary coded integer with each bit controlling one aspect of the text style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | Use -1 to specify the paragraph's ruler style. To set bit 0 and bit 1 (bold italic), use 2<sup>0</sup>+2<sup>1</sup> = 3 for *fontStyle*. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">syntaxColorSelection = *n*</span> | Use *n*=1 to syntax-color the selected text in the notebook. This is the equivalent of selecting Notebook→Syntax Color Selection. Other values of *n* are reserved for future use. |
|  | To remove syntax coloring, use the textRGB keyword to set the selected text to a specified color. |
|  | The syntaxColorSelection keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">textRGB = (*r*,*g*,*b*[,*a*])</span> | Specifies the color of the selected text or the text to be inserted. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
| <span class="table-cell-nowrap">vOffset = *v*</span> | Sets the vertical offset in points (positive offset is down, negative is up). Use this to create subscripts and superscripts. vOffset is allowed for formatted text files only, not for plain text files. |

**Notebook paragraph property parameters**

This section of Notebook relates to setting the paragraph properties of the current selection in the notebook.

The margins, spacing, justification, tabs and rulerDefaults keywords provide control over paragraph properties which are governed by rulers. These keywords, in conjunction with the ruler and newRuler keywords, allow you to set paragraph properties. They are allowed for formatted text notebooks only, not for plain text notebooks.

The ruler keywords are described in detail below. Before we get to the detail, you should understand the different things you can do with rulers.

There are four things you can do with a ruler:

|  |  |
| --- | --- |
| modify it | (analogous to manually adjusting a ruler) |
| redefine it | (analogous to the Redefine Ruler dialog) |
| create it | (analogous to the Define New Ruler dialog) |
| apply it | (analogous to selecting a ruler name from ruler pop-up menu). |

Igor's behavior in response to ruler keywords depends on the order in which the keywords appear.

To modify the ruler(s) for the selected paragraph(s), use the margins, spacing, justification, tabs and rulerDefaults keywords ***without*** using the newRuler or ruler keywords. For example:


```igor
Notebook Notebook0 tabs={36,144,288},justification=1
```

To redefine an existing ruler, invoke the ruler=*rulerName* keyword ***before*** any other keywords. For example:


```igor
Notebook Notebook0 ruler=Ruler1,tabs={36,144,288},justification=1
```

Unlike doing it manually, when you redefine an existing ruler using ruler=*rulerName*, Igor does not apply the ruler to the selected text. However, it does update any text governed by the redefined ruler.

To create a new ruler, invoke the newRuler=*rulerName* keyword ***before*** any other keywords. For example:


```igor
Notebook Notebook0 newRuler=Ruler1,tabs={36,144,288},justification=1
```

Unlike creating it manually, when you create a new ruler using newRuler=*rulerName*, Igor does not apply the new ruler to the selected text. If you do not set a particular ruler property when creating a new ruler, the property will be the same as for the Normal ruler. If the specified ruler already exists, newRuler=*rulerName* overwrites the existing ruler.

To apply an existing ruler to the selected text, invoke the ruler=*rulerName* keyword without any other keywords. For example:


```igor
Notebook Notebook0 ruler=ruler1
```

You or Igor will get confused if you mix ruler keywords with other types of keywords in the same command. It is alright, however to put a selection keyword at the start of the command. Mixing will not cause a crash or any drastic problem but it will likely produce results that you don't understand. To keep things clear, follow these rules:


-	If you use ruler=*rulerName* or newRuler=*rulerName*, put them before any other ruler keywords.


-	Don't mix ruler keywords with other kinds, except that it is alright to use the  selection keyword at the start of the command.


|  |  |
| --- | --- |
| justification=*j* |<table class="nested-table"><tbody><tr><td>*j*&nbsp;=0:</td><td>Left aligned.</td></tr><tr><td>*j*&nbsp;=1:</td><td>Center aligned.</td></tr><tr><td>*j*&nbsp;=2:</td><td>Right aligned.</td></tr><tr><td>*j*&nbsp;=3:</td><td>Fully justified.</td></tr></tbody></table>
| <span class="table-cell-nowrap">margins = {*indent*,*left*,*right* }</span> |  |
|  | *indent* sets the indentation of first line from left page margin. |
|  | *left* sets the paragraph's left margin in points measured from the left page margin. |
|  | *right* sets the paragraph's right margin in points measured from the left page margin. |
| <span class="table-cell-nowrap">newRuler = *rulerName*</span> | Creates a new ruler with the specified name. If a ruler with this name already exists, it is overwritten. |
| <span class="table-cell-nowrap">ruler = *rulerName*</span> | Apply the named ruler to the selected text or redefine the named ruler, as explained above. |
| <span class="table-cell-nowrap">rulerDefaults = {"*fontName* ", *fSize*, *fStyle*, (*r*,*g*,*b*[,*a*])}</span> |  |
|  | "*fontName*"  sets the ruler's text font, e.g., "Helvetica". |
|  | *fSize* sets the ruler's text size. |
|  | *fStyle* sets the ruler's text style. |
|  | (*r*,*g*,*b*[,*a*]) sets the ruler's text color. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque white. |
|  | You can use rulerDefaults only if you are redefining an existing ruler using ruler=*rulerName* or you are creating a new ruler using newRuler=*rulerName*. |
| <span class="table-cell-nowrap">spacing = {*spaceBefore*, *spaceAfter*, *lineSpace* }</span> |  |
|  | *spaceBefore* sets the extra space before paragraph in points. |
|  | *spaceAfter* sets the extra space after paragraph in points. |
|  | *lineSpace* sets the extra space between lines of a paragraph in points. |
| <span class="table-cell-nowrap">tabs = {*tabSpec* }</span> | *tabSpec* is list of tab stops in points added to special values that change the tab stop type. |
|  | Tab stops have two parts: the tab stop position and the tab type. Each integer in the list of tabs encodes both of these parts as follows: |
|  | The low 11 bits contains the tab stop position in points. |
|  | The next two bits are reserved for future use and must be zero. |
|  | The high three bits are used to contain the tab type as follows: |
|  |<table class="nested-table"><tbody><tr><td>left&nbsp;tab</td><td>0</td></tr><tr><td>center&nbsp;tab</td><td>1    add 1*8192 to tab stop position.</td></tr><tr><td>right&nbsp;tab</td><td>2    add 2*8192 to tab stop position.</td></tr><tr><td>decimal&nbsp;tab</td><td>3    add 3*8192 to tab stop position.</td></tr><tr><td>comma&nbsp;tab</td><td>4    add 4*8192 to tab stop position.</td></tr></tbody></table>

### *Tabs Example* {#tabs-example}
The following puts a left tab at 1 inch, a center tab at 3 inches and a decimal tab at 5 inches:


```igor
Notebook Notebook1 tabs={1*72, 3*72 + 8192, 5*72 + 3*8192}
```

**Notebook document property parameters**

This section of Notebook relates to setting the document properties of the notebook.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">adopt = *a*</span> | Adopts a notebook if it is a file saved to disk. Adopting a notebook makes it part of the packed experiment file, which becomes more self-contained; if you send the experiment to a colleague you will not need to send a notebook file. |
|  |<table class="nested-table"><tbody><tr><td>*a*&nbsp;=0:</td><td>Checks only whether the notebook is adoptable. Sets V_flag to 0 if the notebook is already adopted or to 1 if it is adoptable.</td></tr><tr><td>*a*&nbsp;=1:</td><td>Adopts the notebook (breaks the link to the file on disk). Sets V_flag to 1 if the adoption succeeded or to 0 if it did not (was already adopted, or some error).</td></tr></tbody></table>
| <span class="table-cell-nowrap">backRGB = (*r*,*g*,*b*[,*a*])</span> | Sets background color.  *r*, *g* and *b* are values from 0 to 65535. The default is opaque white. Alpha (*a*) is accepted but ignored. |
| <span class="table-cell-nowrap">changeableByCommandOnly = *c*</span> |  |
|  | The changeableByCommandOnly property is used to prevent manual modifications to the notebook but allow modifications using commands. |
|  |<table class="nested-table"><tbody><tr><td>*c*&nbsp;=0:</td><td>Turn changeableByCommandOnly off.</td></tr><tr><td>*c*&nbsp;=1:</td><td>Turn changeableByCommandOnly on.</td></tr></tbody></table>
|  | See [Notebook Read/Write Properties](/igorpro/igor-basics/notebooks.md#notebook-read-write-properties) for details. |
| <span class="table-cell-nowrap">defaultTab = *dtwp*</span> | *dtwp* is the default tab width in points. |
|  | The defaultTab keyword sets the default tab mode to 1 meaning that the default tab width for all paragraphs is specified in units of points. See the defaultTab2 keyword for further discussion. |
| <span class="table-cell-nowrap">defaultTab2 = {*mode*,*dtwp*,*dtws*}</span> |  |
|  | Controls the width of default tab stops. |
|  | The defaultTab2 keyword was added in Igor Pro 9.00. |
|  | *mode* is defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Points mode: The default tab width for all paragraphs is specified in units of points by *dtwp*.</td></tr><tr><td>2:</td><td>Spaces mode: The default tab width for all paragraphs is specified in units of spaces by *dtws*.</td></tr><tr><td>3:</td><td>Mixed mode: The default tab width for paragraphs controlled by proportional fonts is specified in units of points by *dtwp*. The default tab width for paragraphs controlled by monospace fonts is specified in units of spaces by *dtws*.</td></tr></tbody></table>
|  | Specify -1 for *mode* to leave the mode unchanged. |
|  | The space character unit used in mode 2 and in mode 3 for monospace fonts is the width of a space character in the ruler font for a given paragraph. Plain text notebooks have only one ruler so the space character width is the same for all paragraphs. Formatted text notebooks can have many rulers and each has an associated space character width. |
|  | *dtwp* is the default tab width in points. It is used in mode 1 and in mode 3 for proportional fonts. Specify -1 for *dtwp* to leave the default tab width in points unchanged. |
|  | *dtws* is the default tab width in spaces. It is used in mode 2 and in mode 3 for monospace fonts. Specify -1 for *dtwp* to leave the default tab width in spaces unchanged. |
|  | See [Notebook Default Tabs](/igorpro/igor-basics/notebooks.md#notebook-default-tabs) for further discussion. |
| <span class="table-cell-nowrap">magnification = *m*</span> | Specifies the desired magnification in percent (between 25 and 500). Otherwise, *m* can be one of these special values: |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=1:</td><td>Default magnification.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Default magnification.</td></tr><tr><td></td><td>In Igor Pro 6 this specified the no-longer-supported Fit Width mode.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Default magnification.</td></tr><tr><td></td><td>In Igor Pro 6 this specified the no-longer-supported Fit Page mode.</td></tr></tbody></table>
| <span class="table-cell-nowrap">pageMargins = {*left*, *top*, *right,* *bottom* }</span> |  |
|  | Sets page margins in points. *left*, *top*, *right* and *bottom* are distances from the respective edges of the physical page. Values are clipped to the range 0 to 1440 points (20 inches). |
|  | This setting overrides the margins set via the the page setup dialog and the PrintSettings operation margins keyword. |
| rulerUnits=*r* |<table class="nested-table"><tbody><tr><td>*r*&nbsp;=0:</td><td>Points.</td></tr><tr><td>*r*&nbsp;=1:</td><td>Inches.</td></tr><tr><td>*r*&nbsp;=2:</td><td>Centimeters..</td></tr></tbody></table>
| <span class="table-cell-nowrap">startPage = *sp*</span> | sets starting page number for printing. |
| showRuler=*s* |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Hide ruler</td></tr><tr><td>*s*&nbsp;=1:</td><td>Show ruler.</td></tr></tbody></table>
| <span class="table-cell-nowrap">statusWidth = *sw*</span> | As of Igor 7, because of changes to the layout of notebook windows, this keyword does nothing. |
|  | In Igor 6, it set the width in points of status area at left of the horizontal scroll bar. |
| <span class="table-cell-nowrap">userKillMode = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr></tbody></table>
| <span class="table-cell-nowrap">writeBOM = *w*</span> | Sets the document's writeBOM property which determines if Igor writes a byte order mark when saving the notebook. This applies to plain text notebooks only and is ignored for formatted text notebooks. |
|  |<table class="nested-table"><tbody><tr><td>*w*&nbsp;=-1:</td><td>Does not change writeBOM flag.</td></tr><tr><td>*w*&nbsp;=0:</td><td>Sets writeBOM to false.</td></tr><tr><td>*w*&nbsp;=1:</td><td>Sets writeBOM to true.</td></tr></tbody></table>
|  | See [Byte Order Marks](/igorpro/igor-basics/text-encodings.md#byte-order-marks) for details. |
|  | This keyword was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">writeProtect = *wp*</span> | The write-protect property is used to prevent inadvertent manual changes to the notebook. |
|  |<table class="nested-table"><tbody><tr><td>*wp*&nbsp;=0:</td><td>Turn write-protect off.</td></tr><tr><td>*wp*&nbsp;=1:</td><td>Turn write-protect on.</td></tr></tbody></table>
|  | See [Notebook Read/Write Properties](/igorpro/igor-basics/notebooks.md#notebook-read-write-properties) for details. |

**Notebook headers and footers**

You can turn headers and footers on and off and position headers and footers using the keywords in this section.

There is currently no way to set headers and footers except manually through the Document Settings dialog. You may be able to use stationery files to create files with specific headers and footers.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">footerControl = {*defaultFooter*, *firstFooter*, *evenOddFooter* }</span> |  |
|  | *defaultFooter* is 1 to turn the default footer on, 0 to turn it off. |
|  | *firstFooter* is 1 to turn the first page footer on, 0 to turn it off. |
|  | *evenOddFooter* is 1 to turn different footers for even and odd pages on, 0 to use the same footer for even and odd pages. |
| <span class="table-cell-nowrap">footerPos = *pos*</span> | *pos* is the position of the footer relative to the bottom of the page in points. |
| <span class="table-cell-nowrap">headerControl = {*defaultHeader*, *firstHeader*, *evenOddHeader* }</span> |  |
|  | *defaultHeader* is 1 to turn the default header on, 0 to turn it off. |
|  | *firstHeader* is 1 to turn the first page header on, 0 to turn it off. |
|  | *evenOddHeader* is 1 to turn different headers for even and odd pages on, 0 to use the same header for even and odd pages. |
| <span class="table-cell-nowrap">headerPos = *pos*</span> | *pos* is the position of the header relative to the top of the page in points. |

**Notebook miscellaneous property parameters**

This section of Notebook relates to ***setting miscellaneous properties*** of the notebook.

|  |  |
| --- | --- |
| autoSave=*v* |<table class="nested-table"><tbody><tr><td>*v*&nbsp;=&nbsp;0:</td><td>Notebook subwindow contents will not be saved in recreation macros.</td></tr><tr><td>*v*&nbsp;=&nbsp;1:</td><td>Notebook subwindow contents will be saved in recreation macros (default).</td></tr></tbody></table>
|  | This affects notebook subwindows in control panels only. Use autoSave=0 if you do not want the notebook's contents to be saved and restored when the control panel is recreated. Otherwise the notebook subwindow's contents will be restored when recreated. |
| <span class="table-cell-nowrap">frameInset = *i*</span> | Specifies the number of pixels by which to inset the frame of a notebook subwindow. Does not affect a normal notebook window. |
|  | This keyword was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">frameStyle = *f*</span> | Specifies the frame style for a notebook subwindow. Does not affect a normal notebook window. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>None</td></tr><tr><td>*f*&nbsp;=1:</td><td>Single</td></tr><tr><td>*f*&nbsp;=2:</td><td>Double</td></tr><tr><td>*f*&nbsp;=3:</td><td>Triple</td></tr><tr><td>*f*&nbsp;=4:</td><td>Shadow</td></tr><tr><td>*f*&nbsp;=5:</td><td>Indented</td></tr><tr><td>*f*&nbsp;=6:</td><td>Raised</td></tr><tr><td>*f*&nbsp;=7:</td><td>Text well</td></tr></tbody></table>
|  | The last three styles are fake 3D and will look best if the background color behind the subwindow is a light shade of gray. |
|  | This keyword was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">status = {*messageStr*, *flags* }</span> |  |
|  | Sets the message in the status area at the bottom left of the notebook window. |
|  | *flags* is interpreted bitwise. Message is erased when: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>Selection changes.</td></tr><tr><td>bit&nbsp;1:</td><td>Window is activated.</td></tr><tr><td>bit&nbsp;2:</td><td>Window is deactivated.</td></tr><tr><td>bit&nbsp;3:</td><td>Document is modified.</td></tr></tbody></table>
|  | If all bits are zero, the message stays until a new message comes along. All other bits are reserved for future use and should be zero. To set bit 0 and bit 3, use 2<sup>0</sup>+2<sup>3</sup> = 9 for *flags*. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">updating = {*flags*, *r* }</span> | Sets parameters related to the updating of special characters. |
|  | *flags* is interpreted bitwise: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>Suppress automatic periodic updating of date and time special characters. By default this bit is set so date and time special characters are updated only when the user explicitly requests it or during printing when they appear in headers and footers.</td></tr><tr><td>bit&nbsp;1:</td><td>Allow manual updating of special characters via the specialUpdate keyword or via the Special menu. By default this is cleared so manual updating is not allowed.</td></tr></tbody></table>
|  | All other bits are reserved for future use and should be zero. |
|  | *r* is the update rate in seconds for updating date and time special characters. |
|  | These settings have no effect on the updating of special characters in headers or footers. These characters are always automatically updated when the document is printed. |
|  | We recommend that you leave automatic updating off (set bit 0 of the *flags* parameter to 1) so that updating occurs only via the specialUpdate keyword or via the Special menu. |
| visible=*v* |<table class="nested-table"><tbody><tr><td>*v*&nbsp;=&nbsp;0:</td><td>Hides notebook.</td></tr><tr><td>*v*&nbsp;=&nbsp;1:</td><td>Shows notebook but does not make it top window.</td></tr><tr><td>*v*&nbsp;=&nbsp;2:</td><td>Shows notebook and makes it top window.</td></tr></tbody></table>

**Accessing notebook contents**


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">getData = *mode*</span> | Causes Igor to return the contents of the notebook in the S_value variable. The contents are binary data in a private Igor format encoded as text. The only use for this keyword is to transfer data from one notebook to another by calling getData followed by setData. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=&nbsp;1:</td><td>Stores in S_value plain text or formatted text data, depending on the type of the notebook, from the entire notebook.</td></tr><tr><td>*mode*&nbsp;=&nbsp;2:</td><td>Stores in S_value plain text data, regardless of the type of the notebook, from the entire notebook.</td></tr><tr><td>*mode*&nbsp;=&nbsp;3:</td><td>Stores in S_value plain text or formatted text data, depending on the type of the notebook, from the notebook selection only.</td></tr><tr><td>*mode*&nbsp;=&nbsp;4:</td><td>Stores in S_value plain text data, regardless of the type of the notebook, from the notebook selection only.</td></tr></tbody></table>
|  | See the Notebook In Panel example experiment for examples using getData and setData. |

**Writing notebook text parameters**

This section of Notebook relates to inserting text at the current selection in the notebook.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">text = *textStr*</span> | inserts the text at the current selection. |
|  | Before the text is inserted, Igor converts escape sequences in *textStr* as follows: |
|  |<table class="nested-table"><tbody><tr><td>\r</td><td>Carriage return</td></tr><tr><td>\n</td><td>Line feed</td></tr><tr><td>\t</td><td>Tab</td></tr><tr><td>\&quot;</td><td>Double-quote</td></tr><tr><td>\&#39;</td><td>Single-quote</td></tr><tr><td>\\</td><td>Backslash</td></tr></tbody></table>
|  | Then, it checks for illegal characters. The only character code that is illegal is zero (ASCII NUL character). If it finds an illegal character, Igor generates an error and does not insert the text. |
| <span class="table-cell-nowrap">setData = *dataStr*</span> | Inserts the data at the current selection. |
|  | *dataStr* is either a regular string expression or the result returned by Notebook getData. |
| <span class="table-cell-nowrap">zData = *dataStr*</span> | This keyword is used by Igor during the recreation of a notebook subwindow in a control panel. *dataStr* is encoded binary data created by Igor when the recreation macro was generated. It represents the contents of the notebook subwindow in a format private to Igor. |
| <span class="table-cell-nowrap">zDataEnd = 1</span> | This keyword is used by Igor during the recreation of a notebook subwindow in a control panel. It marks the end of encoded binary data created by Igor when the recreation macro was generated. |

**Writing notebook graphics parameters**

This section of Notebook relates to ***inserting graphics*** at the current selection in the notebook.

These graphics keywords are allowed for formatted text files only, not for plain text files.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">convertToPNG = *x*</span> | Converts all pictures in the current selection to the cross-platform PNG format. If the picture is already PNG, it does nothing. |
|  | *x* is the resolution expansion factor, an integer from 1 to 16 times screen resolution. *x* is clipped to legal limits. |
| <span class="table-cell-nowrap">frame = *f*</span> | Sets the frame used for the picture and insertPicture keywords. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>No frame (default).</td></tr><tr><td>*f*&nbsp;=1:</td><td>Single frame</td></tr><tr><td>*f*&nbsp;=2:</td><td>Double frame</td></tr><tr><td>*f*&nbsp;=3:</td><td>Triple border</td></tr><tr><td>*f*&nbsp;=4:</td><td>Shadow frame</td></tr></tbody></table>
| <span class="table-cell-nowrap">insertPicture = {*pictureName*, *pathName*, *filePath*, *options* }</span> |  |
|  | Inserts a picture from a file specified by *pathName* and *filePath*. The supported graphics file formats are listed under [Inserting Pictures](/igorpro/igor-basics/notebooks.md#inserting-pictures). |
|  | *pictureName* is the special character name (see [Special Character Names](/igorpro/igor-basics/notebooks.md#special-character-names)) to use for the inserted notebook picture or $"" to automatically assign a name. |
|  | *pathName* is the name of an Igor symbolic path created via [NewPath](/igorpro/commands/newpath.md) or $"" to use no path. |
|  | *filePath* is a full path to the file to be loaded or a partial path or simple file name relative to the specified symbolic path. |
|  | If *pathName* and *filePath* do not fully specify a file, an Open File dialog is displayed from which the user can choose the file to be inserted. |
|  | *options* is a bitwise parameter defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>If set, an Open File dialog is displayed even if the file is fully specified by *pathName* and *filePath*.</td></tr><tr><td>Bit&nbsp;1:</td><td>Determines what to do in the event of a name conflict. If set, the existing special character with the conflicting name is overwritten. If cleared, a unique name is created and used as the special character name for the inserted picture.</td></tr></tbody></table>
|  | All other bits are reserved and must be set to zero. |
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | The variable V_flag is set to 1 if the picture was inserted or to 0 otherwise, for example, if the user canceled from the Open File dialog. |
|  | The string variable S_name is set to the special character name of the picture that was inserted or to "" if no picture was inserted. |
|  | The string variable S_fileName is set to the full path of the file that was inserted or to "" if no picture was inserted. |
| <span class="table-cell-nowrap">picture = {*objectSpec*, *mode*, *flags* [, *expansion* ] }</span> |  |
|  | Inserts a picture based on the specified object. |
|  | *objectSpec* is usually just an object name, which is the name of a graph, table, page layout, Gizmo plot, or picture from Igor's picture gallery (Misc→Pictures). See further discussion below. |
|  | *mode* specifies the format of the picture as follows: |
|  |<table class="nested-table"><tbody><tr><td>**mode**</td><td>**Windows**</td></tr><tr><td>-9</td><td>SVG</td></tr><tr><td>-8</td><td>PDF</td></tr><tr><td>-7</td><td>TIFF</td></tr><tr><td>-6</td><td>JPEG</td></tr><tr><td>-5</td><td>PNG</td></tr><tr><td>-4</td><td>Device-independent bitmap</td></tr><tr><td>-2</td><td>8X Enhanced metafile</td></tr><tr><td>-1</td><td>8X Enhanced metafile</td></tr><tr><td>0</td><td>8X Enhanced metafile</td></tr><tr><td>1</td><td>8X Enhanced metafile</td></tr><tr><td>2</td><td>8X Enhanced metafile</td></tr><tr><td>4</td><td>8X Enhanced metafile</td></tr><tr><td>8</td><td>8X Enhanced metafile</td></tr></tbody></table>
|  | Modes -6, -7, -8, and -9 require Igor Pro 7.00 or later. |
|  | In Igor 7 and 8, mode=-8 produced EMF. As of Igor Pro 9.00, it produces PDF. If you were using -8 for EMF, change your code to use -2. |
|  | Mode -2 (EMF) is recommended for platform-specific graphics. Mode -5 (PNG) is recommended for platform-independent bitmap graphics. Mode -8 (PDF) is recommended for platform-independent vector graphics but see the note above about -8 on Windows. |
|  | If *objectSpec* names a Gizmo window, only modes -5, -6 or -7 are allowed. |
|  | Modes -2 through 8 are supported for backward compatibility. In previous versions of Igor, they selected other formats that are now obsolete. |
|  | See [Exporting Graphics (Windows)](/igorpro/graphing/making-figures/graphics.md#exporting-graphics-windows), and  [Metafile Formats](/igorpro/graphing/making-figures/graphics.md#metafile-formats) for further discussion of these formats. |
|  | *flags* is interpreted bitwise: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>0 for black and white, 1 for color.</td></tr></tbody></table>
|  | For color, set *flags* = 2<sup>0</sup> = 1. All other bits are reserved for future use and should be zero. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | *expansion* is optional and requires Igor Pro 7.00 or later. It affects only modes -5, -6, and -7. |
|  | *expansion* sets the expansion factor over screen resolution. *expansion* must be an integer between 1 and 8 and is usually 1, 2, 4 or 8. The default value is 1. |
| <span class="table-cell-nowrap">scaling = {*h*, *v* }</span> | Sets the scaling used for the selected picture or the *picture* and *insertPicture* keywords. |
|  | *h* is horizontal scaling of picture in percent. |
|  | *v* is vertical scaling of picture in percent. |

When using the *picture* keyword, you may include a coordinate specification after the object name in *objectSpec*. For example:


```igor
Notebook Notebook1 picture={Layout0(100, 50, 500, 700), 1, 1}
```

The coordinates are in points. A coordinate specification of (0, 0, 0, 0) behaves the same as no coordinate specification at all.

If the object is a graph, the coordinate specification determines the width and height of the graph. If you omit the coordinate specification, Igor takes the width and height from the graph window.

If the object is a layout, the coordinate specification identifies a section of the layout. If you omit the coordinate specification, Igor selects a section of the layout that includes all objects in the layout plus a small margin.

For any other kind of object, Igor ignores the coordinate specification if it is present.

The scaling and frame keywords apply to the selected picture, if any. If no picture is selected, they affect the insertion of a picture using the picture or insertPicture keywords. For example, this command inserts a picture of Graph0 with 50% scaling and a double frame:


```igor
Notebook Test1 scaling={50, 50}, frame=2, picture={Graph0, 1, 1}
```

If no picture is selected and no picture is inserted, scaling and frame have no effect.

### *InsertPicture Example* {#insertpicture-example}

```igor
Function InsertPictureFromFile(nb)
	String nb		// Notebook name or "" for top notebook

	if (strlen(nb) == 0)
		nb = WinName(0, 16, 1)
	endif

	if (strlen(nb) == 0)
		Abort "There are no notebooks"
	endif

	// Display Open File dialog to get the file to be inserted
	Variable refNum		// Required for Open but not really used
	String fileFilter = "Graphics Files:.eps,.jpg,.png;All Files:.*;"
	Open /D /R /F=fileFilter refNum
	String filePath = S_fileName
	if (strlen(filePath) == 0)
		Print "You cancelled"
		return -1
	endif

	Notebook $nb, insertPicture={$"", $"", filePath, 0}
	if (V_flag)	
		Print "Picture inserted"
	else
		Print "No picture inserted"
	endif

	return 0
End
```

**Save notebook pictures to files**

The savePicture keyword is allowed for formatted text files only, not for plain text files.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">savePicture = {*pictureName*, *pathName*, *filePath*, *options* }</span> |  |
|  | Saves a picture from a formatted text notebook to a file specified by *pathName* and *filePath*. |
|  | *pictureName* is the special character name (see [Special Character Names](/igorpro/igor-basics/notebooks.md#special-character-names)) of the picture to be saved or $"" to save the selected picture in which case one picture and one picture only must be selected in the notebook. |
|  | *pathName* is the name of an Igor symbolic path created via [NewPath](/igorpro/commands/newpath.md) or $"" to use no path. |
|  | *filePath* is a full path to the file to be written or a partial path or simple file name relative to the specified symbolic path. |
|  | If *pathName* and *filePath* do not fully specify a file, a Save File dialog is displayed in which the user can specify the file to be written. |
|  | *options* is a bitwise parameter defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>If set, a Save File dialog is displayed even if the file is fully specified by *pathName* and *filePath*.</td></tr><tr><td>Bit&nbsp;1:</td><td>If set, a file with the same name is overwritten if it exists. If cleared, a Save File dialog is displayed if the specified file already exists.</td></tr><tr><td>Bit&nbsp;2:</td><td>If set then the leaf name specified by *filePath* is ignored and a name is automatically generated based on the picture name.</td></tr></tbody></table>
|  | All other bits are reserved and must be set to zero. |
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | The variable V_flag is set to 1 if the picture was written or to 0 otherwise, for example, if the user canceled from the Save File dialog. |
|  | The string variable S_name is set to the special character name of the picture that was saved or to "" if no picture was saved. |
|  | The string variable S_fileName is set to the full path of the file that was written or to "" if no picture was written. |

**Writing special character parameters**

This section of Notebook relates to inserting special characters at the current selection in the notebook. To insert a notebook action, see [NotebookAction](/igorpro/commands/notebookaction.md).

The special characters are page break, short date, long date, abbreviated date and time. They act in some respects like a single character but have special properties. You can insert the special characters using the specialChar keyword.

The specialChar keyword is allowed for formatted text files only, not for plain text files.

Other special characters are allowed in headers and footers only and you cannot insert them in a document using the specialChar keyword. These are window title, page number and total pages.

The special characters other than page break character are dynamic. Igor updates them periodically.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">specialChar = {*type*, *flags*, *optionsStr* }</span> |  |
|  | *type* is the special character type as follows: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Page break.</td></tr><tr><td>2:</td><td>Short date.</td></tr><tr><td>3:</td><td>Long date.</td></tr><tr><td>4:</td><td>Abbreviated date.</td></tr><tr><td>5:</td><td>Time.</td></tr></tbody></table>
|  | *flags* is reserved for future use. You should pass 0 for flags. |
|  | *optionsStr* is reserved for future use. You should pass "" for *optionsStr*. |
| <span class="table-cell-nowrap">specialUpdate = *flags*</span> | Updates special characters in the notebook. |
|  | *flags* is interpreted bitwise: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>0 to update all special characters.</td></tr><tr><td></td><td>1 to update special characters in the selected text.</td></tr><tr><td>bit&nbsp;1:</td><td>If 0 and updating for the document is disabled, it generates an error.</td></tr><tr><td></td><td>If 1, updates regardless of whether updating is enabled or not.</td></tr></tbody></table>
|  | To set bit 1 , use 2<sup>1</sup> = 2 for *flags*. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. All other bits are reserved for future use and should be zero. |
|  | The specialUpdate keyword can update pictures of graphs, tables and page layouts that were created from windows in the current experiment. |

### *See Also* {#notebook-see-also}
[Notebooks](/igorpro/igor-basics/notebooks.md)

[NewNotebook](/igorpro/commands/newnotebook.md), [OpenNotebook](/igorpro/commands/opennotebook.md), [NotebookAction](/igorpro/commands/notebookaction.md)

[SpecialCharacterList](/igorpro/commands/specialcharacterlist.md), [SpecialCharacterInfo](/igorpro/commands/specialcharacterinfo.md)