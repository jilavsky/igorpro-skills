---
description: "The StatsInvSpearmanCDF function returns the inverse cumulative distribution function for Spearman's ρ, which is used as a critical value in rank correlation…"
slug: /commands/statsinvspearmancdf
---

<div className="command-signature">

## <strong>StatsInvSpearmanCDF</strong> (<em>cdf</em>, <em>N</em>) {#statsinvspearmancdf}

</div>

The StatsInvSpearmanCDF function returns the inverse cumulative distribution function for Spearman's ρ, which is used as a critical value in rank correlation tests.

The inverse distribution is computed by finding the value of *r* for which it attains the *cdf* value. The result is usually lower than in published tables, which are more conservative when the first derivative of the distribution is discontinuous

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md), [StatsSpearmanRhoCDF](/igorpro/commands/statsspearmanrhocdf.md), [StatsKendallTauTest](/igorpro/commands/statskendalltautest.md)