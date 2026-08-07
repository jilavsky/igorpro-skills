# Global Claude Code Instructions — Jan Ilavsky

## Identity and context
Scientist at Argonne National Laboratory (APS beamline 12-ID/9-ID), working on
small-angle X-ray scattering (SAXS/USAXS/WAXS). Most code is **Python**
(pyIrena, Matilda, pyirena-ai, DataReporter, MailToVault, MCP servers). Igor
Pro 10 is maintained in exactly one repo, `SAXS_IgorCode`. macOS + Windows.

Scientific correctness outranks style, cleverness and refactoring everywhere.

## Read the repo's own CLAUDE.md first
Repo-level `CLAUDE.md` is authoritative and overrides anything here. Follow its
pointers instead of grepping the tree — the map exists so you don't have to
re-derive it every session.

## Python — house standard
Keep packages as similar as possible. Deviations need a reason written down
next to them (a comment in `pyproject.toml`, not just a commit message).

- **Version floor `>=3.10`**; support through 3.13; cap conda envs at `<3.14`.
  PEP 604 (`X | None`), `match`, and `zip(strict=)` are all fair game.
- **Build**: `setuptools>=77` + `wheel`. Static `version` in `pyproject.toml`
  is authoritative; do not add `hatch-vcs` or dynamic version schemes.
- **Layout**: flat package (`<pkg>/` at repo root), tests in top-level `tests/`.
- **Lint/format**: `ruff` only — no `black`, no `flake8`. `line-length = 100`,
  `select = ["E","F","W","I","UP","B"]`,
  `ignore = ["E501","E741","E701","E702","E402"]`.
  `E741` stays off permanently: `I` (intensity), `l` (level), `Q` are physics
  notation, not sloppy naming. Do not rename them to `intensity_array`.
- **Qt**: PySide6 only. Never add PyQt6 — the two collide in one environment.
  Qt belongs in an optional `[gui]` extra, never in core dependencies, and is
  always imported through a single `<pkg>/gui/_qt.py` shim.
- **Layering**: core math imports numpy/scipy only; no Qt and no matplotlib in
  core/io/batch/api layers. GUI panels stay thin — numpy loops belong in core.
- **Dependencies**: do not add one without asking. Prefer numpy, scipy, h5py,
  matplotlib, PySide6 — the set already in use.
- **Every repo carries**: `README.md`, `CHANGELOG.md`, `LICENSE`,
  `environment.yml` (conda env named after the package), `PLAN.md` for
  in-progress design work.

## Scientific conventions
- Q in Å⁻¹, intensity in cm⁻¹ (absolute) where calibration exists — state
  otherwise explicitly in the docstring.
- NXcanSAS HDF5 is the interchange format; preserve backwards compatibility of
  saved files, always. `from_dict()` supplies a default for every field.
- Keep Irena/Igor terminology and parameter names that users already know.
  When an algorithm comes from Irena, say so in the docstring.
- Results are validated against Igor Irena. A "cleaner" rewrite that shifts a
  numerical result is a regression, not an improvement.

## Igor Pro — SAXS_IgorCode only
Igor Pro 10, 64-bit only; never suggest 32-bit XOP patterns. Full conventions
live in `SAXS_IgorCode/CLAUDE.md`. Load the skills rather than guessing:
`/igor-commands`, `/igor-panel`, `/igor-wave-dfref`, `/igor-10`, `/igor-python`.

Non-negotiable even outside that repo:
- `Function`, never `Macro`. `Static Function` for internal helpers.
- Never reference a wave without a `WAVE` declaration; `WAVE/Z` + `WaveExists()`
  whenever it may not exist.
- Always save and restore the data folder (`DFREF saveDF = GetDataFolderDFR()`).
- Build a path string fully, then apply `$` once — never `$` mid-expression.
- Package globals live in `root:Packages:<PackageName>:`.
- Never guess command syntax: fetch
  `https://docs.wavemetrics.com/igorpro/commands/<name-lowercase>`.

## Working style
- Prefer extending the thing that already does 80% of the job over adding a
  parallel implementation.
- Ask before large refactors, before adding dependencies, and before changing
  a saved-file format.
- Comments and docstrings in English; Google-style docstrings on public APIs.
- Prefer explicit over implicit — name things clearly.
