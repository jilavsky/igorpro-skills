---
description: "The HCluster operation computes the information needed to create a cluster dendrogram using an agglomerative hierarchical clustering algorithm."
slug: /commands/hcluster
---

<div className="command-signature">

## <strong>HCluster</strong>  [ /ITYP=<em>it</em> /OTYP=<em>ot</em> /LINK=<em>nm</em> /DISS=<em>dm</em> /P=<em>pow</em> /VARW=<em>varWave</em> /DEST={<em>dMatrixName</em>, <em>dendrodrogramName</em>} /O ] <em>sourceWave</em> {#hcluster}

</div>

The HCluster operation computes the information needed to create a cluster dendrogram using an agglomerative hierarchical clustering algorithm. "HCluster" stands for "hierarchical clustering". The HCluster operation was added in Igor Pro 9.00.

For background information, see [Hierarchical Clustering](/igorpro/analysis/analysis.md#hierarchical-clustering).

The input *sourceWave* represents either vectors in some data space or a square vector dissimilarity matrix (also called a "distance" matrix). You indicate which type of input you are providing using the /ITYP flag.

HCluster creates an output vector dissimilarity matrix wave or an output dendrogram wave or both, depending on the /OTYP flag. The output wave names default to M_HCluster_Dissimilarity and M_HCluster_Dendrogram but you can override the default using /DEST.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ITYP = *it*</span> | *it* is a keyword specifying the kind of data in *sourceWave*: |
|  |<table class="nested-table"><tbody><tr><td>*it*=Vectors:</td><td>*sourceWave* rows represent data vectors (default).</td></tr><tr><td>*it*=DMatrix:</td><td>*sourceWave* contains a square vector dissimilarity matrix.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/OTYP = *ot*</span> | *ot* is a keyword specifying what type of output to be produced: |
|  |<table class="nested-table"><tbody><tr><td>*ot*=DMatrix:</td><td>The output is a vector dissimilarity matrix. You can use /OTYP=DMatrix only if /ITYP=Vectors or if you omit /ITYP.</td></tr><tr><td>*ot*=Dendrogram:</td><td>The output is a multi-column wave describing the nodes in a dendrogram illustrating the way original data is joined into clusters. This is the default if you omit /OTYP.</td></tr><tr><td>*ot*=*Both*:</td><td>The output is both the vector dissimilarity matrix and a dendrogram.</td></tr></tbody></table>
|  | See the /DEST flag for further discussion of the output wave or waves. |
| <span class="table-cell-nowrap">/LINK = *linkMethod*</span> |  |
|  | *linkMethod* is a keyword specifying the method used to determine the dissimilarity between nodes in the dendrogram that represent more than one data vector. This is also referred to as the "linkage" method. Our definitions of node dissimilarities follows Python `scipy.cluster.hierarchy.linkage`. |
|  | The available keywordds for *linkMethod* are listed and described under [HCluster Linkage Calculation Methods](/igorpro/analysis/analysis.md#hcluster-linkage-calculation-methods). |
|  | If you omit /LINK, HCluster defaults to the average method. |
| <span class="table-cell-nowrap">/DISS = *dm*</span> | *dm* is a keyword specifying the vector dissimilarity metric for calculating the dissimilarity between two data vectors. Our definitions of vector dissimilarity follows Python `scipy.spatial.distance.pdist`. |
|  | The available /DISS keywords are listed and described under [HCluster Vector Dissimilarity Calculation Methods](/igorpro/analysis/analysis.md#hcluster-vector-dissimilarity-calculation-methods). |
|  | If you omit /DISS, HCluster defaults to the Euclidean metric. |
| <span class="table-cell-nowrap">/P = *pow*</span> | *pow* is the power for the *Minkowski* vector dissimilarity metric. The value of *pow* must be positive. The default is 2.0, equivalent to the *Euclidean* vector dissimilarity metric. Values that are too large can lead to floating-point overflow. Values less than 1.0 may give surprising results, as this can cause an inversion of the usual distance ordering. If the vector dissimilarity metric is not *Minkowski* this flag is ignored. |
| <span class="table-cell-nowrap">/VARW = *varWave*</span> |  |
|  | Specifies the normalizing values V<sub>j</sub> for use with the *SEuclidean* vector dissimilarity metric. Usually, the wave elements are variances of the vector elements over all the vectors. Thus, if you have a multi-column wave in which rows represent individual vectors, *varWave* should be filled with variances of the wave's columns. If your vectors have length of *M*, then *varWave* should be a 1D wave with *M* elements. This wave can be conveniently created using the [MatrixOP](/igorpro/commands/matrixop.md) operation, like this: |
|  | <code class="igor">MatrixOp/O varWave = VarCols(rowVectorMatrix)^t</code> |
|  | If the vector dissimilarity matrix is not SEuclidean, the /VARW flag is ignored. |
| <span class="table-cell-nowrap">/DEST = *outWaveName*</span> |  |
|  | Specifies the output waves when you have specified /OTYP=DMatrix or /OTYP=Dendrogram. |
|  | If you specified /OTYP=DMatrix, *outWaveName* is the name of the output vector dissimilarity matrix wave to be created or overwritten, optionally preceded by a data folder path. If you omit /DEST, HCluster creates an output vector dissimilarity matrix named M_HCluster_Dissimilarity in the current data folder. |
|  | If you specified /OTYP=Dendrogram, *outWaveName* is the name of the output dendrogram wave to be created or overwritten, optionally preceded by a data folder path. If you omit /DEST, HCluster creates an output dendrogram named M_HCluster_Dendrogram in the current data folder. |
| <span class="table-cell-nowrap">/DEST = {*dMatrixName*, *dendrodrogramName*}</span> |  |
|  | Specifies the output waves when you have specified /OTYP=*Both*. |
|  | *dMatrixName* and *dendrodrogramName* are names of waves to be created or overwritten, optionally preceded by data folder paths. |
|  | If you specify /OTYP=*Both* and omit /DEST, HCluster creates an output vector dissimilarity matrix named M_HCluster_Dissimilarity and an output dendrogram wave named M_HCluster_Dendrogram, both in the current data folder. |
| <span class="table-cell-nowrap">/O</span> | If present, allows the destination waves specified by the /DEST flag to overwrite a pre-existing wave. |

### *Parameter* {#parameter}
If you specify /ITYP=Vectors or omit /ITYP, *sourceWave* is an N row x M column matrix containing N data vectors of length M in the rows. HCluster creates a vector dissimilarity matrix from this input using the distance calculation method specified by /LINK.

If you specify /ITYP=DMatrix, *sourceWave* is a square matrix of dissimilarities between data vectors. If you choose this format, you are responsible for computing the dissimilarities between vectors. If none of the vector dissimilarity metrics provided by the /DISS flag are suitable, or if you require more processing after computing dissimilarities, you can use this format.

### *Dendrogram Output Wave* {#dendrogram-output-wave}
The HCluster operation optionally produces a dendrogram output wave that can be used to create a dendrogram plot. See [Dendrogram Wave Format](/igorpro/analysis/analysis.md#dendrogram-wave-format) for a description of the dendrogram output wave format.

### *Reference* {#reference}
The HCluster operation is based on code developed by Daniel Müllner. This reference gives details of the algorithm and the various distance and vector dissimilarity measures and node agglomeration methods:

Daniel Müllner, fastcluster: Fast Hierarchical, Agglomerative Clustering Routines for R and Python, Journal of Statistical Software, 53 (2013), no. 9, 1–18, http://www.jstatsoft.org/v53/i09/.

### *See Also* {#see-also}
[Hierarchical Clustering](/igorpro/analysis/analysis.md#hierarchical-clustering)