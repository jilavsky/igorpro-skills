# Igor Pro Panel & Control Geometry Reference

This document is derived from real panel code in the SAXS_IgorCode repository
(Irena/Indra packages). Use these dimensions and patterns when generating any
NewPanel + control layout code. Users will likely fine-tune positions, but
starting from these numbers produces usable, non-overlapping layouts.

Repository reference: https://github.com/jilavsky/SAXS_IgorCode/tree/master/User%20Procedures

---

## 1. Standard Control Heights (pixels)

These are the heights actually used in the codebase. Use these as your defaults.

| Control type        | Height | Notes |
|---------------------|--------|-------|
| `TitleBox`          | 24–30  | Main panel title (fSize=22) |
| `TitleBox` subtitle | 18–22  | Section separator (fSize=18–20) |
| `TitleBox` line     | 3      | Decorative colored line (labelBack used) |
| `Button`            | 20–22  | Standard action button |
| `Button` small      | 15     | Secondary/utility button (e.g. GetHelp) |
| `CheckBox`          | 14–16  | Single checkbox |
| `SetVariable`       | 18–23  | Numeric or string input field |
| `PopupMenu`         | 21     | Dropdown selector |
| `ListBox`           | varies | Always set explicitly — 300–500px typical |
| `ValDisplay`        | 18     | Read-only value display |

---

## 2. Standard Vertical Spacing (pixels)

The vertical gap between consecutive controls:

| Situation | Gap |
|-----------|-----|
| After panel title + decorative line | 5–8 px before first control |
| Between rows of same type (CheckBox row) | 0–2 px (controls same height) |
| Between different control types | 4–8 px |
| After a section TitleBox subtitle | 4–6 px |
| Between logical groups | 8–15 px (use TitleBox subtitle to mark) |
| Before action buttons at bottom | 10–20 px |

**Key rule:** use a running `yPos` variable incremented by `controlHeight + gap`
rather than hardcoding each y coordinate independently.

---

## 3. Standard Horizontal Layout

### Panel width conventions

| Panel type | Total width | Notes |
|------------|-------------|-------|
| Narrow utility panel | 380–430 px | Single-column layout |
| Standard panel | 500–640 px | Two-column layout |
| Wide panel | 640–800 px | Multi-section layout |

### Left margin and column positions

| Element | Typical x position |
|---------|-------------------|
| Left edge margin | 5 px |
| Left column controls | x=5 |
| Right column start (two-column) | x=230–280 |
| Right edge button (e.g. GetHelp) | panelWidth - 90 |
| Full-width control left edge | x=5 |
| Full-width control width | panelWidth - 10 (leaves 5px margin each side) |

### Control widths (for a ~430px wide panel)

| Control | Width |
|---------|-------|
| Full-width Button | 400–420 px |
| Half-width Button | 180–200 px |
| Small utility Button (GetHelp etc.) | 80 px |
| Full-width SetVariable | 340–400 px |
| Half-width SetVariable | 165–200 px |
| Full-width PopupMenu | 185–400 px |
| ListBox (left column) | 220–260 px |
| CheckBox | 16 px (size) — title extends right automatically |

---

## 4. Title and Header Conventions

From the codebase, every panel uses this header pattern:

```igor
// Main title — always first, always styled this way:
TitleBox MainTitle, title="My Panel Title", pos={20,5}, frame=0, fstyle=3
TitleBox MainTitle, fixedSize=1, font="Times New Roman", size={400,24}
TitleBox MainTitle, anchor=MC, fColor=(0,0,52224)

// Decorative blue line immediately below title:
TitleBox FakeLine1, title=" ", fixedSize=1, size={330,3}, pos={16,40}
TitleBox FakeLine1, frame=0, fColor=(0,0,52224), labelBack=(0,0,52224)

// First content starts at y ≈ 50–55 (after title=30px + line=3px + gap=8px)
```

Section subtitles (to divide a panel into named groups):

```igor
TitleBox SectionTitle, title="Section Name", pos={left,yPos}, frame=0, fstyle=3
TitleBox SectionTitle, fixedSize=1, font="Times New Roman", size={panelWidth-20, 22}
TitleBox SectionTitle, fSize=18, fColor=(0,0,52224)
// yPos += 22 + 6  (subtitle height + gap before next control)
```

The blue color `(0,0,52224)` is the standard Irena/Indra house color for titles.

---

## 5. The yPos Accumulator Pattern

**Always use this pattern.** Never hardcode every y coordinate independently.
This is the most important rule for avoiding controls outside the panel.

```igor
Function MyPanel()
    // ── Layout constants ─────────────────────────────────────
    Variable panelLeft   = 3
    Variable panelTop    = 40
    Variable panelWidth  = 430
    Variable leftMargin  = 5
    Variable rightMargin = 5
    Variable colWidth    = panelWidth - leftMargin - rightMargin  // 420

    Variable yPos        = 5     // running y position
    Variable ctrlGap     = 5     // standard gap between controls
    Variable groupGap    = 12    // gap between logical sections

    // ── Estimate total height before creating panel ───────────
    // Count rows and sum: nRows * rowHeight + nGaps * gap + sections * 28
    // For a panel with ~20 rows of controls: estimate 20*22 + 20*5 + 3*28 = 624
    // Add ~60px for header, ~30px margin at bottom
    Variable panelHeight = 720   // adjust after laying out controls

    PauseUpdate
    NewPanel/K=1/W=(panelLeft, panelTop, panelLeft+panelWidth, panelTop+panelHeight)
    NewPanel/N=MyPanelName as "My Panel"

    // ── Header ───────────────────────────────────────────────
    TitleBox MainTitle, title="My Panel Title", pos={20,yPos}, frame=0, fstyle=3
    TitleBox MainTitle, fixedSize=1, font="Times New Roman", size={panelWidth-40,24}
    TitleBox MainTitle, anchor=MC, fColor=(0,0,52224)
    yPos += 30

    TitleBox FakeLine1, title=" ", fixedSize=1, size={panelWidth-20,3}, pos={16,yPos}
    TitleBox FakeLine1, frame=0, fColor=(0,0,52224), labelBack=(0,0,52224)
    yPos += 3 + 8    // line + gap before first control = y≈41

    // ── Section 1 ────────────────────────────────────────────
    TitleBox Sect1Title, title="Input Data", pos={leftMargin,yPos}, frame=0, fstyle=3
    TitleBox Sect1Title, fixedSize=1, font="Times New Roman", size={colWidth,22}, fSize=18
    TitleBox Sect1Title, fColor=(0,0,52224)
    yPos += 22 + 4

    PopupMenu DataTypePopup, pos={leftMargin,yPos}, size={colWidth,21}, title="Data type:"
    PopupMenu DataTypePopup, proc=MyPanel_PopMenuProc
    yPos += 21 + ctrlGap

    CheckBox UseErrors, pos={leftMargin,yPos}, size={16,14}, title="Use error bars?"
    CheckBox UseErrors, variable=root:Packages:MyPkg:UseErrors, proc=MyPanel_CheckProc
    yPos += 14 + ctrlGap

    SetVariable QMin, pos={leftMargin,yPos}, size={200,18}, title="Q min [1/A]:"
    SetVariable QMin, variable=root:Packages:MyPkg:QMin, limits={0,inf,0.001}
    yPos += 18 + ctrlGap

    SetVariable QMax, pos={leftMargin,yPos}, size={200,18}, title="Q max [1/A]:"
    SetVariable QMax, variable=root:Packages:MyPkg:QMax, limits={0,inf,0.001}
    yPos += 18 + groupGap

    // ── Section 2 ────────────────────────────────────────────
    TitleBox Sect2Title, title="Processing Options", pos={leftMargin,yPos}, frame=0, fstyle=3
    TitleBox Sect2Title, fixedSize=1, font="Times New Roman", size={colWidth,22}, fSize=18
    TitleBox Sect2Title, fColor=(0,0,52224)
    yPos += 22 + 4

    SetVariable BackgroundLevel, pos={leftMargin,yPos}, size={200,18}, title="Background:"
    SetVariable BackgroundLevel, variable=root:Packages:MyPkg:Background
    yPos += 18 + ctrlGap

    CheckBox SubtractBackground, pos={leftMargin,yPos}, size={16,14}, title="Subtract background?"
    CheckBox SubtractBackground, variable=root:Packages:MyPkg:SubtractBkg, proc=MyPanel_CheckProc
    yPos += 14 + groupGap

    // ── Action buttons (always at bottom) ─────────────────────
    yPos += 5   // extra breathing room before buttons
    Button RunAnalysis, pos={leftMargin,yPos}, size={200,22}, title="Run Analysis"
    Button RunAnalysis, proc=MyPanel_ButtonProc, fColor=(32768,65535,49386)
    Button RunAnalysis, help={"Run the analysis on selected data"}

    Button GetHelp, pos={panelWidth-90,yPos}, size={80,15}, title="Get Help"
    Button GetHelp, proc=MyPanel_ButtonProc, fColor=(65535,32768,32768)
    Button GetHelp, help={"Open online manual"}
    yPos += 22 + ctrlGap

    // ── Verify panel height is sufficient ─────────────────────
    // yPos at this point should be <= panelHeight set in NewPanel above.
    // If yPos > panelHeight, increase panelHeight and recreate.
    Print "Final yPos =", yPos, " Panel height =", panelHeight
End
```

---

## 6. Two-Column Layout Pattern

For wider panels (500–640px), content splits into left and right columns.
The left column typically holds the file/data list; the right holds controls.

```igor
// Two-column panel: 640px wide
// Left column:  x=5,   width=225  (file list)
// Right column: x=235, width=390  (controls)

Variable panelWidth  = 640
Variable leftColX    = 5
Variable leftColW    = 225
Variable rightColX   = 235
Variable rightColW   = panelWidth - rightColX - 5   // 400

Variable yPosLeft  = 55    // separate y trackers for each column
Variable yPosRight = 55

// Left column: ListBox occupies most of vertical space
ListBox ListOfAvailableData, pos={leftColX, yPosLeft}, size={leftColW, 400}
yPosLeft += 400 + 5

Button SelectAll,   pos={leftColX,      yPosLeft}, size={100,20}, title="Select All"
Button DeSelectAll, pos={leftColX+115,  yPosLeft}, size={100,20}, title="Deselect All"
yPosLeft += 20 + 5

// Right column: stacked controls
PopupMenu DataFormat, pos={rightColX, yPosRight}, size={rightColW, 21}, title="Format:"
yPosRight += 21 + 5

CheckBox SAXSData, pos={rightColX, yPosRight}, size={16,14}, title="SAXS data?"
yPosRight += 14 + 5

// Panel height = max(yPosLeft, yPosRight) + bottom margin
```

---

## 7. CheckBox Row Pattern

Multiple checkboxes on the same row (common in your code):

```igor
// Row of 4 checkboxes on one y position — each separated by ~80px
Variable cbY = yPos
CheckBox IncludeUSAXS, pos={leftMargin,      cbY}, size={16,14}, title="USAXS?"
CheckBox IncludeSAXS,  pos={leftMargin+80,   cbY}, size={16,14}, title="SAXS?"
CheckBox IncludeWAXS,  pos={leftMargin+160,  cbY}, size={16,14}, title="WAXS?"
CheckBox IncludeImage, pos={leftMargin+240,  cbY}, size={16,14}, title="Image?"
yPos += 14 + ctrlGap   // advance yPos once for the whole row
```

Spacing between checkboxes in a row: 75–85px center-to-center
(accounts for 16px box + title text of ~50–60px).

---

## 8. SetVariable + Label Pairs

SetVariable controls include their label in the `title=` parameter. The title
renders to the left of the input box. Budget approximately:

- Short title (8–12 chars): title takes ~80px, leave input box width of 100–120px → total 200px
- Medium title (14–20 chars): title takes ~110px, input box 90px → total 200px
- Long title (20+ chars): title takes ~150px, may need full `colWidth`

```igor
// Short title — 200px total is enough:
SetVariable QMin, pos={leftMargin,yPos}, size={200,18}, title="Q min [1/A]:"

// Long title — needs more width or split into two lines using \r:
SetVariable BlankFileName, pos={leftMargin,yPos}, size={345,23}, title="Selected Blank Name:"
```

---

## 9. Button Conventions

From the codebase, three distinct button styles are used consistently:

```igor
// Primary action button — green, full width or half width, 22px tall:
Button RunAnalysis, pos={leftMargin,yPos}, size={200,22}, title="Run Analysis"
Button RunAnalysis, proc=MyProc, fColor=(32768,65535,49386)

// Secondary action button — default color, smaller:
Button ImportData, pos={leftMargin,yPos}, size={180,20}, title="Import Selected Data"
Button ImportData, proc=MyProc

// Utility/help button — red, small, top-right corner:
Button GetHelp, pos={panelWidth-90,5}, size={80,15}, title="Get Help"
Button GetHelp, proc=MyProc, fColor=(65535,32768,32768)

// Destructive/kill button — placed away from main actions:
Button KillGraphs, pos={panelWidth-90,yPos}, size={80,15}, title="Kill graphs"
Button KillGraphs, proc=MyProc
```

---

## 10. Panel Sizing Formula

Calculate panel height bottom-up before writing `NewPanel`:

```
panelHeight = titleArea          (≈ 45px: title 30 + line 3 + gap 8 + spare 4)
            + sum of all control rows × (controlHeight + gap)
            + number of section subtitles × (22 + 4)
            + number of group gaps × 12
            + bottom margin (≈ 20–30px)
```

Practical shortcut for a single-column panel:
- Count total rows (each SetVariable, CheckBox, PopupMenu, Button = 1 row)
- Multiply by 25px average (height 18–22 + gap 4–5)
- Add 45px header + 25px per section subtitle + 30px bottom margin

For a panel with 20 rows, 3 sections: `45 + (20×25) + (3×25) + 30 = 650px`

**Always add 10% headroom** — it is much easier to have a slightly tall panel
than to have controls clipped at the bottom.

---

## 11. The disable= Pattern for Conditional Controls

Controls are shown/hidden dynamically using `disable=` in a separate update function.
This is cleaner than creating/killing controls at runtime.

```igor
// In panel creation — create ALL controls including ones that start hidden:
CheckBox AdvancedOption, pos={leftMargin,yPos}, size={16,14}, title="Advanced?"
CheckBox AdvancedOption, variable=root:Packages:MyPkg:ShowAdvanced, proc=MyCheckProc
yPos += 14 + ctrlGap

SetVariable AdvancedValue, pos={leftMargin,yPos}, size={200,18}, title="Adv. value:"
SetVariable AdvancedValue, variable=root:Packages:MyPkg:AdvancedValue
yPos += 18 + ctrlGap

// In a separate update function called from checkbox/popup procs:
Function MyPanel_UpdateVisibility()
    NVAR showAdv = root:Packages:MyPkg:ShowAdvanced
    SetVariable AdvancedValue, win=MyPanelName, disable=(!showAdv)
    // disable=0 → visible; disable=1 → hidden but space preserved; disable=2 → hidden, no space
End
```

`disable` values:
- `0` — visible and active
- `1` — hidden, space preserved (control area is blank)
- `2` — hidden and grayed (visible but inactive)

Note: `disable=1` leaves a gap where the control was. If you want no gap,
reorganize controls so hidden ones are at the bottom of their section.

---

## 12. Full Working Example — Minimal Panel

A complete, immediately usable panel template following all conventions above:

```igor
Function MyAnalysisPanel()
    KillWindow/Z MyAnalysisPanel
    MyAnalysis_Init()
    MyAnalysis_PanelFnct()
End

Function MyAnalysis_PanelFnct()
    Variable panelWidth = 430
    Variable leftMargin = 5
    Variable colWidth   = panelWidth - leftMargin - 5
    Variable yPos       = 5
    Variable ctrlGap    = 5
    Variable groupGap   = 12

    PauseUpdate
    NewPanel/K=1/W=(3,40,3+panelWidth,40+750)/N=MyAnalysisPanel as "My Analysis Tool"

    // Header
    TitleBox MainTitle, title="My Analysis Tool", pos={20,yPos}, frame=0, fstyle=3
    TitleBox MainTitle, fixedSize=1, font="Times New Roman", size={panelWidth-40,24}
    TitleBox MainTitle, anchor=MC, fColor=(0,0,52224)
    yPos += 30
    TitleBox FakeLine1, title=" ", fixedSize=1, size={panelWidth-20,3}, pos={16,yPos}
    TitleBox FakeLine1, frame=0, fColor=(0,0,52224), labelBack=(0,0,52224)
    yPos += 3 + 8

    // GetHelp button — fixed in top-right corner independent of yPos
    Button GetHelp, pos={panelWidth-90,35}, size={80,15}, title="Get Help"
    Button GetHelp, proc=MyAnalysis_ButtonProc, fColor=(65535,32768,32768)

    // Section 1: Data selection
    TitleBox DataSect, title="Data Selection", pos={leftMargin,yPos}, frame=0, fstyle=3
    TitleBox DataSect, fixedSize=1, font="Times New Roman", size={colWidth,22}, fSize=18
    TitleBox DataSect, fColor=(0,0,52224)
    yPos += 22 + 4

    PopupMenu DataFolder, pos={leftMargin,yPos}, size={colWidth,21}, title="Data folder:"
    PopupMenu DataFolder, proc=MyAnalysis_PopMenuProc
    PopupMenu DataFolder, value="---", mode=1
    yPos += 21 + ctrlGap

    SetVariable QMin, pos={leftMargin,yPos}, size={200,18}, title="Q min [1/A]:"
    SetVariable QMin, variable=root:Packages:MyAnalysis:QMin, limits={0,inf,0}
    yPos += 18 + ctrlGap

    SetVariable QMax, pos={leftMargin,yPos}, size={200,18}, title="Q max [1/A]:"
    SetVariable QMax, variable=root:Packages:MyAnalysis:QMax, limits={0,inf,0}
    yPos += 18 + groupGap

    // Section 2: Options
    TitleBox OptSect, title="Options", pos={leftMargin,yPos}, frame=0, fstyle=3
    TitleBox OptSect, fixedSize=1, font="Times New Roman", size={colWidth,22}, fSize=18
    TitleBox OptSect, fColor=(0,0,52224)
    yPos += 22 + 4

    CheckBox UseWeights, pos={leftMargin,yPos}, size={16,14}, title="Use error weighting?"
    CheckBox UseWeights, variable=root:Packages:MyAnalysis:UseWeights
    CheckBox UseWeights, proc=MyAnalysis_CheckProc, mode=0
    yPos += 14 + ctrlGap

    SetVariable BackgroundLevel, pos={leftMargin,yPos}, size={200,18}, title="Background:"
    SetVariable BackgroundLevel, variable=root:Packages:MyAnalysis:Background
    yPos += 18 + groupGap

    // Section 3: Results (display only)
    TitleBox ResultsSect, title="Results", pos={leftMargin,yPos}, frame=0, fstyle=3
    TitleBox ResultsSect, fixedSize=1, font="Times New Roman", size={colWidth,22}, fSize=18
    TitleBox ResultsSect, fColor=(0,0,52224)
    yPos += 22 + 4

    ValDisplay FitResult, pos={leftMargin,yPos}, size={200,18}, title="Rg [nm]:"
    ValDisplay FitResult, value=#"root:Packages:MyAnalysis:ResultRg"
    yPos += 18 + groupGap

    // Action buttons at bottom
    yPos += 5
    Button RunFit, pos={leftMargin,yPos}, size={200,22}, title="Run Fit"
    Button RunFit, proc=MyAnalysis_ButtonProc, fColor=(32768,65535,49386)
    Button RunFit, help={"Fit the data with the selected model"}
    yPos += 22 + ctrlGap

    Button SaveResults, pos={leftMargin,yPos}, size={200,20}, title="Save Results"
    Button SaveResults, proc=MyAnalysis_ButtonProc
    yPos += 20 + ctrlGap

    // Sanity check: print final yPos so you can verify against panel height
    // Panel height was set to 750 — if yPos > 750, increase it.
    // Remove this print line once layout is confirmed.
    Print "Panel layout complete, yPos =", yPos
End
```

---

## 13. Common Pitfalls to Avoid

**Controls placed outside panel bounds**
Always verify: last `yPos` value < panel height declared in `NewPanel/W=`.
If unsure, set panel height to 900px and shrink after confirming final yPos.

**Forgetting PauseUpdate**
Always call `PauseUpdate` as the first line of a panel-building function.
Without it, the panel redraws after every control added — very slow and
sometimes causes visual glitches.

**Hardcoding y positions without a running variable**
If you later insert a new control in the middle, every subsequent hardcoded
y coordinate must be manually adjusted. The yPos pattern avoids this entirely.

**CheckBox size parameter**
The `size={}` for CheckBox specifies only the checkbox square itself (16×14).
The title text renders to the right and is not clipped by size. Do not try to
set size to include the title width.

**SetVariable title vs. value width**
The `size=` of SetVariable includes both the title label AND the input box.
A `size={200,18}` with `title="Q min [1/A]:"` allocates 200px total; the
label takes roughly 90px, leaving ~110px for the input field. For very long
titles, increase size or abbreviate the title.

**Two-statement controls**
Button, CheckBox, SetVariable etc. can span two lines (name repeated):

```igor
Button MyButton, pos={5,100}, size={200,22}, title="Do Something"
Button MyButton, proc=MyProc, help={"Tooltip text"}, fColor=(32768,65535,49386)
```

This is valid Igor syntax — the second line modifies the same control.
