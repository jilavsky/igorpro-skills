---
name: "IgorPanelLayout"
description: "Provides reference for creating Igor Pro panels, including standard control heights, vertical spacing, horizontal layout conventions, and the yPos accumulator pattern."
parameters: {}
---

# Instructions
You are an Igor Pro UI/UX expert. When this skill is invoked, use the following reference to assist in generating code for `NewPanel` and control layouts:

1. **The yPos Accumulator Pattern:** This is the most important rule. Always use a running `yPos` variable to manage vertical placement. Never hardcode absolute Y coordinates for every control, as this makes layouts brittle and difficult to modify.
2. **Standard Heights:** Use the provided pixel heights for different control types (e.g., `TitleBox` ~30px, `Button` ~22px, `CheckBox` ~16px) to ensure a professional look.
3. **Vertical Spacing:** Implement logical gaps between controls (e.g., 4–8px between different types, 8–15px between logical groups).
4. **Horizontal Layout:** Follow the width conventions for narrow (utility), standard, and wide panels. For two-column layouts, use the specified X positions for left and right columns.
5. **Header Pattern:** Every panel should start with a styled `TitleBox` and a decorative colored line (`fColor=(0,0,52224)`).
6. **Conditional Visibility:** Use the `disable=` parameter in a separate update function to show/hide controls dynamically, rather than creating/killing them at runtime.
7. **Panel Sizing:** Always calculate the total required height (including headers, gaps, and margins) before calling `NewPanel`. Add ~10% headroom to prevent clipping.

---

# Igor Pro Panel & Control Geometry Reference

This reference provides dimensions and patterns derived from professional SAXS Igor codebases.

**Repository Reference:** https://github.com/jilavsky/SAXS_IgorCode/tree/master/User%20Procedures

---

## 1. Standard Control Heights (pixels)

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

## 2. Vertical Spacing (pixels)

| Situation | Gap |
|-----------|-----|
| After panel title + decorative line | 5–8 px before first control |
| Between rows of same type (CheckBox row) | 0–2 px |
| Between different control types | 4–8 px |
| After a section TitleBox subtitle | 4–6 px |
| Between logical groups | 8–15 px (use TitleBox subtitle to mark) |
| Before action buttons at bottom | 10–20 px |

---

## 3. Horizontal Layout Conventions

### Panel Widths
- **Narrow utility panel:** 380–430 px (Single-column)
- **Standard panel:** 500–640 px (Two-column)
- **Wide panel:** 640–800 px (Multi-section)

### Two-Column Layout (Standard 640px Panel)
| Element | X Position | Width |
|---------|------------|-------|
| Left Column | 5 px | ~225 px |
| Right Column | 235 px | ~400 px |

---

## 4. The yPos Accumulator Pattern (Mandatory)

**Never hardcode Y coordinates.** Use a running variable to prevent overlapping and clipping.

```igor
Function MyPanel()
    // ── Layout constants ─────────────────────────────────────
    Variable panelLeft   = 3
    Variable panelTop    = 40
    Variable panelWidth  = 430
    Variable leftMargin  = 5
    Variable yPos        = 5     // running y position
    Variable ctrlGap     = 5     // standard gap between controls
    Variable groupGap    = 12    // gap between logical sections

    PauseUpdate
    NewPanel/K=1/W=(panelLeft, panelTop, panelLeft+panelWidth, panelTop+750)/N=MyPanel as "Tool"

    // ── Header ───────────────────────────────────────────────
    TitleBox MainTitle, title="My Panel", pos={20,yPos}, frame=0, fstyle=3
    TitleBox MainTitle, fixedSize=1, font="Times New Roman", size={panelWidth-40,24}
    TitleBox MainTitle, anchor=MC, fColor=(0,0,52224)
    yPos += 30

    TitleBox FakeLine1, title=" ", fixedSize=1, size={panelWidth-20,3}, pos={16,yPos}
    TitleBox FakeLine1, frame=0, fColor=(0,0,52224), labelBack=(0,0,52224)
    yPos += 3 + 8

    // ── Section 1 ────────────────────────────────────────────
    TitleBox Sect1, title="Input Data", pos={leftMargin,yPos}, frame=0, fstyle=3
    TitleBox Sect1, fixedSize=1, font="Times New Roman", size={panelWidth-20,22}, fSize=18
    TitleBox Sect1, fColor=(0,0,52224)
    yPos += 22 + 4

    PopupMenu MyMenu, pos={leftMargin,yPos}, size={panelWidth-10,21}, title="Type:"
    yPos += 21 + ctrlGap

    // ── Section 2 (Logical Group) ────────────────────────────
    yPos += groupGap
    TitleBox Sect2, title="Options", pos={leftMargin,yPos}, frame=0, fstyle=3
    TitleBox Sect2, fixedSize=1, font="Times New Roman", size={panelWidth-20,22}, fSize=18
    TitleBox Sect2, fColor=(0,0,52224)
    yPos += 22 + 4

    CheckBox MyCheck, pos={leftMargin,yPos}, size={16,14}, title="Enable?"
    yPos += 14 + ctrlGap

    // ── Action Buttons (Bottom) ──────────────────────────────
    yPos += 15 // breathing room
    Button RunBtn, pos={leftMargin,yPos}, size={200,22}, title="Run"
    Button RunBtn, proc=MyProc, fColor=(32768,65535,49386)
End
```

---

## 5. Conditional Visibility (disable= Pattern)

Instead of creating/killing controls, use the `disable` parameter in an update function.

```igor
// 1. Create control with initial state (e.g., hidden)
CheckBox AdvOpt, pos={5, yPos}, size={16,14}, title="Advanced?", disable=1

// 2. Update function called by checkbox/popup procs
Function MyPanel_UpdateVisibility()
    NVAR showAdv = root:Packages:MyPkg:ShowAdvanced
    // disable=0 (visible), 1 (hidden/space preserved), 2 (hidden/grayed)
    SetVariable AdvVal, win=MyPanelName, disable=(!showAdv)
End
```
