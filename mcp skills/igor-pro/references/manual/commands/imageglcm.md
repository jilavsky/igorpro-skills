---
description: "The ImageGLCM operation calculates the gray-level co-occurrence matrix for an 8-bit grayscale image and optionally evaluates Haralick's texture parameters."
slug: /commands/imageglcm
---

<div className="command-signature">

## <strong>ImageGLCM</strong>  [/Z /FREE /D=<em>distance</em> /E=<em>structure</em> /P=<em>plane</em> /HTFP /DEST=<em>destGLCM</em> /DETP=<em>destParamWave</em>] <em>srcWave</em> {#imageglcm}

</div>

The ImageGLCM operation calculates the gray-level co-occurrence matrix for an 8-bit grayscale image and optionally evaluates Haralick's texture parameters.

The ImageGLCM operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D = *distance*</span> | Sets the offset in pixels for which the co-occurrence matrix is calculated. The default value is 1. |
| <span class="table-cell-nowrap">/DEST = *destGLCM*</span> |  |
|  | Specifies the wave to hold the co-occurrence matrix. If you omit /DEST the operation stores the matrix in the wave M_GLCM in the current data folder. |
| <span class="table-cell-nowrap">/DETP = *destParamWave*</span> |  |
|  | Specifies the wave to hold the computed texture parameters. If you omit /DETP the operation stores the texture parameters in the wave W_TextureParams in the current data folder. |
|  | If the destination wave already exists it is overwritten. Note that you must specify the /HTFP flag to compute the texture parameters. |
| <span class="table-cell-nowrap">/E = *structureBits*</span> |  |
|  | *structureBits* is a bitwise setting that lets you control the combination of co-occurrences that you want to compute. |
|  | Consider a wave displayed in a table and a pixel at position x |
|  | $$ \displaystyle \begin{array}{lll} 0 & 3 & 5 \\ 1 & x & 6 \\ 2 & 4 & 7 \end{array} $$ |
|  | The *structureBits* corresponding to co-occurrence between x and any direction is simply 2^*direction*. By default the operation computes all combinations. This is equivalent to *structureBits*=255. |
|  | Note that the *structureBits* only define directions. The combination of the distance (/D) and the the *structureBits* define the full co-occurrence calculation. |
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">/FREE</span> | Creates output waves as free waves. |
|  | /FREE is permitted in user-defined functions only, not from the command line or in macros. |
|  | If you use /FREE then *destGLCM* and *destParamWave* must be simple names, not paths. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for details on free waves. |
| <span class="table-cell-nowrap">/HTFP</span> | Computes Haralick's texture parameters. See the discussion in the Details section below for more information about the texture parameters. |
| <span class="table-cell-nowrap">/P = *plane*</span> | If the image consists of more than one plane you can use this flag to determine which plane in *srcWave* is analysed. By default it is plane zero. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
ImageGLCM computes the co-occurrence matrix for the image in *srcWave*  and optionally evaluates Haralick's texture parameters. The operation supports 8-bit grayscale images and generates a 256x256 single-precision floating point co-occurrence matrix.

The elements of the matrix P[i][j] are defined as the normalized number of pixels that have a spatial relationship defined by the distance (/D) and the structure (/E) such that the first pixel has gray-level i and the second pixel has gray-level j. The matrix is normalized so that the sum of all its elements is 1.

If you specify the /HTFP flag the operation computes the 13 Haralick texture parameters and stores them sequentially in the destination wave (see /DETP). The wave is saved with dimension labels defining each element. The expressions for the texture parameters are:

$$
\displaystyle f_{1}=\sum_{i} \sum_{j}(p[i][j])^{2},
$$

$$
\displaystyle f_{2}=\sum_{n=0}^{254} n^{2}\left\{\sum_{i=0}^{255} \sum_{\substack{j=0 \\\quad|i-j|=n}}^{255} p[i][j]\right\},
$$

$$
\displaystyle f_{3}=\sum_{i} \sum_{j} \frac{\left(i-\mu_{x}\right)\left(j-\mu_{y}\right) p[i][j]}{\sigma_{x} \sigma_{y}},
$$

$$
\displaystyle f_{4}=\sum_{i} \sum_{j}(i-\mu)^{2} p[i][j],
$$

$$
\displaystyle f_{5}=\sum_{i} \sum_{j} \frac{1}{1+(i-j)^{2}} p[i][j],
$$

$$
\displaystyle f_{6}=\sum_{i} i p_{x+y}(i),
$$

$$
\displaystyle f_{7}=\sum_{i}\left(i-f_{6}\right)^{2} p_{x+y}(i),
$$

$$
\displaystyle f_{8}=-\sum_{i} p_{x+y}(i) \log \left(p_{x+y}(i)\right),
$$

$$
\displaystyle f_{9}=-\sum_{i} \sum_{j} p[i][j] \log (p[i][j]),
$$

$$
\displaystyle f_{10}=\operatorname{Variance}\left(p_{x-y}\right),
$$

$$
\displaystyle f_{11}=\sum_{i} p_{x-y}(i) \log \left(p_{x-y}(i)\right),
$$

$$
\displaystyle f_{12}=\frac{f_{9}-H X Y 1}{\max (H X, H Y)},
$$

$$
\displaystyle f_{13}=\sqrt{1-\exp (-2(H X Y 2-f 9))} .
$$

Here

$$
\displaystyle p_{x}(i)=\sum_{j} p[i][j], \quad p_{y}(j)=\sum_{i} p[i][j],
$$

$$
\displaystyle \mu_{x}=\sum_{i} i p_{x}(i), \quad \mu_{y}=\sum_{i} i p_{y}(i), \quad \mu=\left(\mu_{x}+\mu_{y}\right) / 2 .
$$

$$
\displaystyle \sigma_{x}=\sqrt{\sum_{i}\left(1-\mu_{x}\right)^{2} p_{x}(i)}, \quad \sigma_{y}=\sqrt{\sum_{i}\left(1-\mu_{y}\right)^{2} p_{y}(i)},
$$

$$
\displaystyle p_{x+y}(k)=\sum_{i} \sum_{\substack{j \\ \quad i+j=k}} p[i][j],
$$

$$
\displaystyle p_{x-y}(k)=\sum_{i} \sum_{\substack{j \\\quad \quad |i-j|=k}} p[i][j],
$$

$$
\displaystyle H X Y 1=-\sum_{i} \sum_{j} p[i][j] \log \left(p_{x}(i) p_{y}(j)\right),
$$

$$
\displaystyle H X Y 2=-\sum_{i} \sum_{j} p_{x}(i) p_{y}(j) \log \left(p_{x}(i) p_{y}(j)\right),
$$

$$
\displaystyle H X=-\sum_{i} p_{x}(i) \log \left(p_{x}(i)\right), \quad H Y=-\sum_{i} p_{y}(i) \log \left(p_{y}(i)\right) .
$$

There are at least two versions of f<sub>7</sub> used in the literature and in software. We know of at least three versions of f<sub>14</sub> so ImageGLCM does not compute it.

### *References* {#references}
R.M. Haralick, K. Shanmugam and Itshak Dinstein, "Textural Features for Image Classification", IEEE Transactions on Systems, Man, and Cybernetics, 1973.