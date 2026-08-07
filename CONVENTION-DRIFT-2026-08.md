# Cross-repo convention drift — August 2026

Survey of the Python packages under `~/GitHub`, against the baseline now written
into `global-CLAUDE.md`. **Nothing was changed in these repos** — this is the
report. Rows marked ⚠ are worth fixing; the rest is cosmetic.

## 1. Python version floor

| Repo | `requires-python` | `environment.yml` | |
|---|---|---|---|
| pyirena | `>=3.9` | `>=3.10,<3.14` | ⚠ contradicts itself |
| DataReporter | `>=3.9` | `3.11` | ⚠ contradicts itself |
| pyirena-ai | `>=3.10` | `>=3.10,<3.14` | ✔ baseline |
| MailToVault | `>=3.10` | `3.12` | ok |
| PCA_for_SAXS | `>=3.10` | `3.12` | ok |
| Matilda | `>=3.11` | `3.12` | higher floor |
| bait_mcp | `>=3.11` | — | higher floor |

**The expensive one:** `pyirena/CLAUDE.md` states *"Python 3.9 is the floor, so
no `match`, no PEP 604 `X | Y` in runtime annotations."* No environment you
actually ship or test against is 3.9 — `environment.yml` already requires
`>=3.10`. That sentence makes every session write deliberately dated code for a
platform nobody uses. Raising `requires-python` to `>=3.10` and deleting the
sentence is the single highest-value fix in this report.

Baseline: `>=3.10`, classifiers through 3.13, conda cap `<3.14`.

## 2. Build backend and versioning

| Repo | Backend | Version source |
|---|---|---|
| pyirena, MailToVault | setuptools≥77 | static |
| DataReporter, PCA_for_SAXS | setuptools≥64/68 | static |
| pyirena-ai | setuptools≥61 | `dynamic` → `__version__` attr |
| Matilda | hatchling + hatch-vcs | git tags ⚠ |
| bait_mcp | hatchling | static |

Three different version schemes across seven packages. Baseline: setuptools≥77
+ static version in `pyproject.toml` (which is what pyirena's publish workflow
already enforces against the git tag).

## 3. Lint and format ⚠

| Repo | line-length | ruff `select` | black? |
|---|---|---|---|
| pyirena | 100 | defaults, `ignore = [E741,E701,E702,E402]` | no |
| pyirena-ai | 100 | `E,F,W,I,B,UP` | ⚠ configured |
| DataReporter | 100 | defaults | ⚠ configured + dev dep |
| MailToVault | 100 | `E,F,W,I,UP,B,C4,SIM` | no |
| bait_mcp | 100 | `E,F,I,UP,B` | no |
| Matilda | **200** ⚠ | `E4,E7,E9,F,B006` | no |
| PCA_for_SAXS | — | no ruff config at all ⚠ | no |

Two real problems:

- **black is half-adopted.** Declared in `pyirena-ai` and `DataReporter`,
  absent elsewhere. Two formatters in one ecosystem means the same file gets
  reformatted differently depending on which repo it lands in. `ruff format`
  is a drop-in replacement — drop `[tool.black]` and the `black` dev dep.
- **`E741` is inconsistently suppressed.** pyirena and Matilda turn it off;
  `pyirena-ai`, `MailToVault` and `bait_mcp` select `E` without ignoring it, so
  `I = intensity` gets flagged there. This is exactly the pressure that renames
  physics notation into `intensity_array`. Suppress it everywhere.

Matilda's `line-length = 200` is annotated as deliberate ("legacy code has long
lines; do not fight it yet") — legitimate, but it should converge to 100 as the
legacy files get touched.

## 4. Qt toolkit ⚠ — real conflict

- `pyirena` → PySide6, in `[gui]` extra, behind `gui/_qt.py` shim ✔
- `MailToVault` → PySide6, in `[gui]` extra, behind `gui/_qt.py` shim ✔
- `Matilda` → PySide6 in `[gui]`, pinned `>=6.4,<6.8` (GLIBC 2.28 on RHEL 8)
- `DataReporter` → **PyQt6 as a core dependency** ⚠⚠

Matilda's own `pyproject.toml` carries the warning: *"install only ONE of
PySide6 or PyQt6 — having both on the same environment causes Qt platform-plugin
conflicts on macOS (cocoa not found)."* DataReporter violates that, and does it
in core deps rather than an extra — so a headless CLI install of DataReporter
drags Qt in, and any environment holding both DataReporter and pyirena is in the
exact failure mode Matilda documented.

Two changes, both contained: move PyQt6 → PySide6, and move it from
`dependencies` into a `[gui]` extra behind a `_qt.py` shim like the other two.

Also worth reconciling: pyirena pins `PySide6>=6.4.0,!=6.7.*,!=6.10.*` while
Matilda pins `>=6.4,<6.8`. Both constraints are justified, but they're
mutually incompatible in a shared environment.

## 5. Layout and housekeeping (cosmetic)

- **src-layout**: DataReporter, PCA_for_SAXS. Flat layout: everything else.
- **Tests**: `tests/` at repo root everywhere except pyirena (`pyirena/tests/`,
  excluded from the wheel — deliberate and documented, fine).
- **Plan file naming**: `IMPROVEMENT_PLAN.md` (pyirena, Matilda), `PLAN.md`
  (DataReporter, MailToVault, BeamlineAdvisor), `DEVELOPMENT_PLAN.md`
  (PCA_for_SAXS), `REFACTOR_PLAN.md` + `todo.md` (bait_mcp). Pick one name.
- **Missing `CHANGELOG.md`**: PCA_for_SAXS, bait_mcp, BeamlineAdvisor.
- **DataReporter author field** is still `DataReporter Authors
  <example@example.com>`.

## 6. Cost and efficiency notes

- `SAXS_IgorCode/CLAUDE.md` contained `@~/.claude/CLAUDE.md`. The global file
  loads automatically in Claude Code, so that line pulled it in a second time —
  the whole global file was being paid for twice in every Igor session.
  Removed.
- The old global file spent ~57 of 78 lines on Igor Pro rules that were loaded
  into every Python session too. Those lines now sit in
  `SAXS_IgorCode/CLAUDE.md`, where they're loaded only when relevant.
- The global file also duplicated the panel-geometry reference that
  `/igor-panel` already contains. When that skill fires you were paying for the
  same content twice. Global now points at the skills instead of restating them.
- **Only 5 of ~35 repos have a `CLAUDE.md`** (pyirena, SAXS_IgorCode, bait_mcp,
  bluesky-bits, and `custom-double-click` as `AGENTS.md`). For an active repo,
  a 25–40 line orientation file is strongly net-positive: it costs ~400 tokens
  per session and saves several thousand in exploratory grepping. Worth adding
  to Matilda, pyirena-ai, DataReporter and MailToVault.
- `pyirena/CLAUDE.md` at 220 lines is large but earns it — it's a genuine map of
  a seven-layer codebase and its §7 "maintaining this file" discipline is the
  right model. Use it as the template for the four repos above, scaled down.

## Suggested order of work

1. pyirena: `requires-python = ">=3.10"`, delete the 3.9 sentence from `CLAUDE.md`.
2. DataReporter: PyQt6 → PySide6, move to `[gui]` extra.
3. Drop `[tool.black]` from pyirena-ai and DataReporter; add `ignore = ["E741"]`
   to pyirena-ai, MailToVault, bait_mcp.
4. Add short `CLAUDE.md` to Matilda, pyirena-ai, DataReporter, MailToVault.
5. Everything else is cosmetic — fold in as those files get touched anyway.
