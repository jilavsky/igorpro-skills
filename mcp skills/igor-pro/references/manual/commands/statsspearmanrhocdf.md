---
description: "The StatsSpearmanRhoCDF function returns the cumulative distribution function for Spearman's ρ, which is used in rank correlation test."
slug: /commands/statsspearmanrhocdf
---

<div className="command-signature">

## <strong>StatsSpearmanRhoCDF</strong> (<em>r</em>, <em>N</em>) {#statsspearmanrhocdf}

</div>

The StatsSpearmanRhoCDF function returns the cumulative distribution function for Spearman's ρ, which is used in rank correlation test. It is valid for *N*>1 and -1<=*r* <= 1. The distribution is mostly computed using the Edgeworth series expansion.

### *References* {#references}
Algorithm AS 89, *Appl. Statist.*, *24*, 377, 1975.

van de Wiel, M.A., and A. Di Bucchianico, Fast computation of the exact null distribution of Spearman's rho and Page's L statistic for samples with and without ties, *J. of Stat. Plan. and Inferenc*e, *92*, 133-145, 2001..

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md), [StatsInvSpearmanCDF](/igorpro/commands/statsinvspearmancdf.md), [StatsKendallTauTest](/igorpro/commands/statskendalltautest.md)