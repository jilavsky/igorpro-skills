---
description: "ImageUnwrapPhase unwraps a 2D phase in srcPhaseWave and stores the result in the specified destination wave or in the wave M_UnwrappedPhase in the current…"
slug: /commands/imageunwrapphase
---

<div className="command-signature">

## <strong>ImageUnwrapPhase</strong>   [/Q] [/E] [/M=<em>method</em> ] [/L] [/R=<em>RoiWave</em> ] [/MAX=<em>len</em> ] [<em>qualityWave</em>=<em>qWave</em>,] <em>srcWave</em>=<em>srcPhaseWave</em> {#imageunwrapphase}

</div>

ImageUnwrapPhase unwraps a 2D phase in *srcPhaseWave* and stores the result in the specified destination wave or in the wave M_UnwrappedPhase in the current data folder. *srcPhaseWave* must be a 2D real-valued wave of single or double precision. The phase is measured in cycles (units of 2*Pi).

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">qualityWave = *qWave*</span> |  |
|  | Specifies the wave containing numbers that rate the quality of the phase stored in the pixels. *qWave* is 2D wave of the same dimensions as srcWave that can be any real data type and values can have an arbitrary scale.  If used with /M=1 the quality values determine the order of phase unwrapping subject to branch cuts, with higher quality unwrapped first. If used with /M=2 the unwrapping is guided by the quality values only. This wave must not contain any NaNs or INFs. |
| <span class="table-cell-nowrap">srcwave = *phaseWave*</span> |  |
|  | Specifies a 2D real-valued SP or DP wave which may contain NaNs or INFs but is otherwise assumed to contain the phase modulo 1. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destP*</span> | Use this flag to specify the destination wave for the unwrapped phase data. If this flag is not specified, the operation saves the output in the wave in the wave M_UnwrappedPhase in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTL = *destL*</span> | Use this flag to specify the destination wave for the lookup table  If this flag is not specified, the operation saves the lookup table in the wave M_PhaseLUT in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/E</span> | Eliminate dipoles. Only applies to Goldstein's method (/M=1). Dipoles are a pair of a positive and negative residues that are side by side. They are eliminated from the unwrapping process by replacing them with a branch cut. The variable V_numResidues contains the number of residues remaining after removal of the dipoles. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination waves as a free waves.  This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/L</span> | Saves the lookup table(LUT) used in the analysis with /M=1. This information may be useful in analyzing your results. The LUT is saved as a 2D unsigned byte wave M_PhaseLUT in the current data folder. Each entry consists of 8-bit fields: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>Positive residue.</td></tr><tr><td>bit&nbsp;1:</td><td>Negative residue.</td></tr><tr><td>bit&nbsp;2:</td><td>Branch cut.</td></tr><tr><td>bit&nbsp;3:</td><td>Image boundary exclusion.</td></tr></tbody></table>
|  | Other bits are reserved and subject to change. |
| <span class="table-cell-nowrap">/M = *method*</span> | Determines the method for computing the unwrapped phase: |
|  |<table class="nested-table"><tbody><tr><td>*method*=0:</td><td>Modified Itoh&#39;s algorithm. The method stipulates that there are no residues in the phase. The phase is unwrapped in a contiguous way subject only to the ROI or singularities in the data (e.g., NaNs or INFs). You will get wrong results for the unwrapped phase if you use this method and your data contains residues.</td></tr><tr><td>*method*=1:</td><td>Modified Goldstein&#39;s algorithm. Creates the variables V_numResidues and V_numRegions. Optional *qWave* can determine the order of unwrapping around the branch cuts.</td></tr><tr><td>*method*=2:</td><td>Uses a quality map to decide the unwrapping path priority. The quality map is a 2D wave that has the same dimensions as the source wave, but could have an arbitrary data type. The phase is unwrapped starting from the largest value in the quality map.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/MAX = *len*</span> | Specifies the maximum length of a branch cut. Only applicable to Goldstein's method (/M=1). By default this is set to the largest of rows or columns. |
| <span class="table-cell-nowrap">/Q</span> | Suppresses messages to the history. |
| <span class="table-cell-nowrap">/R = *roiWave*</span> | Specifies a region of interest (ROI). The ROI is defined by a wave of type unsigned byte (/B/U) that has the same number of rows and columns as *srcPhaseWave*. The ROI itself is defined by entries in the *roiWave* with value of 1. Pixels outside the ROI should be set to zero. The ROI does not have to be contiguous, but it is best if you choose a convex ROI in order to make sure that any branch cuts computed by the algorithm lie completely inside the ROI domain. |
| <span class="table-cell-nowrap">/REST = *threshold*</span> |  |
|  | Sets the threshold value for evaluating a residue. The residue is evaluated by the equivalent of a closed path integral. If the path integral value exceeds the threshold value, the top-left corner of the quad is taken to be a positive residue. If the path integral is less than -*threshold*, it is a negative residue. The default value of the residue threshold is 0.01. |

### *Details* {#details}
Phase unwrapping in two dimensions is difficult because the result of the operation needs to be such that any path integral over a closed contour will vanish. In many practical situations, certain points in the plane have the property that a path integral around them is not zero. These nonzero points are residues. We use the definition that when a counterclockwise path integral leads to a positive value, the residue is called a positive residue.

ImageUnwrapPhase uses the modified Itoh's method by default. Phase is unwrapped with an offset equal to the first element that is allowed by the ROI starting at (0,0) and scanning by rows. If there are no residues or if you unwrap the phase using Itoh's algorithm, then the phase is unwrapped only subject to the optional ROI using a seed-fill type algorithm that unwraps by growing a region outward from the seed pixel. Each time that the region growing is terminated by boundaries (external or due to the ROI), the algorithm returns to the row scanning to find a new starting point.

If there are residues and you choose Goldstein's method, the residues are first mapped into a lookup table (LUT) and branch-cuts are determined between residues and boundaries. It is also possible to remove some residues (dipoles) using the /E flag. Phase is then unwrapped in regions bounded by branch cuts using a seed-fill type algorithm that does not cross branch cuts. With a quality wave, the algorithm follows the same seed-fill approach except that it gives priority to pixels with high quality level. The phase on the branch cuts themselves is subsequently calculated.

The output wave M_UnwrappedPhase has the same wave scaling and dimension units as srcWave. The unwrapped phase is units of cycles; you will have to multiply it by 2Pi if you need the results in radians.

The operation creates two variables:


|  |  |
| --- | --- |
| V_numResidues | Number of residues encountered (if using /M=1). |
| V_numRegions | Number of independent phase regions. In Goldstein's method the regions are bounded by branch cuts. In Itoh's method they depend on the content of the ROI wave. |

### *Examples* {#examples}

```igor
// Unwrap the phase of a complex wave wCmplx
MatrixOP/O phaseWave=atan2(imag(wCmplx),real(wCmplx))/(2*pi)
ImageUnwrapPhase/M=1 srcWave=phaseWave
// Find the locations of positive residues in the phase
ImageUnwrapPhase/M=1/L srcWave=phaseWave
MatrixOP/O ee=greater(bitAnd(M_PhaseLUT,2),0)
// Find the branch cuts
MatrixOP/O bc=greater(bitAnd(M_PhaseLUT,8),0)
```

### *See Also* {#see-also}
[Unwrap](/igorpro/commands/unwrap.md), [mod](/igorpro/commands/mod.md)

### *Demos* {#demos}
[Open Image Unwrap Phase Demo](#igor-pxp/Examples/Analysis/ImageUnwrapPhase__Demo.pxp)

### *References* {#references}
The reference below is an excellent text containing in-depth theory and detailed explanation of many two-dimensional phase unwrapping algorithms.

Ghiglia, Dennis C., and Mark D. Pritt, *Two Dimensional Phase Unwrapping - Theory, Algorithms and Software*, Wiley 1998.