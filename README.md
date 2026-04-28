# Igor Pro — Claude Code Skills and Memory Files

This folder contains [Claude Code](https://code.claude.com) memory and skill
files that significantly improve AI-assisted Igor Pro programming. They are
designed for use with **Igor Pro 9 and 10** on macOS and Windows.

These files were developed at the APS beamline 12-ID (Argonne National
Laboratory) for the [Irena](https://usaxs.xray.aps.anl.gov/software/irena), 
[Nika](https://usaxs.xray.aps.anl.gov/software/nika),
and [Indra](https://usaxs.xray.aps.anl.gov/software/indra) SAXS/USAXS
data reduction and analysis packages, but are general enough to benefit any Igor Pro project.

---

## Why This Exists

Claude's general training data contains limited Igor Pro knowledge, and
essentially none for:

- Igor Pro 10 breaking changes and new features
- The `igorpro` Python module (proprietary to Igor, not on PyPI)
- Correct panel/GUI geometry and layout patterns
- The precise WAVE/DFREF reference syntax that avoids silent bugs

Without guidance, Claude generates Igor code that often:
- Uses waves without proper `WAVE` reference declarations
- Forgets to save/restore the current data folder
- Places panel controls outside the panel bounds or overlapping
- Invents non-existent flags for operations
- Writes Python code using a hallucinated `igorpro` API

These skill files fix all of that.

---

## Repository Structure

```
IgorPro-skills/
├── .claude/
│   └── skills/
│       ├── igor-commands/
│       │   └── SKILL.md       # All 1060+ built-in commands with doc links
│       ├── igor-10/
│       │   └── SKILL.md       # Igor Pro 10 new features and breaking changes
│       ├── igor-wave-dfref/
│       │   └── SKILL.md       # WAVE/DFREF/NVAR/SVAR reference syntax
│       ├── igor-panel/
│       │   └── SKILL.md       # Panel geometry, control sizes, layout patterns
│       └── igor-python/
│           └── SKILL.md       # igorpro Python module complete API reference
├── global-CLAUDE.md           # Template for ~/.claude/CLAUDE.md (global, all projects)
├── project-CLAUDE.md          # Template CLAUDE.md for your Igor project repos
├── .gitignore
└── README.md
```

The `.claude/skills/` folder is the distributable unit — copy it into any Igor
project repo, or into `~/.claude/` to apply the skills globally across all projects.

The two `CLAUDE.md` templates are starting points you edit for your own context:
- [`global-CLAUDE.md`](global-CLAUDE.md) → copy to `~/.claude/CLAUDE.md`
- [`project-CLAUDE.md`](project-CLAUDE.md) → copy to `<your-igor-repo>/CLAUDE.md`

---

## Installation

### Option A — Global installation (skills available in all your projects)

```bash
git clone https://github.com/ilavsky/IgorPro-skills
mkdir -p ~/.claude
cp -r IgorPro-skills/.claude/skills ~/.claude/
cp IgorPro-skills/global-CLAUDE.md ~/.claude/CLAUDE.md
```

Edit `~/.claude/CLAUDE.md` to reflect your own name, facility, and personal
conventions. The skills are now active in every Claude Code session.

### Option B — Per-project installation

```bash
git clone https://github.com/ilavsky/IgorPro-skills
cp -r IgorPro-skills/.claude /path/to/your/igor/project/
cp IgorPro-skills/project-CLAUDE.md /path/to/your/igor/project/CLAUDE.md
```

Then edit `CLAUDE.md` in your project root to describe your specific
package structure and helper functions.

### Option C — Both (recommended)

Install globally so skills are always available, and add a project `CLAUDE.md`
to each Igor repo to give Claude context about that project's conventions.

### (Optional) Personal CLAUDE.local.md

For personal notes that should not be committed:

```bash
touch CLAUDE.local.md
echo "CLAUDE.local.md" >> .gitignore
```

---

## How Claude Code Uses These Files

Claude Code loads memory files automatically using a cascading hierarchy:

| File | When loaded |
|------|-------------|
| `~/.claude/CLAUDE.md` | Every session, all projects |
| `<repo>/CLAUDE.md` | Every session in this project |
| `<repo>/CLAUDE.local.md` | Every session, personal only (gitignored) |
| `.claude/skills/<name>/SKILL.md` | On demand, when relevant |

The **global** and **project** `CLAUDE.md` files are loaded at the start of
every conversation. Keep them concise — they consume context window space in
every session regardless of what you are working on.

**Skills** are different: they are only loaded when Claude determines they
are relevant to the current task, or when you invoke them explicitly. This
means the large reference files (like the full command list) do not cost
context window space unless actually needed.

---

## Using Skills Explicitly

You can invoke any skill by name in your prompt:

```
Use the igor-panel skill to help me build a panel for this analysis tool.
```

```
Following the igor-wave-dfref skill, refactor this function to use proper
DFREF parameters instead of SetDataFolder.
```

```
Using the igor-python skill, write a Python script that reads all waves
from root:SAS and computes the Guinier Rg for each one.
```

You can also reference a skill file directly with `@` syntax:

```
@.claude/skills/igor-panel/SKILL.md
Help me lay out these 12 controls in a panel that is 430px wide.
```

---

## Skill Descriptions

### `/igor-commands` — Built-in Command Index

A complete alphabetical list of all 1060+ Igor Pro built-in operations and
functions, each with a direct link to its official documentation page.

**Use when:** you need to know what built-in commands exist, or need the
exact URL to look up a command's flags, output variables, and examples.

The URL pattern for any command is:
```
https://docs.wavemetrics.com/igorpro/commands/<commandname-lowercase>
```

Claude Code can fetch these pages on demand to get precise syntax rather
than guessing.

---

### `/igor-10` — Igor Pro 10 Changes

Covers all Igor Pro 10 features and breaking changes that affect code
generation, including:

- Python integration (`Python`, `PythonFile`, `PythonEnv` operations)
- New compiler errors (unreachable code in `switch`, `#pragma independentModule=ProcGlobal`)
- New language features (`DFREF` in Multiple Return Syntax, `#pragma moduleName` in main Procedure)
- New `MatrixOP` functions and `/K=4` window flag
- Bug fixes that silently change results (`area()`, `faverage()`, `CurveFit` subranges)

**Use when:** writing any Igor 10-specific code, using Python integration,
or debugging behavior differences from earlier Igor versions.

---

### `/igor-wave-dfref` — Wave and Data Folder Reference Syntax

The most impactful skill for avoiding subtle bugs. Covers:

- The core `WAVE` / `WAVE/Z` / `WaveExists()` pattern
- Passing waves as function parameters
- Returning wave references from functions
- `NVAR` and `SVAR` for global variables
- `DFREF` data folder references and navigation
- Free waves (`Make/FREE`) and free data folders
- The `$` operator for dynamic name resolution
- Common pitfalls: forgetting to restore the current data folder,
  using `$` mid-path, returning free waves unsafely

**Use when:** writing any function that handles waves, data folders, or
global variables — which is most Igor code.

---

### `/igor-panel` — Panel Geometry and GUI Layout

Derived from real panel code in the Irena/Indra codebase. Covers:

- Standard pixel heights for every control type
- Vertical and horizontal spacing conventions
- The `yPos` accumulator pattern (use this — never hardcode every coordinate)
- Panel height calculation formula
- Two-column layout pattern
- Checkbox row pattern
- Title and header conventions (including the Irena house style)
- The `disable=` pattern for conditional control visibility
- A complete minimal panel template ready to copy and modify

**Use when:** building any new panel or adding controls to an existing one.

---

### `/igor-python` — igorpro Python Module

Complete API reference for the `igorpro` module, which is proprietary to
Igor Pro 10 and has no presence in general Python training data. Covers:

- `igorpro.execute()`, `igorpro.print()`, `igorpro.version()`
- `igorpro.wave` — create, access, read, modify, get statistics
- `igorpro.folder` — navigate and manipulate data folders
- `igorpro.variable` and `igorpro.string` — global Igor variables
- `igorpro.fn` — call any Igor built-in or user function from Python
- `igorpro.WaveType` enumeration and NumPy ↔ Igor type mappings
- `igorpro.fn` limitations (what it cannot call and why)
- Setup: virtual environments, sys.path, VSCode autocomplete configuration
- SAXS-specific patterns: batch processing sample folders, Guinier fitting,
  writing results back to Igor

**Use when:** writing any `.py` file intended to be run from within Igor Pro,
or writing Igor procedure code that calls Python.

---

## Keeping Skills Up to Date

The official Igor Pro documentation lives at:
- **Commands:** https://docs.wavemetrics.com/igorpro/commands
- **Python module:** https://docs.wavemetrics.com/igorpro/python/python-module-reference
- **What's new in Igor 10:** https://docs.wavemetrics.com/igorpro/igor-pro-10/what-s-new-in-igor-pro-10
- **Changes since 10.00:** https://docs.wavemetrics.com/igorpro/igor-pro-10/what-s-changed-since-igor-pro-10-00

When WaveMetrics releases a new Igor Pro 10 point release, update
`.claude/skills/igor-10/SKILL.md` with any new breaking changes or new
functions. The commands index and Python module reference are stable between
point releases.

---

## Contributing

If you add skill files for other Igor topics (e.g. HDF5 patterns, specific
XOP APIs, curve fitting conventions), follow the same structure:

```
.claude/skills/<skill-name>/SKILL.md
```

Keep skill files focused and practical — they should answer the question
"what would Claude get wrong without this?" not serve as a general tutorial.
Include working code examples wherever possible.

---

## Compatibility

| Tool | Support |
|------|---------|
| Claude Code (CLI + VSCode extension) | ✅ Full support — skills and CLAUDE.md |
| Claude.ai Projects | ✅ Attach skill `.md` files as project documents |
| AnythingLLM | ✅ Use as embedded documents in a workspace |
| Other editors (Cursor, Zed, etc.) | ⚠️ Rename `CLAUDE.md` → `AGENTS.md` for cross-tool support |

---

## License

Same license as the parent repository.
