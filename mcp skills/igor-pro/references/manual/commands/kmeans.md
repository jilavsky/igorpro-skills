---
description: "KMeans analyzes the clustering of data in populationWave using an iterative algorithm."
slug: /commands/kmeans
---

<div className="command-signature">

## <strong>KMeans</strong>  [/CAN /DEAD=<em>method</em>  /DIST=<em>mode</em>  /INIT=<em>method</em>  /INW=<em>iWave</em> /NCLS=<em>num</em>  /OUT=<em>format</em>  /SEED=<em>val</em>  /TER=<em>method</em>  /TERN=<em>num</em> /Z] <em>populationWave</em> {#kmeans}

</div>

KMeans analyzes the clustering of data in *populationWave* using an iterative algorithm. The result of KMeans is a listing of classes that is saved by default in the wave M_KMClasses in the current data folder. Optional results include the distribution of class members (W_KMMembers), the inter-class distances (M_KMCDistances) and class dispersion (W_KMDispersion). *populationWave* is a 2D wave in which columns correspond to members of the population and rows contain dimensional information.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CAN</span> | Analyzes the clustering by computing distances between the means of the resulting classes. The distances are stored in the wave M_KMCDistances in the current data folder or in the wave specified by /DSTS.  The wave contains an NxN square matrix where N is the number of classes. Self distances (along the diagonal) or distances involving classes that did not survive the iterations are filled with NaN. The operation also saves the wave W_KMDispersion, which contains the sum of the distances between the center of each class and all its members. Distances are evaluated using the method specified by /DIST. |
| <span class="table-cell-nowrap">/DEAD = *method*</span> | Specifies how the algorithm should handle "dead" classes, i.e., classes that lose all members during a given iteration. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=1:</td><td>Remove the class if it loses all members.</td></tr><tr><td>*method*&nbsp;=2:</td><td>Keep the last value of the mean vector in case the class might get new members in a subsequent iteration. This is the default method.</td></tr><tr><td>*method*&nbsp;=3:</td><td>Assign the class a random mean vector.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/DIST = *mode*</span> | Specifies how the class distances are evaluated. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=1:</td><td>Distance is evaluated as the sum of the absolute values (also known as Manhattan distance).</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Distance is evaluated as Euclidian distance. This is the default distance mode.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/DSTC = *dstCWave*</span> |  |
|  | Specifies the output classes information wave. If you do not use this flag, the output is saved in the wave M_KMClasses in the current data folder. |
|  | It is an error to specify the same wave as both destination and source wave. |
|  | When used in a function, the operation creates a real wave reference for the *dstCWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTD = *dstDWave*</span> |  |
|  | Specifies the output dispersion wave. If you do not use this flag, the operation saves the dispersion data in the wave W_KMDispersion in the current data folder. See /CAN above for more details. |
|  | It is an error to specify the same wave as both destination and source wave. |
|  | When used in a function, the operation creates a real wave reference for the *dstDWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTM = *dstMWave*</span> |  |
|  | Specifies the output classes membership wave. If you do not use this flag, the operation saves this information in the wave W_KMMembers in the current data folder. See /OUT=2 below for more information. |
|  | It is an error to specify the same wave as both destination and source wave. |
|  | When used in a function, the operation creates a real wave reference for the *dstMWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTS = *dstSWave*</span> |  |
|  | Specifies the wave containing the distance matrix described in /CAN above (which is saved by default as M_KMCDistances in the current data folder). |
|  | It is an error to specify the same wave as both destination and source wave. |
|  | When used in a function, the operation creates a real wave reference for the *dstSWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all the specified destination waves as free waves. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/INIT = *method*</span> | Specifies the initialization method. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=1:</td><td>Random assignment of members of the population to a class</td></tr><tr><td>*method*&nbsp;=2:</td><td>User specified mean values (/INW).</td></tr><tr><td>*method*&nbsp;=3:</td><td>Initialize classes using values of a random selection from the population. This is the default initialization method.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/INW = *iWave*</span> | Specifies the initial classes. The number of rows of *iWave* equals the dimensionality of the class, and the number of columns of *iWave* is the number of classes. For example, if we want to initialize 5 classes in a problem that involves position in two dimensions, then *iWave* must have 2 rows and 5 columns. The number of rows must also match the number of rows in *populationWave*. |
| <span class="table-cell-nowrap">/NCLS = *num*</span> | Sets the number of classes in the data. If the initialization method uses specific means (/INIT=2), then the number of columns of *iWave* (see /INW) must match *num*. The default number of classes is 2. |
| <span class="table-cell-nowrap">/OUT = *format*</span> | Specifies the format for the results. |
|  |<table class="nested-table"><tbody><tr><td>*format*=1:</td><td>Default; output only the specification of the classes in the 2D wave M_KMClasses. Each column in M_KMClasses represents a class. The number of rows in M_KMClasses is equal to the number of rows in *populationWave* +1. The last row contains the number of class members. The remaining rows represent the center of the class. For example, if *populationWave* has two rows, then the dimensionality of the problem is 2 and M_KMClasses has 3 rows with the first row containing the first components of each class center, the second row containing the second components of each class center and the third row containing the number of elements in each class.</td></tr><tr><td>*format*=2:</td><td>Output (in addition to M_KMClasses) the class membership in the wave W_KMMembers. The rows in this 1D wave correspond to sequential members of *populationWave* and the entries correspond to the (zero based) column number in M_KMClasses.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/SEED = *val*</span> | Sets the seed for a new sequence in the pseudo-random number generator that is used by the operation. *val* must be an integer greater than zero. |
|  | By changing the sequence you may be able to find new solutions or just make the process converge at a different rate. |
| <span class="table-cell-nowrap">/TER = *method*</span> | Determines when the iterations stop. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=1:</td><td>User-specified number of iterations (/TERN).</td></tr><tr><td>*method*&nbsp;=2:</td><td>Continue iterating until no more than a fixed number of elements change classes in one iteration (TERN). This is the default termination method.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/TERN = *num*</span> | Specifies the termination number. The meaning of the number is determined by /TER above. By default, the termination *method* =2 and the default value of the maximum number of elements that change classes in one iteration is 5% of the size of the population. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. If an error occurs, sets V_flag to a non-zero error code but does not halt function execution. |

### *Details* {#details}
KMeans uses an iterative algorithm to analyze the clustering of data. The algorithm is not guaranteed to find a global optimum (maximum likelihood solution), so the operation provides various flags to control when the iterations terminate. You can determine if the operation iterates a fixed number of times or loops until at most a specified maximum number of elements change class membership in a single iteration. If you are computing KMeans in more than one dimension, you should pay attention to the relative magnitudes of the data in each dimension. For example, if your data is distributed on the interval [0,1] in the first dimension and on the interval [0,1e7] in the second dimension, the operation will be biased by the much larger magnitude of values in the second dimension.

### *Examples* {#examples}
Create data with 3 classes:


```igor
Make/O/N=(1,128) jack=4+gnoise(1)
jack[0][15,50]+=10
jack[0][60,]+=20
```

Perform KMeans looking for 5 classes:


```igor
KMeans/init=1/out=1/ter=1/dead=1/tern=1000/ncls=5 jack
Print M_KMClasses
  M_KMClasses[0][0]= {24.1439,68}
  M_KMClasses[0][1]= {14.1026,36}
  M_KMClasses[0][2]= {4.01537,24}
```

### *See Also* {#see-also}
[FPClustering](/igorpro/commands/fpclustering.md)

### *Demos* {#demos}
[Open Clustering Demo](#igor-pxp/Examples/Analysis/Clustering.pxp)