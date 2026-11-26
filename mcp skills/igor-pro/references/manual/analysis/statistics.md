---
description: "This help file describes operations and functions for statistical analysis together with some general guidelines for their use."
slug: /analysis/statistics
---

# Statistical Analysis {#statistical-analysis}

This help file describes operations and functions for statistical analysis together with some general guidelines for their use. This is not a statistics tutorial; for that you can consult one of the references at the end of this help file or the references listed in the documentation of a particular operation or function. The material below assumes that you are familiar with techniques and methods of statistical analysis.

Most statistics operations and functions are named with the prefix "Stats". Naming exceptions include the random noise functions which have traditionally been named based on the distribution they represent.

There are six natural groups of statistics operations and functions. They include:


-	Test operations


-	Noise functions


-	Probability distribution functions (PDFs)


-	Cumulative distribution functions (CDFs)


-	Inverse cumulative distribution functions


-	General purpose statistics operations and functions



## Statistical Test Operations {#statistical-test-operations}

Test operations analyze the input data to examine the validity of a specific hypothesis. The common test involves a computation of some numeric value (also known as "test statistic") which is usually compared with a critical value in order to determine if you should accept or reject the test hypothesis (H<sub>0</sub>). Most tests compute a critical value for the given significance *alpha* which has the default value 0.05 or a user-provided value via the /ALPH flag. Some tests directly compute the P-value which you can compare to the desired significance value.

In the past, critical values have been published in tables for various significance levels and tails of distributions. They are by far the most difficult technical aspect in implementating statistical tests. The critical values are usually obtained from the inverse of the CDF for the particular distribution, i.e., from solving the equation

$$
\displaystyle { cdf }({ criticalValue })=1- { alpha },
$$

where *alpha*  is the significance. In some distributions (e.g., Friedman's) the calculation of the CDF is so computationally intensive that it is impractical (using desktop computers in 2006) to compute for very large parameters. Fortunately, large parameters usually imply that the distributions can be approximated using simpler expressions. Igor's tests provide whenever possible exact critical values as well as the common relevant approximations.

Comparison of critical values with published table values can sometimes be interesting as there does not appear to be a standard for determining the published critical value when the CDF takes a finite number of discrete values (step-like). In this case the CDF attains the value (1-*alpha*) in a vertical transition so one could use the x-value for the vertical transition as a critical value or the x-value of the subsequent vertical transition. Some tables reflect a "convervative" approach and print the x-value of subsequent transitions.

Statistical test operations can print their results to the history area of the command window and save them in a wave in the current data folder. Result waves have a fixed name associated with the operation. Elements in the wave are designated by dimension labels. You can use the /T flag to display the results of the operation in a table with dimension labels. The argument for this flag determines what happens when you kill the table. You can use /Q in all test operations to prevent printing information in the history area and you can use the /Z flag to make sure that the operations do not report errors except by setting the V_Flag variable to -1.

Statistical test operations tend to include several variations of the named test. You can usually choose to execute one or more variations by specifying the appropriate flags. The following table can be used as a guide for identifying the operation associated with a given test name.

### Statistical Test Operations by Name {#statistical-test-operations-by-name}




| Test Name | Where to find it |
| --- | --- |
| Angular Distance | [StatsAngularDistanceTest](/igorpro/commands/statsangulardistancetest.md) |
| Bartlett's test for variances | [StatsVariancesTest](/igorpro/commands/statsvariancestest.md) |
| BootStrap | [StatsResample](/igorpro/commands/statsresample.md) |
| Brown and Forsythe | [StatsANOVA1Test](/igorpro/commands/statsanova1test.md) |
| Chi-squared test for means | [StatsChiTest](/igorpro/commands/statschitest.md) |
| Cochran's test | [StatsCochranTest](/igorpro/commands/statscochrantest.md) |
| Dunn-Holland-Wolfe | [StatsNPMCTest](/igorpro/commands/statsnpmctest.md) |
| Dunnette multicomparison test | [StatsDunnettTest](/igorpro/commands/statsdunnetttest.md), [StatsLinearRegression](/igorpro/commands/statslinearregression.md) |
| Fisher's Exact Test | [StatsContingencyTable](/igorpro/commands/statscontingencytable.md) |
| Fixed Effect Model | [StatsANOVA1Test](/igorpro/commands/statsanova1test.md) |
| Friedman test on randomized block | [StatsFriedmanTest](/igorpro/commands/statsfriedmantest.md) |
| F-test on two distributions | [StatsFTest](/igorpro/commands/statsftest.md) |
| Hartigan test for unimodality | [StatsDIPTest](/igorpro/commands/statsdiptest.md) |
| Hodges-Ajne (Batschelet) | [StatsHodgesAjneTest](/igorpro/commands/statshodgesajnetest.md) |
| Hotelling | [StatsCircularTwoSampleTest](/igorpro/commands/statscirculartwosampletest.md), [StatsCircularMeans](/igorpro/commands/statscircularmeans.md) |
| Jackknife | [StatsResample](/igorpro/commands/statsresample.md) |
| Jarque-Bera Test | [StatsJBTest](/igorpro/commands/statsjbtest.md) |
| Kolmogorov-Smirnov | [StatsKSTest](/igorpro/commands/statskstest.md) |
| Kruskal-Wallis | [StatsKWTest](/igorpro/commands/statskwtest.md) |
| Kuiper Test | [StatsCircularMoments](/igorpro/commands/statscircularmoments.md) |
| Levene's test for variances | [StatsVariancesTest](/igorpro/commands/statsvariancestest.md) |
| Linear Correlation Test | [StatsLinearCorrelationTest](/igorpro/commands/statslinearcorrelationtest.md) |
| Linear Order Statistic | [StatsCircularMoments](/igorpro/commands/statscircularmoments.md) |
| Mann-Kendall | [StatsKendallTauTest](/igorpro/commands/statskendalltautest.md) |
| Moore test | [StatsCircularTwoSampleTest](/igorpro/commands/statscirculartwosampletest.md), [StatsCircularMeans](/igorpro/commands/statscircularmeans.md) |
| Non-parametric multiple contrasts | [StatsNPMCTest](/igorpro/commands/statsnpmctest.md) |
| Non-parametric angular-angular correlation | [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md) |
| Non-parametric second order circular analysis | [StatsCircularMeans](/igorpro/commands/statscircularmeans.md) |
| Non-parametric serial randomness (nominal) | [StatsNPNominalSRTest](/igorpro/commands/statsnpnominalsrtest.md) |
| Parametric angular-angular correlation | [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md) |
| Parametric angular-Linear correlation | [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md) |
| Parametric second order circular analysis | [StatsCircularMeans](/igorpro/commands/statscircularmeans.md) |
| Parametric serial randomness test | [StatsSRTest](/igorpro/commands/statssrtest.md) |
| Rayleigh | [StatsCircularMoments](/igorpro/commands/statscircularmoments.md) |
| Repeated Measures | [StatsANOVA2RMTest](/igorpro/commands/statsanova2rmtest.md) |
| Scheffe equality of means | [StatsScheffeTest](/igorpro/commands/statsscheffetest.md) |
| Shapiro-Wilk test for normality | [StatsShapiroWilkTest](/igorpro/commands/statsshapirowilktest.md) |
| Spearman | [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md) |
| Student-Newman-Keuls | [StatsNPMCTest](/igorpro/commands/statsnpmctest.md) |
| Tukey Test | [StatsTukeyTest](/igorpro/commands/statstukeytest.md), [StatsLinearRegression](/igorpro/commands/statslinearregression.md), [StatsMultiCorrelationTest](/igorpro/commands/statsmulticorrelationtest.md), [StatsNPMCTest](/igorpro/commands/statsnpmctest.md) |
| Two-Factor ANOVA | [StatsANOVA2NRTest](/igorpro/commands/statsanova2nrtest.md) |
| T-test | [StatsTTest](/igorpro/commands/statsttest.md) |
| Watson's nonparametric two-sample U<sup>2</sup> | [StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md), [StatsCircularTwoSampleTest](/igorpro/commands/statscirculartwosampletest.md) |
| Watson-Williams | [StatsWatsonWilliamsTest](/igorpro/commands/statswatsonwilliamstest.md) |
| Weighted -rank correlation test | [StatsWRCorrelationTest](/igorpro/commands/statswrcorrelationtest.md) |
| Wheeler-Watson nonparametric test | [StatsWheelerWatsonTest](/igorpro/commands/statswheelerwatsontest.md) |
| Wilcoxon-Mann-Whitney two-sample | [StatsWilcoxonRankTest](/igorpro/commands/statswilcoxonranktest.md) |
| Wilcoxon signed rank | [StatsWilcoxonRankTest](/igorpro/commands/statswilcoxonranktest.md) |



### Statistical Test Operations by Data Format {#statistical-test-operations-by-data-format}

The following tables group statistical operations and functions according to the format of the input data.

### Tests For Single Waves {#tests-for-single-waves}


| Analysis Method | Comment |
| --- | --- |
| [StatsChiTest](/igorpro/commands/statschitest.md) | Compares with known binned values |
| [StatsCircularMoments](/igorpro/commands/statscircularmoments.md) | WaveStats for circular data |
| [StatsKendallTauTest](/igorpro/commands/statskendalltautest.md) | Similar to Spearman's correlation |
| [StatsMedian](/igorpro/commands/statsmedian.md) | Returns the median |
| [StatsNPNominalSRTest](/igorpro/commands/statsnpnominalsrtest.md) | Non-parametric serial randomness test |
| [StatsQuantiles](/igorpro/commands/statsquantiles.md) | Computes quantiles and more |
| [StatsResample](/igorpro/commands/statsresample.md) | Bootstrap analysis |
| [StatsSRTest](/igorpro/commands/statssrtest.md) | Serial randomness test |
| [StatsTrimmedMean](/igorpro/commands/statstrimmedmean.md) | Returns the trimmed mean |
| [StatsTTest](/igorpro/commands/statsttest.md) | Compares with known mean |
| [Sort](/igorpro/commands/sort.md) | Reorders the data |
| [WaveStats](/igorpro/commands/wavestats.md) | Basic statistical description |
| [StatsJBTest](/igorpro/commands/statsjbtest.md) | Jarque-Bera test for normality |
| [StatsKSTest](/igorpro/commands/statskstest.md) | Limited scope test for normality |
| [StatsDIPTest](/igorpro/commands/statsdiptest.md) | Hartigan test for unimodality |
| [StatsShapiroWilkTest](/igorpro/commands/statsshapirowilktest.md) | Shapiro-Wilk test for normality |



### Tests For Two Waves {#tests-for-two-waves}


| Analysis Method | Comment |
| --- | --- |
| [StatsChiTest](/igorpro/commands/statschitest.md) | Chi-squared statistic for comparing two distributions |
| [StatsCochranTest](/igorpro/commands/statscochrantest.md)<sub> </sub> | Randomized block or repeated measures test |
| [StatsCircularTwoSampleTest](/igorpro/commands/statscirculartwosampletest.md) | Second order analysis of angles |
| [StatsDunnettTest](/igorpro/commands/statsdunnetttest.md) | Compares multiple groups to a control |
| [StatsFTest](/igorpro/commands/statsftest.md) | Computes ratio of variances |
| [StatsFriedmanTest](/igorpro/commands/statsfriedmantest.md) | Non-parametric ANOVA |
| [StatsKendallTauTest](/igorpro/commands/statskendalltautest.md) | Similar to Spearman's correlation |
| [StatsTTest](/igorpro/commands/statsttest.md) | Compares the means of two distributions |
| [StatsANOVA1Test](/igorpro/commands/statsanova1test.md) | One-way analysis of variances |
| [StatsLinearRegression](/igorpro/commands/statslinearregression.md) | Linear regression analysis |
| [StatsLinearCorrelationTest](/igorpro/commands/statslinearcorrelationtest.md) | Linear correlation coefficient and its error |
| [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md) | Computes Spearman's rank correlation |
| [StatsVariancesTest](/igorpro/commands/statsvariancestest.md) | Compares variances of waves |
| [StatsWilcoxonRankTest](/igorpro/commands/statswilcoxonranktest.md) | Two-sample or signed rank test |
| [StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md) | Compares two populations of circular data |
| [StatsWatsonWilliamsTest](/igorpro/commands/statswatsonwilliamstest.md) | Compares mean values of angular distributions |
| [StatsWheelerWatsonTest](/igorpro/commands/statswheelerwatsontest.md) | Compares two angular distributions |



### Tests For Multiple or Multidimensional Waves {#tests-for-multiple-or-multidimensional-waves}


| Analysis Method | Comment |
| --- | --- |
| [StatsANOVA1Test](/igorpro/commands/statsanova1test.md) | One-way analysis of variances |
| [StatsANOVA2Test](/igorpro/commands/statsanova2test.md) | Two-factor analysis of variances |
| [StatsANOVA2RMTest](/igorpro/commands/statsanova2rmtest.md) | Two-factor repeated measure ANOVA |
| [StatsCochranTest](/igorpro/commands/statscochrantest.md) | Randomized block or repeated measures test |
| [StatsContingencyTable](/igorpro/commands/statscontingencytable.md) | Contingency table analysis |
| [StatsDunnettTest](/igorpro/commands/statsdunnetttest.md) | Compares multiple groups to a control |
| [StatsFriedmanTest](/igorpro/commands/statsfriedmantest.md) | Non-parametric ANOVA |
| [StatsNPMCTest](/igorpro/commands/statsnpmctest.md) | Non-parametric multiple comparison tests |
| [StatsScheffeTest](/igorpro/commands/statsscheffetest.md) | Tests equality of means |
| [StatsTukeyTest](/igorpro/commands/statstukeytest.md) | Multiple comparisons based on means |
| [StatsWatsonWilliamsTest](/igorpro/commands/statswatsonwilliamstest.md) | Compares mean values of angular distributions |
| [StatsWheelerWatsonTest](/igorpro/commands/statswheelerwatsontest.md) | Compares two angular distributions |



### Statistical Test Operations for Angular/Circular Data {#statistical-test-operations-for-angular-circular-data}


|  |
| --- |
| [StatsAngularDistanceTest](/igorpro/commands/statsangulardistancetest.md) |
| [StatsCircularMoments](/igorpro/commands/statscircularmoments.md) |
| [StatsCircularMeans](/igorpro/commands/statscircularmeans.md) |
| [StatsCircularTwoSampleTest](/igorpro/commands/statscirculartwosampletest.md) |
| [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md) |
| [StatsHodgesAjneTest](/igorpro/commands/statshodgesajnetest.md) |
| [StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md) |
| [StatsWatsonWilliamsTest](/igorpro/commands/statswatsonwilliamstest.md) |
| [StatsWheelerWatsonTest](/igorpro/commands/statswheelerwatsontest.md) |



### Statistical Test Operations: Non-Parametric Tests {#statistical-test-operations-non-parametric-tests}


|  |  |
| --- | --- |
| [StatsAngularDistanceTest](/igorpro/commands/statsangulardistancetest.md) |  |
| [StatsFriedmanTest](/igorpro/commands/statsfriedmantest.md) |  |
| [StatsCircularTwoSampleTest](/igorpro/commands/statscirculartwosampletest.md) | Parametric or nonparametric |
| [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md) | Parametric or nonparameteric |
| [StatsCircularMeans](/igorpro/commands/statscircularmeans.md) | Parametric or nonparameteric |
| [StatsHodgesAjneTest](/igorpro/commands/statshodgesajnetest.md) |  |
| [StatsKendallTauTest](/igorpro/commands/statskendalltautest.md) |  |
| [StatsKWTest](/igorpro/commands/statskwtest.md) |  |
| [StatsNPMCTest](/igorpro/commands/statsnpmctest.md) |  |
| [StatsNPNominalSRTest](/igorpro/commands/statsnpnominalsrtest.md) |  |
| [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md) |  |
| [StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md) |  |
| [StatsWheelerWatsonTest](/igorpro/commands/statswheelerwatsontest.md) |  |
| [StatsWilcoxonRankTest](/igorpro/commands/statswilcoxonranktest.md) |  |



## Noise Functions {#noise-functions}

The following functions return numbers from a pseudo-random distribution of the specified shapes and parameters. Except for [enoise](/igorpro/commands/enoise.md) and [gnoise](/igorpro/commands/gnoise.md) where you have an option to select a random number generator, the remaining noise functions use a Mersenne Twister algorithm for the initial uniform pseudo-random distribution. 

:::note
Whenever you need repeatable results you should use [SetRandomSeed](/igorpro/commands/setrandomseed.md) prior to executing any of the noise functions.
:::

The following noise generation functions are available:

|  |  |
| --- | --- |
| [binomialNoise](/igorpro/commands/binomialnoise.md) | [logNormalNoise](/igorpro/commands/lognormalnoise.md) |
| [enoise](/igorpro/commands/enoise.md) | [lorentzianNoise](/igorpro/commands/lorentziannoise.md) |
| [expNoise](/igorpro/commands/expnoise.md) | [poissonNoise](/igorpro/commands/poissonnoise.md) |
| [gammaNoise](/igorpro/commands/gammanoise.md) | [StatsPowerNoise](/igorpro/commands/statspowernoise.md) |
| [gnoise](/igorpro/commands/gnoise.md) | [StatsVonMisesNoise](/igorpro/commands/statsvonmisesnoise.md) |
| [HyperGNoise](/igorpro/commands/hypergnoise.md) | [wnoise](/igorpro/commands/wnoise.md) |

## Cumulative Distribution Functions {#cumulative-distribution-functions}

A Cumulative Distribution Function (CDF) is the integral of its respective probability distribution function (PDF). CDFs are usually well behaved functions with values in the range [0,1]. CDFs are important in computing critical values, P-values and power of statistical tests.

Many CDFs are computed directly from closed form expressions. Others can be difficult to compute because they involve evaluating a very large number of states, e.g., Friedman or USquared distributions. In these cases you have the following options:


1.	Use a built-in table that consists of exact, pre-computed values.


2.	Compute an approximate CDF based on the prevailing approximation method or using a Monte-Carlo approach.


3.	Compute the exact CDF.

Built-in tables are ideal if they cover the range of the parameters that you need. Monte-Carlo methods can be tricky in the sense that repeated application may return small variations in values. Computing the exact CDF may be desirable, but it is often impractical. In most situations the range of parameters that is practical to compute on a desktop machine is already covered in the built-in tables. Larger parameters have not been considered because they take days to compute or because they require 64 bit processors. In addition, most of the approximations tend to improve with increasing size of the parameters.

The functions to calculate values from CDFs are as follows:


|  |  |  |
| --- | --- | --- |
| [StatsBetaCDF](/igorpro/commands/statsbetacdf.md) | [StatsHyperGCDF](/igorpro/commands/statshypergcdf.md) | [StatsQCDF](/igorpro/commands/statsqcdf.md) |
| [StatsBinomialCDF](/igorpro/commands/statsbinomialcdf.md) | [StatsKuiperCDF](/igorpro/commands/statskuipercdf.md) | [StatsRayleighCDF](/igorpro/commands/statsrayleighcdf.md) |
| [StatsCauchyCDF](/igorpro/commands/statscauchycdf.md) | [StatsLogisticCDF](/igorpro/commands/statslogisticcdf.md) | [StatsRectangularCDF](/igorpro/commands/statsrectangularcdf.md) |
| [StatsChiCDF](/igorpro/commands/statschicdf.md) | [StatsLogNormalCDF](/igorpro/commands/statslognormalcdf.md) | [StatsRunsCDF](/igorpro/commands/statsrunscdf.md) |
| [StatsCMSSDCDF](/igorpro/commands/statscmssdcdf.md) | [StatsMaxwellCDF](/igorpro/commands/statsmaxwellcdf.md) | [StatsSpearmanRhoCDF](/igorpro/commands/statsspearmanrhocdf.md) |
| [StatsDExpCDF](/igorpro/commands/statsdexpcdf.md) | [StatsMooreCDF](/igorpro/commands/statsmoorecdf.md) | [StatsStudentCDF](/igorpro/commands/statsstudentcdf.md) |
| [StatsErlangCDF](/igorpro/commands/statserlangcdf.md) | [StatsNBinomialCDF](/igorpro/commands/statsnbinomialcdf.md) | [StatsTopDownCDF](/igorpro/commands/statstopdowncdf.md) |
| [StatsEValueCDF](/igorpro/commands/statsevaluecdf.md) | [StatsNCFCDF](/igorpro/commands/statsncfcdf.md) | [StatsTriangularCDF](/igorpro/commands/statstriangularcdf.md) |
| [StatsExpCDF](/igorpro/commands/statsexpcdf.md) | [StatsNCTCDF](/igorpro/commands/statsnctcdf.md) | [StatsUSquaredCDF](/igorpro/commands/statsusquaredcdf.md) |
| [StatsFCDF](/igorpro/commands/statsfcdf.md) | [StatsNormalCDF](/igorpro/commands/statsnormalcdf.md) | [StatsVonMisesCDF](/igorpro/commands/statsvonmisescdf.md) |
| [StatsFriedmanCDF](/igorpro/commands/statsfriedmancdf.md) | [StatsParetoCDF](/igorpro/commands/statsparetocdf.md) | [StatsQCDF](/igorpro/commands/statsqcdf.md) |
| [StatsGammaCDF](/igorpro/commands/statsgammacdf.md) | [StatsPoissonCDF](/igorpro/commands/statspoissoncdf.md) | [StatsWaldCDF](/igorpro/commands/statswaldcdf.md) |
| [StatsGeometricCDF](/igorpro/commands/statsgeometriccdf.md) | [StatsPowerCDF](/igorpro/commands/statspowercdf.md) | [StatsWeibullCDF](/igorpro/commands/statsweibullcdf.md) |



## Probablility Distribution Functions {#probablility-distribution-functions}

Probability distribution functions (PDF) are sometimes known as probability densities. In the case of continuous distributions, the area under the curve of the PDF for each interval equals the probability for the random variable to fall within that interval. The PDFs are useful in calculating event probabilities, characteristic functions and moments of a distribution.

The functions to calculate values from PDFs are as follows:


|  |  |  |
| --- | --- | --- |
| [StatsBetaPDF](/igorpro/commands/statsbetapdf.md) | [StatsGammaPDF](/igorpro/commands/statsgammapdf.md) | [StatsParetoPDF](/igorpro/commands/statsparetopdf.md) |
| [StatsBinomialPDF](/igorpro/commands/statsbinomialpdf.md) | [StatsGeometricPDF](/igorpro/commands/statsgeometricpdf.md) | [StatsPoissonPDF](/igorpro/commands/statspoissonpdf.md) |
| [StatsCauchyPDF](/igorpro/commands/statscauchypdf.md) | [StatsHyperGPDF](/igorpro/commands/statshypergpdf.md) | [StatsPowerPDF](/igorpro/commands/statspowerpdf.md) |
| [StatsChiPDF](/igorpro/commands/statschipdf.md) | [StatsLogNormalPDF](/igorpro/commands/statslognormalpdf.md) | [StatsRayleighPDF](/igorpro/commands/statsrayleighpdf.md) |
| [StatsDExpPDF](/igorpro/commands/statsdexppdf.md) | [StatsMaxwellPDF](/igorpro/commands/statsmaxwellpdf.md) | [StatsRectangularPDF](/igorpro/commands/statsrectangularpdf.md) |
| [StatsErlangPDF](/igorpro/commands/statserlangpdf.md) | [StatsNBinomialPDF](/igorpro/commands/statsnbinomialpdf.md) | [StatsStudentPDF](/igorpro/commands/statsstudentpdf.md) |
| [StatsErrorPDF](/igorpro/commands/statserrorpdf.md) | [StatsNCChiPDF](/igorpro/commands/statsncchipdf.md) | [StatsTriangularPDF](/igorpro/commands/statstriangularpdf.md) |
| [StatsEValuePDF](/igorpro/commands/statsevaluepdf.md) | [StatsNCFPDF](/igorpro/commands/statsncfpdf.md) | [StatsVonMisesPDF](/igorpro/commands/statsvonmisespdf.md) |
| [StatsExpPDF](/igorpro/commands/statsexppdf.md) | [StatsNCTPDF](/igorpro/commands/statsnctpdf.md) | [StatsWaldPDF](/igorpro/commands/statswaldpdf.md) |
| [StatsFPDF](/igorpro/commands/statsfpdf.md) | [StatsNormalPDF](/igorpro/commands/statsnormalpdf.md) | [StatsWeibullPDF](/igorpro/commands/statsweibullpdf.md) |



## Inverse Cumulative Distribution Functions {#inverse-cumulative-distribution-functions}

The inverse cumulative distribution functions return the values at which their respective CDFs attain a given level. This value is typically used as a critical test value. There are very few functions for which the inverse CDF can be written in closed form. In most situations the inverse is computed iteratively from the CDF.

The functions to calculate values from inverse CDFs are as follows:


|  |  |  |
| --- | --- | --- |
| [StatsInvBetaCDF](/igorpro/commands/statsinvbetacdf.md) | [StatsInvKuiperCDF](/igorpro/commands/statsinvkuipercdf.md) | [StatsInvQpCDF](/igorpro/commands/statsinvqpcdf.md) |
| [StatsInvBinomialCDF](/igorpro/commands/statsinvbinomialcdf.md) | [StatsInvLogisticCDF](/igorpro/commands/statsinvlogisticcdf.md) | [StatsInvRayleighCDF](/igorpro/commands/statsinvrayleighcdf.md) |
| [StatsInvCauchyCDF](/igorpro/commands/statsinvcauchycdf.md) | [StatsInvLogNormalCDF](/igorpro/commands/statsinvlognormalcdf.md) | [StatsInvRectangularCDF](/igorpro/commands/statsinvrectangularcdf.md) |
| [StatsInvChiCDF](/igorpro/commands/statsinvchicdf.md) | [StatsInvMaxwellCDF](/igorpro/commands/statsinvmaxwellcdf.md) | [StatsInvSpearmanCDF](/igorpro/commands/statsinvspearmancdf.md) |
| [StatsInvCMSSDCDF](/igorpro/commands/statsinvcmssdcdf.md) | [StatsInvMooreCDF](/igorpro/commands/statsinvmoorecdf.md) | [StatsInvStudentCDF](/igorpro/commands/statsinvstudentcdf.md) |
| [StatsInvDExpCDF](/igorpro/commands/statsinvdexpcdf.md) | [StatsInvNBinomialCDF](/igorpro/commands/statsinvnbinomialcdf.md) | [StatsInvTopDownCDF](/igorpro/commands/statsinvtopdowncdf.md) |
| [StatsInvEValueCDF](/igorpro/commands/statsinvevaluecdf.md) | [StatsInvNCFCDF](/igorpro/commands/statsinvncfcdf.md) | [StatsInvTriangularCDF](/igorpro/commands/statsinvtriangularcdf.md) |
| [StatsInvExpCDF](/igorpro/commands/statsinvexpcdf.md) | [StatsInvNormalCDF](/igorpro/commands/statsinvnormalcdf.md) | [StatsInvUSquaredCDF](/igorpro/commands/statsinvusquaredcdf.md) |
| [StatsInvFCDF](/igorpro/commands/statsinvfcdf.md) | [StatsInvParetoCDF](/igorpro/commands/statsinvparetocdf.md) | [StatsInvVonMisesCDF](/igorpro/commands/statsinvvonmisescdf.md) |
| [StatsInvFriedmanCDF](/igorpro/commands/statsinvfriedmancdf.md) | [StatsInvPoissonCDF](/igorpro/commands/statsinvpoissoncdf.md) | [StatsInvWeibullCDF](/igorpro/commands/statsinvweibullcdf.md) |
| [StatsInvGammaCDF](/igorpro/commands/statsinvgammacdf.md) | [StatsInvPowerCDF](/igorpro/commands/statsinvpowercdf.md) |  |
| [StatsInvGeometricCDF](/igorpro/commands/statsinvgeometriccdf.md) | [StatsInvQCDF](/igorpro/commands/statsinvqcdf.md) |  |



## General Purpose Statistics Operations and Functions {#general-purpose-statistics-operations-and-functions}

This group includes operations and functions that existed before IGOR Pro 6.0 and some general purpose operations and functions that do not belong to the main groups listed above.


|  |  |  |
| --- | --- | --- |
| [binomial](/igorpro/commands/binomial.md) | [Sort](/igorpro/commands/sort.md) | [StatsTrimmedMean](/igorpro/commands/statstrimmedmean.md) |
| [binomialln](/igorpro/commands/binomialln.md) | [StatsCircularMoments](/igorpro/commands/statscircularmoments.md) | [StudentA](/igorpro/commands/studenta.md) |
| [erf](/igorpro/commands/erf.md) | [StatsCorrelation](/igorpro/commands/statscorrelation.md) | [StudentT](/igorpro/commands/studentt.md) |
| [erfc](/igorpro/commands/erfc.md) | [StatsMedian](/igorpro/commands/statsmedian.md) | [WaveStats](/igorpro/commands/wavestats.md) |
| [inverseERF](/igorpro/commands/inverseerf.md) | [StatsQuantiles](/igorpro/commands/statsquantiles.md) | [StatsPermute](/igorpro/commands/statspermute.md) |
| [inverseERFC](/igorpro/commands/inverseerfc.md) | [StatsResample](/igorpro/commands/statsresample.md) |  |



## Hazard and Survival Functions {#hazard-and-survival-functions}

Igor does not provide built-in functions to calculate the Survival or Hazard functions. They can be calculated easily from the Probability Density Functions and Cumulative Density Functions provided by Igor.

In the following, the [Cumulative Distribution Functions](#cumulative-distribution-functions) are denoted by F(x) and the [Probablility Distribution Functions](#probablility-distribution-functions) are denoted by p(x).

The Survival Function S(x) is given by

$$
\displaystyle S(x)=1-F(x) .
$$

The Hazard function h(x) is given by

$$
\displaystyle h(x)=\frac{p(x)}{S(x)}=\frac{p(x)}{1-F(x)} .
$$

The cumulative hazard function H(x)

$$
\displaystyle H(x)=\int_{-\infty}^{x} h(u) d u,
$$

$$
\displaystyle H(x)=-\ln [1-F(x)] .
$$

Inverse Survival Function Z(α)

$$
\displaystyle Z(\alpha)=G(1-\alpha),
$$

where G() is the inverse CDF (see [Inverse Cumulative Distribution Functions](#inverse-cumulative-distribution-functions)).



## Statistics Procedures {#statistics-procedures}

Several procedure files are provided to extend the built-in statistics capability described in this help file. Some of these procedure files provide control-panel user interfaces to the built-in statistics funtionality. Others extend the functionality.

In the Analysis menu you will find a Statistics item that brings up a submenu. Selecting any item in the submenu will cause all the statistics-related procedure files to be loaded, making them ready to use. Alternativelly, you can load all the statistics procedures by adding the following include statement to the top of your procedure window:


```igor
#include <AllStatsProcedures>
```

Functionality provided by the statistics procedure files includes the 1D Statistics Report package for automatic analysis of single 1D waves, and the [ANOVA Power Calculations Panel](IgorAction:Execute/P__"INSERTINCLUDE__\<ANOVA1PowerCalc\>"\<semicolon\>Execute/P__"COMPILEPROCEDURES__"\<semicolon\>Execute/P__"WM_SetupANOVAPowerPanel()"), as well as functions to create specialized graphs:

|  |  |
| --- | --- |
| StatsAutoCorrPlot() | StatsPlotLag() |
| StatsBoxPlot() | StatsProbPlot() |
| StatsPlotHistogram() |  |

Also included are these of convenience functions:

|  |  |
| --- | --- |
| WM_2MeanConfidenceIntervals() | WM_MCPointOnRegressionLines() |
| WM_2MeanConfidenceIntervals2() | WM_MeanConfidenceInterval() |
| WM_BernoulliCdf() | WM_OneTailStudentA() |
| WM_BinomialPdf() | WM_OneTailStudentT() |
| WM_CIforPooledMean() | WM_PlotBiHistogram() |
| WM_CompareCorrelations() | WM_RankForTies() |
| WM_EstimateMinDetectableDiff() | WM_RankLetterGradesWithTies() |
| WM_EstimateReqSampleSize() | WM_RegressionInversePrediction() |
| WM_EstimateReqSampleSize2() | WM_SSEstimatorFunc() |
| WM_EstimateSampleSizeForDif() | WM_SSEstimatorFunc2() |
| WM_GetANOVA1Power() | WM_SSEstimatorFunc3() |
| WM_GetGeometricAverage() | WM_VarianceConfidenceInterval() |
| WM_GetHarmonicMean() | WM_WilcoxonPairedRanks() |
| WM_GetPooledMean() | WM_StatsKaplanMeier() |
| WM_GetPooledVariance() |  |


## Statistics References {#statistics-references}

Ajne, B., A simple test for uniformity of a circular distribution, *Biometrica*, *55*, 343-354, 1968.

Bradley, J.V., *Distribution-Free Statistical Tests*, Prentice Hall, Englewood Cliffs, New Jersey, 1968.

Cheung, Y.K., and J.H. Klotz, The Mann Whitney Wilcoxon distribution using linked lists, *Statistica Sinica*, *7*, 805-813, 1997.

Copenhaver, M.D., and B.S. Holland, Multiple comparisons of simple effects in the two-way analysis of variance with fixed effects, *Journal of Statistical Computation and Simulation*, *30*, 1-15, 1988.

Evans, M., N. Hastings, and B. Peacock, *Statistical Distributions*, 3rd ed., Wiley, New York, 2000.

Fisher, N.I., *Statistical Analysis of Circular Data*, 295pp., Cambridge University Press, New York, 1995.

Iman, R.L., and W.J. Conover, A measure of top-down correlation, *Technometrics*, *29*, 351-357, 1987.

Kendall, M.G., *Rank Correlation Methods*, 3rd ed., Griffin, London, 1962.

Klotz, J.H., *Computational Approach to Statistics*.

Moore, B.R., A modification of the Rayleigh test for vector data, *Biometrica*, *67*, 175-180, 1980.

Press, William H., et al., *Numerical Recipes in C*, 2nd ed., 994 pp., Cambridge University Press, New York, 1992.

van de Wiel, M.A., and A. Di Bucchianico, Fast computation of the exact null distribution of Spearman's rho and Page's L statistic for samples with and without ties, *J. of Stat. Plan. and Inferenc*e, *92*, 133-145, 2001..

Wallace, D.L., Simplified Beta-Approximation to the Kruskal-Wallis H Test, *Jour. Am. Stat. Assoc.*, *54*, 225-230.

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.