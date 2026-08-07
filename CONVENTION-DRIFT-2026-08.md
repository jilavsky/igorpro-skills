# Cross-repo convention drift — August 2026

Survey of the Python packages under `~/GitHub`, against the baseline now written
into `global-CLAUDE.md`. Rows marked ⚠ are worth fixing; the rest is cosmetic.

**Status:** the pyirena items were applied 2026-08-07 and the Matilda items on
2026-08-07; both have been struck from this report. Everything remaining below
is still outstanding.

## 1. Python version floor

| Repo | `requires-python` | `environment.yml` | |
|---|---|---|---|
| pyirena | `>=3.10` | `>=3.10,<3.14` | ✔ baseline |
| DataReporter | `>=3.9` | `3.11` | ⚠ contradicts itself |
| pyirena-ai | `>=3.10` | `>=3.10,<3.14` | ✔ baseline |
| MailToVault | `>=3.10` | `3.12` | ok |
| PCA_for_SAXS | `>=3.10` | `3.12` | ok |
| Matilda | `>=3.11` | `3.12` | higher floor, reason documented ✔ |
| bait_mcp | `>=3.11` | — | higher floor |

Baseline: `>=3.10`, classifiers through 3.13, conda cap `<3.14`.

Matilda keeps `>=3.11` deliberately — server and CI matrix are 3.11/3.12, so
`>=3.10` would be an untested claim. The reason is now written next to the pin
in `pyproject.toml`, which is what the baseline asks for.

## 2. Build backend and versioning

| Repo | Backend | Version source |
|---|---|---|
| pyirena, MailToVault, Matilda | setuptools≥77 | static |
| DataReporter, PCA_for_SAXS | setuptools≥64/68 | static |
| pyirena-ai | setuptools≥61 | `dynamic` → `__version__` attr |
| bait_mcp | hatchling | static |

Baseline: setuptools≥77 + static version in `pyproject.toml` (which is what
pyirena's publish workflow already enforces against the git tag). Only
`pyirena-ai`'s `dynamic` → `__version__` scheme is still off-baseline, and it is
harmless.

## 3. Lint and format ⚠

| Repo | line-length | ruff `select` | black? |
|---|---|---|---|
| pyirena | 100 | `E,F,W,I`, `ignore = [E501,E741,E701,E702,E402]` | no |
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

pyirena took `W` and `I` on 2026-08-07 and deliberately deferred `UP` and `B`:
enabling them there is 1541 findings, of which ~1050 are annotation rewrites
(`Optional[X]` → `X | None`) and ~100 need hand review, including 7 genuine
`B023` loop-variable captures. Worth doing, but as its own reviewable pass — the
`B023` hits in particular are potential bugs, not style.

## 4. Qt toolkit 

- `pyirena` → PySide6, in `[gui]` extra, behind `gui/_qt.py` shim ✔
- `MailToVault` → PySide6, in `[gui]` extra, behind `gui/_qt.py` shim ✔
- `Matilda` → PySide6 in `[gui]`, pinned `>=6.4,<6.8` (GLIBC 2.28 on RHEL 8)
- `DataReporter` → PySide6 in [gui]

Also worth reconciling: pyirena pins `PySide6>=6.4.0,!=6.7.*,!=6.10.*` while
Matilda pins `>=6.4,<6.8`. Both constraints are justified. Correction to the
original report — they are *not* mutually incompatible: the intersection is
6.4.x–6.6.x, so a shared environment resolves, just onto an old Qt. Left
unchanged in both repos, since narrowing pyirena to match Matilda's RHEL 8
GLIBC cap would give up 6.8/6.9 for everyone else.

## 5. Layout and housekeeping (cosmetic)

- **src-layout**: DataReporter, PCA_for_SAXS. Flat layout: everything else.
- **Tests**: `tests/` at repo root everywhere except pyirena (`pyirena/tests/`,
  excluded from the wheel — deliberate and documented, fine).
- **Plan file naming**: `PLAN.md` (pyirena, DataReporter, MailToVault,
  BeamlineAdvisor, Matilda), `DEVELOPMENT_PLAN.md` (PCA_for_SAXS),
  `REFACTOR_PLAN.md` + `todo.md` (bait_mcp). `PLAN.md` is the baseline; the
  remaining two should converge.
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
- **Only 6 of ~35 repos have a `CLAUDE.md`** (pyirena, Matilda, SAXS_IgorCode,
  bait_mcp, bluesky-bits, and `custom-double-click` as `AGENTS.md`). For an
  active repo, a 25–40 line orientation file is strongly net-positive: it costs
  ~400 tokens per session and saves several thousand in exploratory grepping.
  Worth adding to pyirena-ai, DataReporter and MailToVault.
- `pyirena/CLAUDE.md` at 220 lines is large but earns it — it's a genuine map of
  a seven-layer codebase and its §7 "maintaining this file" discipline is the
  right model. Use it as the template for the four repos above, scaled down.

## Suggested order of work

1. DataReporter: `requires-python = ">=3.10"`.
2. Drop `[tool.black]` from pyirena-ai and DataReporter; add `ignore = ["E741"]`
   to pyirena-ai, MailToVault, bait_mcp.
3. Add short `CLAUDE.md` to pyirena-ai, DataReporter, MailToVault.
4. pyirena: separate pass for ruff `UP` + `B` (see §3) — the 7 `B023` findings
   should be looked at as possible bugs.
5. Matilda: same separate `UP` + `B` pass — currently 9 `UP`, 11 `B`, including
   2 `B023` loop-variable captures and 4 `B905` bare `zip()`. Small enough to be
   one reviewable commit, but it touches the reduction path, so not folded into
   the packaging cleanup.
6. Everything else is cosmetic — fold in as those files get touched anyway.

**Done:** pyirena floor → 3.10 (§1); pyirena ruff `E,F,W,I` (§3); DataReporter
PyQt6 → PySide6 in `[gui]` (§4); pyirena `IMPROVEMENT_PLAN.md` → `PLAN.md` (§5).
Matilda 2026-08-07: hatchling + hatch-vcs → setuptools≥77 + static version (§2);
`>=3.11` deviation documented in `pyproject.toml` (§1); `IMPROVEMENT_PLAN.md` →
`PLAN.md` (§5); `CLAUDE.md` added (§6). Still open there: `line-length = 200`
(§3, deliberate for now) and the `UP` + `B` pass above.
