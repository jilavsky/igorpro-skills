---
description: "The FPClustering operation performs cluster analysis using the farthest-point clustering algorithm."
slug: /commands/fpclustering
---

<div className="command-signature">

## <strong>FPClustering</strong>  [/NOR][/SHUB=<em>startHub</em>][/MAXR=<em>maxRad</em>] [/Q/Z] <em>srcWave</em> {#fpclustering}

</div>

The FPClustering operation performs cluster analysis using the farthest-point clustering algorithm. The input for the operation *srcWave*  defines M points in N-dimensional space. Outputs are the waves W_FPCenterIndex and W_FPClusterIndex.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CAC</span> | Computes all the clusters specified by /MAXC. |
| <span class="table-cell-nowrap">/CM</span> | Computes the center of mass for each cluster. The results are in the wave M_clustersCM in the current data folder or in *clusterCMDestWave* (if specified). Each row corresponds to a single cluster with columns providing the respective dimensional components. |
| <span class="table-cell-nowrap">/DSCI = *clusterIndexDest*</span> |  |
|  | Specify the destination wave containing the cluster index. If not specified via this flag the cluster index is save by default in the wave W_FPClusterIndex in the current data folder. |
| <span class="table-cell-nowrap">/DSCN = *clusterCenterDest*</span> |  |
|  | Specify the destination wave containing the index of the centers of clusters.  If not specified via this flag, the indices of the cluster centers are saved in the wave W_FPCenterIndex. |
| <span class="table-cell-nowrap">/DSO</span> | Returns the distance map of *srcWave* in M_DistanceMap or in *distanceMapWave* (if specified). No other output is generated and all other flags are ignored. |
|  | /DSO was added in Igor Pro 8.00. |
|  | The distance map is the Cartesian distance between any two rows in *srcWave*. The results are stored in the upper triangle of the double-precision output wave M_DistanceMap. The lower triangle is set to zero (results can be obtained by symmetry). |
|  | Each element of the upper triangle is given by: |
|  | $$ \displaystyle {M\_DistanceMap }_{r c}=\sqrt{\sum_{i=0}^{nCols-1}({srcWave}[r][i]-{srcWave}[c][i])^{2}} $$ |
| <span class="table-cell-nowrap">/FREE</span> | Creates all specified destination waves free waves. |
|  | /FREE is allowed only in functions and only if *destWave* and *destSWave*, as specified by /DEST and /DSTS, are simple names or wave references structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/INCD</span> | Computes the inter-cluster distances. The result is stored in the wave M_InterClusterDistance in the current data folder or in *icdDestWave* (if specified. M_InterClusterDistance is a 2D wave in which the [i][j] element contains the distance between cluster i and cluster j. |
| <span class="table-cell-nowrap">/MAXC = *nClusters*</span> |  |
|  | Terminates the calculation when the number of clusters reaches the specified value. Note that this termination condition is sufficient but not necessary, i.e., the operation can terminate earlier if the farthest distance of an element from a hub is less than the average distance. |
| <span class="table-cell-nowrap">/MAXR = *maxRad*</span> | Terminates the calculation when the maximum distance is less than or equal to *maxRad*. |
| <span class="table-cell-nowrap">/NOR</span> | Normalizes the data on a column by column basis. The normalization makes each columns of the input span the range [0,1] so that even when *srcWave*  contains columns that may be different by several orders of magnitude, the algorithm is not biased by a larger implied cartesian distance. |
| <span class="table-cell-nowrap">/Q</span> | Don't print information to the history area. |
| <span class="table-cell-nowrap">/SHUB = *sHub*</span> | Specifies the row which is used as a starting hub number. By default the operation uses the first row in *srcWave*. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The input for FPClustering is a 2D wave *srcWave* which consists of M rows by N columns where each row represents a point in N-dimensional space. *srcWave*  can contain only finite real numbers and must be of type SP or DP. The operation computes the clustering and produces the wave W_FPCenterIndex which contains the centers or "hubs" of the clusters. The hubs are specified by the (zero based) row number in *srcWave* which contains the cluster center. In addition, the operation creates the wave W_FPClusterIndex where each entry maps the corresponding input point to a cluster index. By default, the operation continues to add clusters as long as the largest possible distance is greater than the average intercluster distance. You can also stop the processing when the operation has formed a specified number of clusters (see /MAXC).

The variable V_max contains the maximum distance between any element and its cluster hub.

It is possible that in some circumstances you can get slightly different clustering depending on your starting point. The default starting hub is row zero of *srcWave* but you can use the /SHUB flag to specify a different starting point.

FPClustering computes the Cartesian distance between points. As a result, if the scale of any dimension is significantly larger than other dimensions it might bias the clustering towards that dimension. To avoid this situation you can use the /NOR flag which normalizes each column to the range [0,1] and hence equalizes the weight of each dimension in the clustering process.

It is an error to specify *srcWave* as both the source and a destination wave. It is also an error to specify the same destination wave for more than one destination.

When used in a function, the FPClustering operation creates real wave references for all the destination waves. Default output waves (fixed names) still require wave references. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details.

### *References* {#references}
Gonzalez, T., Clustering to minimize the maximum intercluster distance, *Theoretical Computer Science*, *38*, 293-306, 1985.

### *See Also* {#see-also}
[KMeans](/igorpro/commands/kmeans.md)

### *Demos* {#demos}
[Open Clustering Demo](#igor-pxp/Examples/Analysis/Clustering.pxp)