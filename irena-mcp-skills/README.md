# Irena / Indra / Nika — skills for AI agents driving Igor Pro via MCP

Experimental (started 2026-11). These skills teach an MCP-capable agent (Claude, Aida, ...)
how to use the **Indra** (USAXS/SAXS/WAXS reduction), **Irena** (SAS analysis) and **Nika**
(2D reduction) packages inside a running Igor Pro 10.05+ through the official
[Igor Pro MCP Server](https://docs.wavemetrics.com/igorpro/mcp-server).

- Use together with the generic `mcp skills/igor-pro` skill (Igor syntax, graphs, manual).
- **Prefer pyIrena / Matilda** (cross-platform, own MCP server) for new analysis work. This
  skill is for users who work in Igor experiments or need an Igor-only tool.
- The MCP server is Windows-only. It also works under CrossOver on macOS.

Status of covered workflows (tested 2026-11-26, Igor 10 in CrossOver):

| Workflow | Reference | Tested via MCP |
|---|---|---|
| Load packages | `references/loading-and-conventions.md` | yes, works |
| USAXS(+SAXS/WAXS) reduction, Indra 4 | `references/usaxs-reduction.md` | import mode works; FX4 raw recalculation not supported by Igor code |
| Import ASCII / NXcanSAS | `references/import-data.md` | yes, works (ASCII needs 2 extra globals) |
| Unified fit | `references/unified-fit.md` | fits run, but limit-warning DoAlerts block the agent |
| Size distribution | `references/size-distribution.md` | not yet |

Planning document: `SAXS_IgorCode/Planning/AGENT_CONTROL_PLAN.md`.

## Example MCP config (Igor under CrossOver, macOS)

```json
"igor": {
  "command": "/Applications/CrossOver.app/Contents/SharedSupport/CrossOver/bin/wine",
  "args": ["--bottle", "IgorPro10", "--cx-app",
           "C:\\users\\crossover\\AppData\\Local\\Programs\\WaveMetrics\\Igor Pro MCP Server\\igor-mcp-server.exe"]
}
```
In Igor: `Help → AI Tools → Allow AI Apps to Connect`.
