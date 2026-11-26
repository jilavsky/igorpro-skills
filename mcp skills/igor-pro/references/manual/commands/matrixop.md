---
description: "The MatrixOp operation evaluates expression and stores the results in destWave."
slug: /commands/matrixop
---

<div className="command-signature">

## <strong>MatrixOp</strong>  [ /C /FREE /NTHR=<em>n</em>  /O /S ] <em>destwave</em> = <em>expression</em> {#matrixop}

</div>

The MatrixOp operation evaluates *expression* and stores the results in *destWave*.

*expression* may include literal numbers, numeric variables, numeric waves, and the set of operators and functions described below. MatrixOp does not support text waves, strings or structures.

MatrixOp is faster and in some cases more readable than standard Igor waveform assignments and matrix operations.

See [Using MatrixOp](/igorpro/analysis/analysis.md#using-matrixop) for an introduction to MatrixOp.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *destWave* | Specifies a destination wave for the assignment expression. *destWave* is created at runtime. If it already exists, you must use the /O flag to overwrite it or the operation returns an error. |
|  | When the operation is completed, *destWave* has the dimensions and data type implied by *expression*. In particular, it may be complex if *expression* evaluates to a complex quantity. If *expression* evaluates to a scalar, *destWave* is a 1x1 wave. |
|  | If you include the /FREE flag then *destWave* is created as a free wave. |
|  | Be default the data type of *destWave* depends on the data types of the operands and the nature of the operations on the right-hand side of the assignment. If *expression* references integer waves only, *destWave* may be an integer wave too but most operations with a scalars convert *destWave* into a double precision wave. See [MatrixOp Data Promotion Policy](/igorpro/analysis/analysis.md#matrixop-data-promotion-policy) for further discussion. |
|  | Even if *destWave* exists before the operation, MatrixOp may change its data type and dimensionality as implied by *expression*. |
|  | You can force the number type using MatrixOp functions such as `uint16` or `fp32`. |
| *expression* | *expression* is a mathematical expression referencing waves, local variables, global variables and literal numbers together with MatrixOp operators and MatrixOp functions as listed in the following sections. |
|  | You can use any combination of data types for operands. In particular, you can mix real and complex types in *expression*. MatrixOp determines data types of inputs and the appropriate output data type at runtime without regard to any type declaration such as Wave/C. |

### *Operators* {#operators}

|  |  |
| --- | --- |
| + | Addition between scalars, matrix addition or addition of a scalar (real or complex) to each element of a matrix. |
| - | Subtraction of one scalar from another, matrix subtraction, or subtracting a scalar from each element of a matrix. Subtraction of a matrix from a scalar is not defined. |
| \* | Multiplication between two scalars, multiplication of a matrix by a scalar, or element-by-element multiplication of two waves of the same dimensions. |
| / | Division of two scalars, division of a matrix by a scalar, or element-by-element division between two waves of the same dimensions. |
|  | Division of a scalar by a matrix is not supported but you can use the rec function with multiplication instead. |
| x | Matrix multiplication (lower case x symbol only). |
|  | This operator ***must*** be preceded and followed by a space. Matrix multiplication requires that the number of columns in the matrix on the left side be equal to the number of rows in the matrix on the right. |
| **.** | Generalized form of a dot product. In an expression *a*.*b* it is expected that *a* and *b* have the same number of points although they may be of arbitrary numeric type. The operator returns the sum of the products of the sequential elements as if both *a* and *b* were 1D arrays. |
|  | For complex binary operands waves *a* and *b*, this operator returns the MatrixOp equivalent of sum(*a*\*conj(*b*)). The [MatrixDot](/igorpro/commands/matrixdot.md) function returns sum(*b*\*conj(*a*)). |
| ^t | Matrix transpose. This is a postfix operator meaning that ^t appears after the name of a matrix wave. |
| ^h | Hermitian transpose. This is a postfix operator meaning that ^h appears after the name of a matrix wave. |
| && | Logical AND operator supports all real data types and results in a signed byte numeric token with the value of either 0 or 1. The operation acts on an element by element basis and is performed for each element of the operand waves. |
| \|\| | Logical OR operator supports all real data types and results in a signed byte numeric token with the value of either 0 or 1. The operation acts on an element by element basis and is performed for each element of the operand waves. |

MatrixOp does not support operator combinations such as +=.

This table shows the precedence of MatrixOp operators:


| MatrixOp Operator | Precedence |
| --- | --- |
| ^h             ^t | Highest |
| x                **.** |  |
| \*                / |  |
| +               - |  |
| &&            \|\| | Lowest |

You can use parentheses to force evaluation order.

When operators have the same precedence, execution associativity is from right to left. This means that a \* b / c is equivalent to a \* (b / c).

### *Functions* {#functions}
These functions are available for use with MatrixOp.


|  |  |
| --- | --- |
| abs(*w*) | Returns the absolute value of a real number or the magnitude of a complex number. |
| acos(*w*) | Returns the arc cosine of *w*. |
| acosh(*w*) | Returns the inverse hyperbolic cosine of *w*. Added in Igor Pro 7.00. |
| addCols(*w*,*dc*) | Returns a matrix where elements of the 1D wave *dc* are added to the corresponding column in w: |
|  | <code class="igor">out = w + dc[q]</code> |
|  | Added in Igor Pro 9.00. |
| addRows(*w*,*dr*) | Returns a matrix where elements of the 1D wave *dr* are added to the corresponding row in *w*: |
|  | <code class="igor">out = w + dr[p]</code> |
|  | Added in Igor Pro 9.00. |
| asin(*w*) | Returns the arc sine of *w*. |
| asinh(*w*) | Returns the inverse hyperbolic sine of *w*. Added in Igor Pro 7.00. |
| asyncCorrelation(*w*) | Returns the asynchronous spectrum correlation matrix for a real valued input matrix wave *w*. See syncCorrelation for details. |
| atan(*w*) | Returns the arc tangent (inverse tangent) of *w*. |
| atan2(*y*,*x*) | Returns the arc tangent (inverse tangent) of real *y*/*x*. |
| atanh(*w*) | Returns the inverse hyperbolic tangent of *w*. Added in Igor Pro 7.00. |
| averageCols(*w*) | Returns a (1xcolumns) wave containing the averages of the columns of matrix *w*. This is equivalent to sumCols(*w*)/numRows(*w*). |
|  | Added in Igor Pro 7.00. |
| axisToQuat(*ax*) | See ***Functions Using Quaternions*** below. |
| backwardSub(*U*,*c*) | Returns a column vector solution for the matrix equation Ux=c, where *U* is an (NxN) wave representing an upper triangular matrix and *c* is a column vector of N rows. If *c* has additional columns they are ignored. |
|  | Ideally, *U* and *c* should be either SP or DP waves (real or complex). Other numeric data types are supported with a slight performance penalty. |
|  | This function is typically used in solving linear equations following a matrix decomposition into lower and upper triangular matrices (e.g., Cholesky), with an expression of the form: |
|  | <code class="igor">MatrixOp/O solVector=backwardSub(U,forwardSub(L,b))</code> |
|  | where U and L are the upper and lower triangular factors. |
|  | Added in Igor Pro 7.00. |
| beam(*w*,*row*,*col*) | When *w* is a 3D wave the beam function returns a 1D array corresponding to the data in the beam defined by *w*[*row* ][*col* ][]. In other words, it returns a 1D array consisting of all elements in the specified row and column from all layers. See also [ImageTransform](/igorpro/commands/imagetransform.md) getBeam. |
|  | When *w* is a 4D wave it returns a 2D array containing *w*[*row* ][*col* ][][]. In other words, it returns a matrix consisting of all elements in the specified row and column from all layers and all chunks. |
|  | The beam function belongs to a special class in that it does not operate on a layer by layer basis. It therefore does not permit compound expressions in place of any of its parameters. |
|  | The beam function has the highest precedence. |
| binMean(*w*,*binWave*) | Returns a double precision matrix containing mean values of bins of data specified by the *binWave*. The binWave is a 1D wave containing pairs of indices. The first element of a pair is a bin's starting row index and the second member of the pair is the bin's last row index. Bins are allowed to overlap, but the first index has to be smaller or equal to the second index of each pair. The order of pairs within the *binWave* is unrestricted. The *binWave* must be real and should not include NaNs or INFs. Bin averages are computed for each column of *w*. Therefore, if *w* is an (mxn) matrix and  if *binWave* consists of 2k points, the function returns a (kxn) matrix of mean values. |
| binVar(*w*,*binWave*) | Similar to binMean() above, but returns the variance of the bins instead of the Mean. |
| bitAnd(*w1*,*w2*) | Returns an array of the same dimensions and number type as *w1* where each entry corresponds to the bitwise AND operation between *w1* and *w2*. |
|  | *w2* can be either a single number or a matrix of the same dimensions as *w1*. Both *w1* and *w2* must be real integer numeric types. |
|  | Added in Igor Pro 7.00. |
| bitOr(*w1*,*w2*) | Returns an array of the same dimensions and number type as *w1* where each element corresponds to the bitwise OR operation between *w1* and *w2*. |
|  | *w2* can be either a single number or a matrix of the same dimensions as *w1*. Both *w1* and *w2* must be real integer numeric types. |
|  | Added in Igor Pro 7.00. |
| bitReverseCol(*w*,*c*,*order*) |  |
|  | Returns the matrix *w* with the entries of column *c* reordered. |
|  | bitReverseCol was added in Igor Pro 9.00. |
|  | *order* is one of the following values: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Direct binary reversal of the index</td></tr><tr><td>1:</td><td>Hadamard order</td></tr><tr><td>2:</td><td>Dyadic/Paley/Gray order</td></tr><tr><td>3:</td><td>Unchanged order</td></tr></tbody></table>
|  | bitReverseCol can be used for changing the order of entries in fast transform algorithms such as FFT and the fast Walsh-Hadamard transform. The number of rows in *w* must be a power of 2. |
|  | See ***Examples*** below for an example using bitReverseCol. |
| bitShift(*w1*,*w2*) | Returns an array of the same dimensions and number type as *w1* shifted by the amount specified in *w2*. |
|  | *w2* can be either a single number or a matrix of the same dimensions as *w1*. Both *w1* and *w2* must be real integer numeric types. |
|  | When *w2* is positive the shifting is to the left. When it is negative the shifting is to the right. |
|  | Added in Igor Pro 7.00. |
| bitXor(*w1,w2*) | Returns an array of the same dimensions and number type as w1 where each element corresponds to the bitwise XOR operation between *w1* and *w2*. |
|  | *w2* can be either a single number or a matrix of the same dimensions as *w1*. Both *w1* and *w2* must be real integer numeric types. |
|  | Added in Igor Pro 7.00. |
| bitNot(*w*) | Returns an array of the same dimensions and number type as *w* where each element is the bitwise complement of the corresponding *w* element. |
|  | Added in Igor Pro 7.00. |
| catCols(*w1*,*w2*) | Concatenates the columns of *w2* to those of *w1*. *w1* and *w2* must have the same number of rows and the same number type. |
|  | Added in Igor Pro 7.00. |
| catRows(*w1*,*w2*) | Concatenates the rows of *w2* to those of *w1*. *w1* and *w2* must have the same number of columns and the same number type. |
|  | Added in Igor Pro 7.00. |
| cbrt(*w*) | Returns the cube root of the elements of *w*. When *w* is complex cbrt returns the principal cube root (the root with a positive imaginary number). |
|  | Added in Igor Pro 8.00. |
| ceil(*z*) | Returns the smallest integer larger than *z*. |
| chirpZ(*data*,*A*,*W*,*M*) | Returns the Chirp Z Transform of the 1D wave *data* calculated for the contour defined by |
|  | $$ \displaystyle \begin{array}{l} z_{k}=A W^{-k}, \\ \\ k=0,1, \ldots M-1 . \end{array} $$ |
|  | Here both *A* and *W* are complex and the standard z transform for a sequence {x(n)} is defined by |
|  | $$ \displaystyle X(z)=\sum_{k=0}^{N-1} x(n) z^{-k}. $$ |
|  | Note that the phase of the output is inverted to match the result of the ChirpZ transform on the unit circle with that of the FFT. |
| chirpZf(*data*,*f1*,*f2*,*df*) |  |
|  | Returns the Chirp Z Transform except that the transform parameters are specified by real valued starting frequency *f1*, end frequency *f2* and frequency resolution *df*. In this case the transform is confined to the unit circle because both *A* and *W* have unit magnitude. |
| chol(*w*) | Returns the Cholesky decomposition U of a positive definite symmetric matrix w such that w=U^t x U. Note that only the upper triangle of *w* is actually used in the computation. |
| chunk(*w*,*n*) | Returns chunk *n* from 4D wave *w.* |
|  | Added in Igor Pro 7.00. |
| clip(*w*,*low*,*high*) | Returns the values in the wave *w* clipped between the *low* and the *high* parameters. If *w* contains NaN or INF values, they are not modified. The result retains the same number type as the input wave *w* irrespective of the range of the *low* and *high* input parameters. |
| cmplx(*re*,*im*) | Returns a complex token from two real tokens. *re* and *im* must have the same dimensionality. |
|  | Added in Igor Pro 7.00. |
| col(*w*,*c*) | Returns column *c* from matrix wave *w*. |
| colRepeat(*w*,*n*) | Returns a matrix that consists of *n* identical columns containing the data in the wave *w*. If *w* is a 2D wave, it is treated as if it were a single column containing all the data. Higher dimensions are supported on a layer-by-layer basis. MatrixOp returns an error if *n*<2. |
|  | Added in Igor Pro 7.00. |
| conj(*matrixWave*) | Returns the complex conjugate of the input expression. |
| const(*r,c*,*val*) | Returns an (*r* x *c*) matrix where all elements are equal to *val.* The data type of the returned matrix is the same as that of *val*. See also zeroMat below. |
|  | Added in Igor Pro 7.00. |
| convolve(w1,w2,opt) | Returns the convolution of *w1* with *w2* subject to options *opt*. The dimensions of the result are determined by the largest dimensions of *w1* and *w2* with the number of rows padded (if necessary) so that they are even. Supported options include *opt*=0 for circular convolution and *opt*=4 for acausal convolution. |
|  | For fast 2D convolutions where where *w1* is an image and *w2* is a square kernel of the same numeric type, you can use *opt*=-1 or *opt*=-2. When *opt*=-1 the convolution at the boundaries is evaluated using zero padding. When *opt*=-2 the padding is a reflection of *w1* about the boundaries. When working with integer waves the kernel is internally normalized by the sum of its elements. The kernel for floating point waves remain unchanged. |
|  | To convolve an image in *w1* with a smaller point spread function in *w2* you can use: |
|  |<table class="nested-table"><tbody><tr><td>*opt*=-1:</td><td>If you want to pad the image boundaries with zeros or</td></tr><tr><td>*opt*=-2:</td><td>If you want to pad the boundaries by reflecting image values about each boundary.</td></tr></tbody></table>
|  | The negative options are designed for a very optimized convolution calculation which requires that *w1* and *w2* have the same numeric type. If the size of the point spread function is larger than about 13x13 it may become more efficient to compute the convolution using the positive options. |
| correlate(w1,w2,opt) |  |
|  | Returns the correlation of *w1* with *w2* subject to options *opt*. The dimensions of the result are determined by the largest dimensions of *w1* and *w2* with the number of rows padded (if necessary) so that they are even. Supported options include *opt*=0 for circular correlation and *opt*=4 for acausal correlation. |
| cos(*w*) | Returns the cosine of *w*. |
| cosh(*w*) | Returns the hyperbolic cosine of *w*. Added in Igor Pro 7.00. |
| covariance(*w*) | Returns the sample covariance matrix. Added in Igor Pro 8.00. |
|  | If *w* is a rows x cols real matrix then the returned value is the cols x cols matrix Q with elements |
|  | $$ \displaystyle q_{i j}=\frac{1}{\operatorname{rows}-1} \sum_{i=0}^{\text {rows }-1}\left(w_{i j}-\bar{w}_{j}\right)\left(w_{i k}-\bar{w}_{k}\right), $$ |
|  | where |
|  | $$ \displaystyle \bar{w}_{k}=\frac{1}{r o w s} \sum_{i=0}^{r o w s-1} w_{i k} . $$ |
| crossCovar(*w1*, *w2*, *opt*) |  |
|  | Returns the cross-covariance for 1D waves *w1* and *w2*. The options parameter *opt* can be set to 0 for the raw cross-covariance or to 1 if you want the results to be normalized to 1 at zero offset. If *w1* has N rows and *w2* has M rows then the returned vector is of length N+M-1. The cross-covariance is computed by subtracting the mean of each input followed by correlation and optional normalization. See also [Correlate](/igorpro/commands/correlate.md) with the /NODC flag. |
| decimateMinMax(*w*,*N*) | Decimates the matrix *w* on a column by column basis. Each column is divided into *N* bins and each bin is represented by its minimum and maximum values. |
|  | For an RxC real valued input *w*, the output is an array of dimensions 2*N*xC and the extrema are ordered as in {min0,max0,min1,max1...}. |
|  | Because of roundoff, sequential bins may not represent the same number of elements when R is not an integer multiple of *N*. In this case you not count on the exact form of the bin size roundoff. |
|  | The decimateMinMax function was added in Igor Pro 9.00. |
| det(*w*) | Returns a scalar corresponding to the determinant of matrix *w*, which must be real. |
| diagonal(*w*) | Creates a square matrix that has the same number of rows as *w*. All elements are zero except for the diagonal elements which are taken from the first column in *w*. Use DiagRC if the input is not an existing wave (such as a result from another function). |
| diagRC(*w*,*rows*,*cols*) |  |
|  | Returns a 2D matrix of dimensions *rows* by *cols*. All matrix elements are set to zero except those of the diagonal which are filled sequentially from elements of *w*. The dimensionality of *w* is unimportant. If the total number of elements in *w* is less than the number of elements on the diagonal then all elements will be used and the remaining diagonal elements will be set to zero. |
| e | Returns the base of the natural logarithm. |
| enoise(*w*) | Returns a token of the same dimensions as *w,* where each element is set to a value returned by enoise(w[i][j]). |
| equal(*w1,w2*) | Returns unsigned byte result with 1 for equality and zero otherwise. The dimensionality of the result matches the dimensionality of the largest parameter. |
|  | Either or both *w1* and *w2* can be constants (i.e., one row by one column). |
|  | If *w1* and *w2* are not constants, they must have the same number of rows and columns. If *w1* or *w2* have multiple layers, they must either have the same number of layers or one of them must have a single layer. |
|  | Both parameters can be either real or complex. A comparison of a real with a complex parameter returns zero. |
| erf(*w*) | Returns the error function (see [erf](/igorpro/commands/erf.md)) for the real values in *w*. |
| erfc(*w*) | Returns the complementary error function (see [erfc](/igorpro/commands/erfc.md)) for the real values in *w*. |
| exp(*w*) | Returns the exponential function for *w* which can be real or complex, scalar or a matrix. |
| expIntegralE1(w) | Returns the exponential integral for real arguments *w*. See also [ExpIntegralE1](/igorpro/commands/expintegrale1.md). Added in Igor Pro 9.00. |
| expm(*w*) | Returns the matrix exponential of a real-valued square matrix *w*. Added in Igor Pro 9.00. |
| FCT(*w*,*dir*) | See ***Trigonometric Transform Functions*** below. |
| fft(*w*,*options*) | Returns the FFT of *w*. |
|  | *w* must have an even number of rows. |
|  | *options* contains a binary field flag. Set bit 1 to 1 if you want to disable the zero centering (see /Z flag in the [FFT](/igorpro/commands/fft.md) operation). Other bits are reserved. |
|  | MatrixOp does not support wave scaling and therefore it does not produce the same wave scaling changes as the [FFT](/igorpro/commands/fft.md) operation. |
| floor(*w*) | Returns the largest integer smaller than *w*. If *w* is complex the function is separately applied to the real and imaginary parts. |
| forwardSub(*L*,*b*) | Returns a column vector solution for the matrix equation Lx=b, where *L* is an (NxN) wave representing a lower triangular matrix and *b* is a column vector of N rows. If *b* has additional columns they are ignored. |
|  | Ideally, *L* and *b* should be either SP or DP waves (real or complex). Other numeric data types are supported with a slight performance penalty. |
|  | This function is typically used in solving linear equations following a matrix decomposition into lower and upper triangular matrices (e.g., Cholesky), with an expression of the form: |
|  | <code class="igor">MatrixOp/O solVector=backwardSub(U,forwardSub(L,b))</code> |
|  | where U and L are the upper and lower triangular factors. |
|  | Added in Igor Pro 7.00. |
| fp32(*w*) | Converts *w* to 32-bit single precision floating point representation. See also the /NPRM flag below for more information. Added in Igor Pro 7.00. |
| fp64(*w*) | Converts *w* to 64-bit double precision floating point representation. See also the /NPRM flag below for more information. Added in Igor Pro 7.00. |
| Frobenius(*w*) | Returns the Frobenius norm of a matrix defined as the square root of the sum of the squared absolute values of all elements. |
| FST(*w*,*dir*) | See ***Trigonometric Transform Functions*** below. |
| FSST(*w*,*dir*) | See ***Trigonometric Transform Functions*** below. |
| FSCT(*w*,*dir*) | See ***Trigonometric Transform Functions*** below. |
| FSST2(*w*,*dir*) | See ***Trigonometric Transform Functions*** below. |
| FSCT2(*w*,*dir*) | See ***Trigonometric Transform Functions*** below. |
| gamma(*w*) | Returns the gamma function for real arguments *w*. See also [gamma](/igorpro/commands/gamma.md). Added in Igor Pro 9.00. |
| gammaln(*w*) | Returns the the natural log of the gamma function for real arguments *w*. See also [gammln](/igorpro/commands/gammln.md). Added in Igor Pro 9.00. |
| getDiag(w2d,d) | Returns a 1D wave that contains diagonal *d* of *w2d*. *d*=0 is the main diagonal, *d*>0 correspond to upper diagonals and *d*<0 to lower diagonals. |
|  | Added in Igor Pro 7.00. |
| greater(*a*,*b*) | Returns an unsigned byte for the truth of *a* > *b*. Both *a* and *b* must be real, but one or both can be constants (see equal() above). The dimensionality of the result matches the dimensionality of the largest parameter. |
| greaterOrEqual(*a*,*b*) | Returns an unsigned byte for the truth of *a* >= *b*. Both *a* and *b* must be real, but one or both can be constants (see equal() above). The dimensionality of the result matches the dimensionality of the largest parameter. |
|  | Added in Igor Pro 9.00. |
| hypot(*w1*,*w2*) | Returns the square root of the sum of the squares of *w1* and *w2*. |
|  | Added in Igor Pro 7.00. |
| ifft(*w*,*options*) | Returns the IFFT of *w*. |
|  | *options* is a bitwise parameter defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Forces the result to be real, like the [IFFT](/igorpro/commands/ifft.md) operation /C flag.</td></tr><tr><td>Bit&nbsp;1:</td><td>Disables center-zero.</td></tr><tr><td>Bit&nbsp;2:</td><td>Swaps the results.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | MatrixOp does not support wave scaling and therefore it does not produce the same wave scaling changes as the [IFFT](/igorpro/commands/ifft.md) operation. |
| identity(*n*,*m*) |  |
| identity(*n*) | Creates a computational object that is an identity matrix. If you use a single argument *n*, the identity created is an (*n* x*n*) square matrix with 1's for diagonal elements (the remaining elements are set to zero). If you use both arguments, the function creates an (*n* x*m*) zero matrix and fills its diagonal elements with 1's. Note that the identity is created at runtime and persists only for the purpose of the specific operation. |
| imag(*w*) | Returns the imaginary part of *w*. |
| indexCols(*w*) | Returns a token of the same dimensions as *w* where each element is equal to its column index. This is the MatrixOp equivalent of q used on righthand side of a standard wave assignment statement. The returned token is unsigned 32-bit integer if the number of columns in *w* is less than 2<sup>32</sup> or double-precision floating point otherwise. Added in Igor Pro 8.00. |
| IndexMatch(*w*,*val* [,*tol*]) | Returns a two-column wave specifying the row and column of the matrix *w* where a match for *val* is found (subject to the optional *tol*). The input *w* can be 1D or 2D. Higher dimensions are not supported. |
| indexRows(*w*) | Returns a token of the same dimensions as *w* where each element is equal to its row index. This is the MatrixOp equivalent of p used on righthand side of a standard wave assignment statement. The returned token is unsigned 32-bit integer if the number of rows in *w* is less than 2<sup>32</sup> or double-precision floating point otherwise. Added in Igor Pro 8.00. |
| inf() | Returns INF. Added in Igor Pro 7.00. |
| insertMat(s,d,r,c) | Inserts matrix *s* into matrix *d* starting at row *r* and column *c*. The waves *s* and *d* must be of the same numeric data type. The inserted range is clipped to the dimension of the wave *d*. Both *r* and *c* must be non-negative. Added in Igor Pro 7.00. |
| int8(*w*) | Converts *w* to 8-bit signed integer representation. See also the /NPRM flag below for more information. Added in Igor Pro 7.00. |
| int16(*w*) | Converts *w* to 16-bit signed integer representation. See also the /NPRM flag below for more information. Added in Igor Pro 7.00. |
| int32(*w*) | Converts *w* to 32-bit signed integer representation. See also the /NPRM flag below for more information. Added in Igor Pro 7.00. |
| integrate(*w*,*opt*) | Returns a running sum of *w*. |
|  | If *opt*=0 the sum runs over the entire input wave treating the columns of 2D waves as if they were part of one big column. |
|  | If *opt*=1 the running sum is computed separately for each column of a 2D wave. |
|  | Added in Igor Pro 7.00. |
| intMatrix(*w*) | Returns a double-precision matrix of the same dimensions as *w*. |
|  | Each element of the returned matrix is the sum of all the corresponding elements of *w* that are above and to the left of it, i.e., |
|  | $$ \displaystyle \text { out }_{i j}=\sum_{m=0}^{i} \sum_{n=0}^{j} w_{m n} . $$ |
|  | The utility of this function is apparent in the following relationship: |
|  | $$ \displaystyle \sum_{i=x_{1}}^{x_{2}} \sum_{j=y_{1}}^{y_{2}} w_{i j}=\operatorname{out}\left[x_{2}, y_{2}\right]-\operatorname{out}\left[x_{2}, y_{1}-1\right]-\operatorname{out}\left[x_{1}-1, y_{2}\right]+\operatorname{out}\left[x_{1}-1, y_{1}-1\right] . $$ |
|  | intMatrix was added in Igor Pro 7.00. |
| inv(*w*) | Returns the inverse of the square matrix *w*. |
|  | If *w* is not invertible, the operation returns a matrix of the same dimensions where all elements are set to NaN. |
| inverseErf(*w*) | Returns the inverse error function (see [inverseErf](/igorpro/commands/inverseerf.md)) for the real values in *w*. |
|  | Added in Igor Pro 7.00. |
| inverseErfc(*w*) | Returns the inverse complementary error function (see [inverseErfc](/igorpro/commands/inverseerfc.md)) for the real values in *w*. |
|  | Added in Igor Pro 7.00. |
| kronProd(*u,v*) | Returns the Kronecker product of matrices *u* and *v*. |
|  | kronProd was added in Igor Pro 9.00. |
|  | If *u* has dimensions M x N and *v* has dimensions P x Q then the returned block matrix has dimensions M*P x N*Q. It is given by |
|  | $$ \displaystyle u \otimes v=\left[\begin{array}{cccccccccc} u_{11} v_{11} & u_{11} v_{112} & \cdots & u_{11} v_{1 q} & \cdots & \cdots & u_{1 n} v_{11} & u_{1 n} v_{12} & \cdots & u_{1 n} v_{1 q} \\ u_{11} v_{21} & u_{11} v_{22} & \cdots & u_{11} v_{2 q} & \cdots & \cdots & u_{1 n} v_{21} & u_{1 n} v_{22} & \cdots & u_{1 n} v_{2 q} \\ \vdots & \vdots & \ddots & \vdots & & & \vdots & \vdots & \ddots & \vdots \\ u_{11} v_{p 1} & u_{11} v_{p 2} & \cdots & u_{11} v_{p q} & \cdots & \cdots & u_{1 n} v_{p 1} & u_{1 n} v_{p 2} & \cdots & u_{1 n} v_{p q} \\ \vdots & \vdots & & \vdots & & & \vdots & \vdots & & \vdots \\ \vdots & \vdots & & \vdots & & & \vdots & \vdots & & \vdots \\ u_{m 1} v_{11} & u_{m 1} v_{12} & \cdots & u_{m 1} v_{1 q} & \cdots & \cdots & u_{m n} v_{11} & u_{m n} v_{12} & \cdots & u_{m n} v_{1 q} \\ u_{m 1} v_{21} & u_{m 1} v_{22} & \cdots & u_{m 1} v_{2 q} & \cdots & \cdots & u_{m n} v_{21} & u_{m n} v_{22} & \cdots & u_{m n} v_{2 q} \\ \vdots & \vdots & \ddots & \vdots & & & \vdots & \vdots & & \vdots \\ u_{m 1} v_{p 1} & u_{m 1} v_{p 2} & \cdots & u_{m 1} v_{p q} & & & u_{m n} v_{p 1} & u_{m n} v_{p 2} & & u_{m n} v_{p q} \end{array}\right] $$ |
|  | See ***Examples*** below for an example using kronProd. |
| layer(*w*,*n*[,*chunk*]) | Returns a layer of a 3D or 4D wave. |
|  | The layer function was added in Igor Pro 7.00. |
|  | The optional *chunk* parameter was added in Igor Pro 9.00. |
|  | If you omit *chunk* and *w* is a 3D wave, the layer function returns layer *n* from *w*. |
|  | If you omit *chunk* and *w* is a 4D wave, the layer function returns layer *n* of chunk 0 from *w*. |
|  | If you include *chunk*, w must be a 4D wave and the layer function returns layer *n* of the specified chunk from *w*. |
|  | In all cases *w* must be a an actual wave and not an expression. |
| layerStack(*w*,*n*) |  |
|  | The layerStack function takes a 4D input wave *w* and a layer number *n* and returns a 3D wave (stack) that contains sequentially the data in layer *n* of each chunk of *w*. *w* must be a wave and not a derived token. |
|  | layerStack was added in Igor Pro 9.00. |
|  | Example: |
|  | <code class="igor">// Create a 3D stack from the red channel of a 4D RGB movie wave&#10;MatrixOP/O redChannelStack=layerStack(myRGBMovie,0)</code> |
| limit(*w*,*low*,*high*) | Returns the values in the wave *w* clipped between the *low* and the *high* parameters. Unlike the clip() function, limit() clips +-INF values to the specified [low,high] range. The result retains the same number type as the input wave *w* irrespective of the range of the *low* and *high* input parameters. |
| limitProduct(*w1*,*w2*) | Returns a partial element-by-element multiplication of waves *w1* and *w2*. |
|  | It is assumed that the dimensions of *w1* are greater than or equal to those of *w2*. If *w2* is of dimensions NxM then the function returns a matrix of the same dimensions as *w1* with the first NxM elements contain the product of the corresponding elements in *w1* and *w2* and the remaining elements set to zero. |
|  | The function is designed to be used in filtering applications where the size of the kernel *w2* is much smaller than the size of the input *w1*. |
|  | Added in Igor Pro 7.00. |
| log(*w*) | Returns the log base 10 of a token *w* which can be real or complex, scalar or a matrix. |
| log2(*w*) | Returns the log base 2 of a token *w* which can be real or complex, scalar or a matrix. log2 was added in Igor Pro 9.00. |
| ln(*w*) | Returns the natural logarithm of a token *w* which can be real or complex, scalar or a matrix. |
| mag(*w*) | Returns a real valued wave containing the magnitude of each element of *w*. This is equivalent to the abs function. |
| magSqr(*w*) | Returns a real value wave containing the square of a real *w* or the squared magnitude of complex *w*. |
| maxAB(*a*,*b*) | Returns the larger of the two real numbers *a* and *b*. |
|  | maxAB does not support NaN or complex inputs. |
|  | Added in Igor Pro 7.00. |
| maxMagAB(*a*,*b*) | For each data point in the tokens *a* and *b*, maxMagAB returns the one with the larger absolute value. |
|  | maxMagAB does not support complex numbers. |
|  | Added in Igor Pro 9.00. |
| maxCols(*w*) | Returns a 1D wave containing the maximum value of each column in the wave *w*. If *w* is complex the output is the maximum magnitude of each column of *w*. |
|  | maxCols does not support NaNs. |
|  | Added in Igor Pro 7.00. |
| maxRows(*w*) | Returns a 1D wave containing the maximum value of each row in the wave *w*. If *w* is complex the output contains the maximum magnitude of each row of *w*. |
|  | maxRows does not support NaNs. |
|  | Added in Igor Pro 8.00. |
| maxVal(*w*) | Returns the maximum value of the wave *w*. If *w* is complex it returns the maximum magnitude of *w*. |
|  | When *w* is real, the returned number type is the same as *w*'s. |
|  | When *w* is complex, the result is real and represents the maximum of the magnitudes of the elements of *w*. If *w* is double precision then the result is double precision; otherwise it is single precision. |
|  | When *w* is a 3D or 4D wave, maxVal returns a (1 x 1 x layers x chunks) data token. |
|  | maxVal does not support NaN values. |
| mean(*w*) | Returns the mean value of *w*. |
| median(*w*, *r*, *c*) | Returns a matrix containing median values for *r* rows by *c* columns neighborhoods of entries of *w*. The median value is equivalent to the one returned by Igor's median() function. The median skips NaNs but not INFs. The return value is of type DP if the input is DP otherwise it is SP. The median is returned when both *r* and *c* are positive. Otherwise the function returns the original *w*. There is no data reflection or duplication along the boundaries. Instead, when entries are less than *r* or *c* from the corresponding boundary, the median is computed using the available values only. |
| minCols(*w*) | Returns a 1D wave containing the minimum value of each column in the wave *w*. If *w* is complex the output contains the minimum magnitude of each column of *w*. |
|  | minCols does not support NaNs. |
|  | Added in Igor Pro 8.00. |
| minAB(*a*,*b*) | Returns the smaller of the two real numbers *a* and *b*. |
|  | minAB does not support complex numbers. |
|  | Added in Igor Pro 9.00. |
| minMagAB(*a*,*b*) | For each data point in the tokens *a* and *b*, minMagAB returns the one with the smaller absolute value. |
|  | minMagAB does not support complex numbers. |
|  | Added in Igor Pro 9.00. |
| minRows(*w*) | Returns a 1D wave containing the minimum value of each row in the wave *w*. If *w* is complex the output contains the minimum magnitude of each row of *w*. |
|  | minRows does not support NaNs. |
|  | Added in Igor Pro 8.00. |
| minVal(*w*) | Returns the minimum value of the wave *w*. If *w* is complex the function returns the minimum magnitude of *w*. |
|  | When *w* is real, the returned number type is the same as *w*'s. |
|  | When *w* is complex, the result is real and represents the minimum of the magnitudes of the elements of *w*. If *w* is double precision then the result is double precision; otherwise it is single precision. |
|  | When *w* is a 3D or 4D wave, minVal returns a (1 x 1 x layers x chunks) data token. |
|  | minVal does not support NaN values. |
| mod(*w*,*b*) | Returns the remainder after dividing *w* by *b*. *b* can be a scalar or a matrix of the same dimensions as *w*. |
|  | Added in Igor Pro 7.00. |
| nan() | Returns NaN. |
| normalize(*w*) | Returns a normalized version of a vector or a matrix. Normalization is such that the returned token should have a unity magnitude except if all elements are zero, in which case output is unchanged. |
| normalizeCols(*w*) | Divides each column of the real wave *w* by the square root of the sum of the squares of all elements of the column. |
| normalizeRows(*w*) | Divides each row of the real wave *w* by the square root of the sum of the squares of all the elements in that row. |
| normP(*w,pn*) | Returns the p-norm of matrix *w* defined by |
|  | $$ \displaystyle \|W\|_{p}=\left(\sum_{j=0}^{\text {cols }} \sum_{i=0}^{\text {rows }}\|w[i][j]\|^{p}\right)^{1 / p} . $$ |
|  | The case of *pn*=2 is equivalent to the MatrixOp Frobenius function. |
|  | Added in Igor Pro 9.00. |
| not(w) | Returns an unsigned byte array of the same dimensions as *w*, where each entry corresponds to the binary test: |
|  | <code class="igor">w[i][j]==0? 1:0</code> |
|  | *w* can be any real number type. 
|  | Added in Igor Pro 10.00.
| numCols(*w*) | Returns the number of columns in *w*. When *w* is 1D the function returns 1. |
| numPoints(*w*) | Returns the number of points in a layer of *w*. |
| numRows(*w*) | Returns the number of rows in *w*. |
| numType(*w*) | Returns the number type of *w* : |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>*w* is a normal number</td></tr><tr><td>1:</td><td>*w* is +/-INF</td></tr><tr><td>2:</td><td>*w* is NaN</td></tr></tbody></table>
| oneNorm(*w*) | Returns the 1-norm of matrix *w* defined as the maximum absolute column sum |
|  | $$ \displaystyle \|W\|=\max _{0 \leq j \leq \text { cols }}\left(\sum_{i=0}^{\text {rows }}\|w[i][j]\|\right) . $$ |
|  | Added in Igor Pro 9.00. |
| outerProduct(*w1*,*w2*) | For a 1D wave *w1* containing M points and a 1D wave *w2* containing N points, outerProduct returns an M by N matrix where the (i,j) element is: |
|  | <code class="igor">out[i][j] = w1[i] * conj(w2[j])</code> |
|  | Added in Igor Pro 8.00. |
| p2Rect(*w*) | Converts each element of *w* from polar to rectangular representation. |
| phase(*w*) | Returns a real valued wave containing the phase of each element of *w* calculated using phase=atan2(y,x). |
| Pi | Returns π. |
| powC(*w1*,*w2*) | Returns the complex valued *w1*<sup>*w2*</sup> where *w1* and *w2* can be real or complex. |
| powR(*x*,*y*) | Returns *x*<sup>*y*</sup> for real *x* and *y*. |
| productCol(*w*,*c*) | Returns the a (1 x 1) wave containing the product of the elements in column *c* of wave *w*. The output is double precision real or complex. |
|  | Added in Igor Pro 7.00. |
| productCols(*w*) | Returns a (1 x cols) wave where each entry is the product of all the elements in the corresponding column. The output is double precision real or complex. |
|  | Added in Igor Pro 7.00. |
| productDiagonal(*w*,*d*) | Returns a (1 x 1) wave containing the product of the elements on the specified diagonal of wave *w*. *d*=0 is the main diagonal, *d*>0 correspond to upper diagonals and *d*<0 to lower diagonals. The output is double precision real or complex. |
|  | Added in Igor Pro 7.00. |
| productRow(*w*,*r*) | Returns a (1 x 1) wave containing the product of all elements in row *r* of wave *w*. The output is double precision real or complex. |
|  | Added in Igor Pro 7.00. |
| productRows(*w*) | Returns a (1 x rows) wave where each entry is the product of all the elements in the corresponding row. The output is double precision real or complex. |
|  | Added in Igor Pro 7.00. |
| quat(*arg*) | See ***Functions Using Quaternions*** below. |
| quatFromSpherical(*theta*, *phi*) |  |
|  | See ***Functions Using Quaternions*** below. |
| quatInverse(*inQuat*) | See ***Functions Using Quaternions*** below. |
| quatToEuler(*qIn,mode*) | See ***Functions Using Quaternions*** below. |
| quatToAxis(*qIn*) | See ***Functions Using Quaternions*** below. |
| quatToMatrix(*qIn*) | See ***Functions Using Quaternions*** below. |
| r2Polar(*w*) | Performs the equivalent of the [r2polar](/igorpro/commands/r2polar.md) function on each element of *w*, i.e., each complex number (x+iy) is converted into the polar representation r,theta with x+iy=r*exp(i*theta) |
| real(*w*) | Returns the real part of *w*. |
| rec(*w*) | Returns the reciprocal of each element in *w*. |
| redimension(*w,nr,nc*) |  |
|  | Returns an (*nr* x *nc* ) matrix from the data in the wave *w*. The data in *w* are moved contiguously (column by column regardless of dimensionality) into the output. If the output size is larger than *w* the remaining points are set to zero. If *w* contains more than one layer the new dimensions apply on a layer by layer basis. For example: |
|  | <code class="igor">Make/N=(10,20,30) ddd = p + 10*q + 100*r&#10;MatrixOp/O aa = redimension(ddd,25,1)</code> |
|  | creates a wave *aa* with dimensions (25,1,30). |
| removeCol(*w*, *c*) | Returns a copy of the matrix *w* with column *c* removed. |
| removeCols(*w*, *mask*) | Returns a copy of the matrix *w* with the masked columns removed. Here *mask* is a real numeric wave that has at least as many points as the number of columns in *w*. Columns in the matrix *w* are removed if the corresponding entry in the *mask* wave is non-zero. |
| replace(*w*,*findVal*,*replacementVal*) |  |
|  | Replace in wave *w* every occurrence of *findVal* with *replacementVal*. The wave *w* retains its dimensionality and number type. *replacementVal* is converted to the same number type as w which may cause truncation. |
| replaceInfs(*w*, *replacementVal*) |  |
|  | Returns a copy of the wave *w* with all INF entries replaced by *replacementVal*. If *w* is complex, replacement takes place if either the real or the imaginary parts are INF. If the *replacementVal* is real and *w* is complex, the imaginary component of replaced entries are set to zero. It is an error to provide a complex replacement value when *w* is real. |
| replaceNaNs(*w*,*replacementVal*) |  |
|  | Replaces every occurrence of NaN in the wave *w* with *replacementVal*. The wave *w* retains its dimensionality. *replacementVal* is converted to the same number type as *w* which may cause truncation. |
| reverseCol(*w*,*c*) | Returns the array *w* with column *c* in reverse order. |
|  | Added in Igor Pro 7.00. |
| reverseCols(*w*) | Returns the array *w* with all columns in reverse order. |
|  | Added in Igor Pro 7.00. |
| reverseRow(*w*,*r*) | Returns the array *w* with row *r* in reverse order. |
|  | Added in Igor Pro 7.00. |
| reverseRows(*w*) | Returns the array *w* with all rows reversed. |
|  | Added in Igor Pro 7.00. |
| rotateChunks(*w,n*) | Returns a matrix where the last *n* chunks of *w* are moved to chunks [0, *n*-1]. If *n* is negative then the first abs(*n*) chunks are moved to the end of the data. It is an error to pass NaN for *n*. |
|  | Added in Igor Pro 7.00. |
| rotateCols(*w*,*nc*) | Rotates the columns of a 2D wave *w* so that the last *nc* columns are moved to columns [0,*nc* -1] of the data. If *nc* is negative the first abs(*nc* ) columns are moved to columns [n-1-*nc* ,n-1]. Here n is the total number of columns. It is an error to pass NaN for *nc*. If *nc* is greater than the number of columns then the effective rotation is mod(*nc* ,actualCols). |
| rotateLayers(*w,n*) | Returns a matrix where the last *n* layers are moved to layers [0,*n*-1]. If *n* is negative then the first abs(*n*) layers are moved to the end of the data. It is an error to pass NaN for *n*. |
|  | Added in Igor Pro 7.00. |
| rotateRows(*w*,*nr*) | Rotates the rows of a 2D wave *w* so that the last *nr* rows are moved to rows [0,*nr* -1] of the data. If *nr* is negative the first abs(*nr* ) rows are moved to rows [n-1-*nr* , n-1] where n is the total number of rows. It is an error to pass NaN for *nr*. If *nr* is greater than the number of rows then the effective rotation is mod(*nr* ,actualRows). |
| round(*z*) | Rounds *z* to the nearest integer. The rounding method is "away from zero". |
| row(*w*,*r*) | Returns row *r* from matrix wave *w*. The returned row is a (1xC) wave where C is the number of columns in *w*. To convert it to a 1D wave use Redimension/N=(C). See also [ImageTransform](/igorpro/commands/imagetransform.md) getRow. |
| rowDiff(*w*) | When the matrix *w* is of dimensions rows x cols, this function returns a matrix *M* of dimensions (rows-1) x cols, where every element satisfies the relation: |
|  | <code class="igor">M[i][j] = w[i+1][j] - w[i][j]</code> |
|  | Added in Igor Pro 10.00. |
| rowRepeat(*w*,*n*) | Returns a matrix that consists of *n* identical rows containing the data in the wave *w*. If *w* is a 2D wave, it is treated as if it were a single column containing all the data. Higher dimensions are supported on a layer-by-layer basis. MatrixOp returns an error if *n*<2. |
|  | Added in Igor Pro 7.00. |
| scale(w,low,high) | Returns the values in the wave *w* scaled between the *low* and the *high* parameters. If *w* contains NaN or INF values, they are not modified. The result retains the same number type as that of *w* irrespective of the range of the *low* and *high* input parameters. |
| scaleChunks(*w*, *scalingW*) |  |
|  | Returns a wave containing chunks of *w* scaled by consecutive factors from *scalingW*. Here w must be a wave token (not a compound expression). The resulting wave has the same dimensions as *w*. If *w* is a 3D wave (or lower dimensions), all the data in *w* is scaled as a single chunk by the first entry in *scalingW*. |
| scaleCols(*w1*,*w2*) | Returns a matrix of the same dimensions as *w1* where each column of *w1* is scaled by the value in the corresponding row of the 1D wave *w2*. The number of rows in *w2* must equal the number of columns in *w1*. |
|  | Added in Igor Pro 7.00. |
| scaleLayers(*w*, *scalingW*) |  |
|  | Returns a wave containing layers of *w* scaled by consecutive factors from *scalingW*. If *w* is a 2D or 1D wave, all the data in *w* is scaled as a single layer by the first entry in *scalingW*. |
| scaleRows(*w1*,*w2*) | Returns a matrix of the same dimensions as *w1* where each row of *w1* is scaled by the value in the corresponding row of the 1D wave *w2*. The number of rows in *w2* must equal the number of rows in *w1*. |
|  | Added in Igor Pro 7.00. |
| select(*w,sr,sc*) | Returns a matrix consisting of the elements of the matrix *w* for which the row index satisfies (p%*sr*)=0 and the column index satisfies (q%*sc*)=0. The first row and column are always selected. |
|  | *sr* and *sc* must real, finite and non-negative. You can set them to zero to include all elements of a dimension. |
|  | Added in Igor Pro 9.00. |
| setCol(*w2d,c,w1d*) | Returns the data in the *w2d* with the contents of *w1d* stored in column *c*. |
|  | *w1d* must have at least as many elements as the number of rows of *w2d*. *w2d* and *w1d* must be either both real or both complex. |
|  | Added in Igor Pro 7.00. |
| setColsRange(*w*,*low*,*high*) |  |
|  | Returns a matrix in which each column of *w* is scaled to the range [*low*,*high*]. *w* must be real-valued. |
|  | setColsRange was added in Igor Pro 9.00. |
| setNaNs(*w,mask*) | Returns the data in the wave *w* with NaNs stored where the *mask* wave is non-zero. The wave *w* can be of any numeric type. |
|  | *mask* must have the same dimensions as *w* and must be real. It is usually the result of another expression. For example, to set all values in the destination to NaN where *w* is greater than 5: |
|  | <code class="igor">MatrixOp/O out = setNaNs(w,greater(w,5))</code> |
|  | Added in Igor Pro 7.00. |
| setOffDiag(*w*,*d*,*w1*) | Returns the data in the *w* with the contents of *w1* stored in diagonal *d*. |
|  | *d*=0 is the main diagonal of *w*, *d*>0 correspond to upper diagonals and *d*<0 to lower diagonals. *w* and *w1* can either be both real or both complex. |
|  | Added in Igor Pro 7.00. |
| setRow(*w2d,r,w1d*) | Returns the data in the *w2d* with the contents of *w1d* stored in row *r*. |
|  | *w1d* must have at least as many elements as the number of columns in *w2d*. *w2d* and *w1d* must be either both real or both complex. |
|  | Added in Igor Pro 7.00. |
| setType(*w*, wType) | Returns a wave of the same dimensions as *w* having data type specified by *wType*. Supported wave types are: 2, 4, 8, 16, 32, 72, 80, 96. These correspond to fp32, fp64, int8, int16, int32,uint8, uInt16, and uInt32. These values can also be OR'ed with 1 to get the corresponding complex type. |
| sgn(*w*) | Returns the sign of each element in *w*. It returns -1 for negative numbers and 1 otherwise. It does not accept complex numbers. |
| shiftVector(*w*,*n*,*val*) | Shifts the element of a 1D row-vector *w* by *n* elements and fills the displaced elements with *val*, which must match the data type of *w* and should be expressed as cmplx(*a*,*b*) for complex *w*. |
| sin(*z*) | Returns the sine of *z*. |
| sinh(*z*) | Returns the hyperbolic sine *z*. Added in Igor Pro 7.00. |
| slerp(*qIn1*,*qIn2*,*frac*) | See ***Functions Using Quaternions*** below. |
| spliceCols(*w*,*c*,*d*,*ic*) | Returns a matrix where *ic* columns from matrix *d* are spliced into matrix *w* starting at column *c* of *w*. Matrix *d* must have the same number of rows as matrix *w* and they must both have the same number type. *ic* must be non-negative integer. If *ic* is greater than the number of columns in the matrix *d*, the function repeats as many columns of *d* as necessary. |
|  | Added in Igor Pro 9.00. |
| sq(*w*) | Returns the square of each element in the matrix *w*. |
|  | For complex elements z the returned value is z*z, not magsqr(z). |
|  | Added in Igor Pro 9.00. |
| sqrt(*z*) | Returns the square root of *z*. When z is real the function returns NaN for negative numbers. When z is complex the function returns the complex square root of z. |
| subRange(*w*,*rs*,*re,cs,ce*) |  |
|  | Returns a contiguous subset of the wave *w* from starting row *rs* through ending row *re* and from starting column *cs* through ending column *ce*. This is similar to Duplicate/R except that dimension scaling and labels are not preserved. |
| subtractCols(w, wc) | Returns a wave of the same dimensions as *w* where the 1D wave *wc* is subtracted from each column of *w*. The wave wc must have the same number of points as the rows in *w*. |
| subtractMean(*w*,*opt*) | Computes the mean of the real wave *w* and returns the values of the wave minus the mean value (*opt*=0). Computes the mean of each column and subtracts it from that column (*opt*=1). Subtracts the mean of each row from row values (*opt*=2). |
| subtractMin(*w*) | Returns a wave of the same dimensions of *w* where the minimum value of *w* is subtracted from each entry. This function does not support complex valued *w*. |
| subtractRows(w, wr) | Returns a wave of the same dimensions as *w* where the 1D wave *wr* is subtracted from each row of *w*. The wave wr must have the same number of points as the columns in *w*. |
| subWaveC(*w*,*r,c,count[,stride]*) |  |
|  | Returns a subset of the data that is sampled along columns of the wave *w*, containing *count* elements starting with the element at row *r* and column *c*. By default *stride*=1 and the sampling is continuous. |
|  | You can specify a negative *stride* to sample backwards from the starting element. |
|  | The operation returns an error if the sampling would exceed the array bounds in either direction.<br>Examples: |
|  | <code class="igor">Make/O/N=(22,33) ddd=x&#10;MatrixOP/O/P=1 aa=subWaveC(ddd,4,5,10,2)&#10;//	aa={4,6,8,10,12,14,16,18,20,0}&#10;MatrixOP/O/P=1 aa=subWaveC(ddd,4,5,5,-4)&#10;//	aa={4,0,18,14,10}</code> |
| subWaveR(*w*,*r,c,count[,stride]*) |  |
|  | Returns a subset of the data that is sampled along rows of the wave *w*, containing *count* elements starting with the element at row *r* and column *c*. By default *stride*=1 and the sampling is continuous. |
|  | You can specify a negative *stride* to sample backwards from the starting element. |
|  | The operation returns an error if the sampling would exceed the array bounds in either direction.<br>Examples: |
|  | <code class="igor">Make/O/N=(10,20) ddd=y&#10;// Forward sampling across right boundary&#10;MatrixOP/O/P=1 aa=subWaveR(ddd,4,15,6,2)&#10;//	aa={15,17,19,1,3,5}&#10;// Reverse sampling across left boundary&#10;MatrixOP/O/P=1 aa=subWaveR(ddd,2,3,5,-1)&#10;//	aa={3,2,1,0,19}</code>
| sum(*z*) | Returns the sum of all the elements in expression *z*. |
| sumBeams(*w*) | Returns an (n x m) matrix containing the sum over all layers of all the beams of the 3D wave *w* : |
|  | $$ \displaystyle \text { out }_{i j}=\sum_{k=0}^{\text {nLayers }-1} w_{i j k} . $$ |
|  | A beam is a 1D array in the Z-direction. |
|  | sumBeams is a non-layered function which requires that *w* be a proper 3D wave and not the result of another expression. |
| sumCols(*w*) | Returns an (1 x m) matrix containing the sums of the m columns in the nxm input wave *w*: |
|  | $$ \displaystyle \text { out }_{j}=\sum_{i=0}^{n R o w s-1} w_{i j} . $$ |
| sumND(*w*) | Returns a 1-point wave containing the sum of the token *w* regardless of its dimensionality. |
|  | sumND was added in Igor Pro 9.00. |
|  | This example illustrates the difference between sumND and the sum function which operates on a layer-by-layer basis: |
|  | <code class="igor">Make/O/N=(5,6,3) w3D = z&#10;MatrixOP/O/P=1 sumOut=sum(w3D)        // Prints 3 layer sums&#10;MatrixOP/O/P=1 sumNDOut=sumND(w3D)    // Prints a single sum</code> |
| sumRows(*w*) | Returns an (n x 1) matrix containing the sums of the n rows in the nxm input wave *w* : |
|  | $$ \displaystyle \text { out }_{i}=\sum_{j=0}^{\text {nCols }-1} w_{i j}. $$ |
| sumSqr(*w*) | Returns the sum of the squared magnitude of all elements in *w*. |
| syncCorrelation(*w*) | Returns the synchronous spectrum correlation matrix for a real valued input matrix wave w. See also asyncCorrelation. |
|  | The correlation matrix is computed by subtracting from each column of *w* its mean value, multiplying the resulting matrix by its transpose and finally dividing all elements by (nrows-1) where nrows is the number of rows in *w*. |
| tan(*w*) | Returns the tangent of *w*. |
| tanh(*w*) | Returns the hyperbolic tangent of *w*. Added in Igor Pro 7.00. |
| tensorProduct(*w1*,*w2*) | Returns a 2D matrix that is the tensor product of the 2D matrices *w1* and *w2*. For example, the tensor product of two (2 x 2) matrices is given by: |
|  | $$ \displaystyle \left(\begin{array}{ll} a_{11} & a_{12} \\ a_{21} & a_{22} \end{array}\right) \otimes\left(\begin{array}{ll} b_{11} & b_{12} \\ b_{21} & b_{22} \end{array}\right)=\left(\begin{array}{llll} a_{11} b_{11} & a_{11} b_{12} & a_{12} b_{11} & a_{12} b_{12} \\ a_{11} b_{21} & a_{11} b_{22} & a_{12} b_{21} & a_{12} b_{22} \\ a_{21} b_{11} & a_{21} b_{12} & a_{22} b_{11} & a_{22} b_{12} \\ a_{21} b_{21} & a_{21} b_{22} & a_{22} b_{21} & a_{22} b_{22} \end{array}\right) $$ |
|  | Added in Igor Pro 7.00. |
| Trace(*w*) | Returns a real or complex scalar which is the sum of the diagonal elements of *w*. If *w* is not a square matrix, the sum is over the elements for which the row and column indices are the same. |  |
| transposeVol(*w*,*mode*) | For 3D wave *w* , transposeVol returns a transposed 3D wave depending on the value of the *mode* parameter: |
|  |<table class="nested-table"><tbody><tr><td>*mode*=1:</td><td>output=w[p][r][q]</td></tr><tr><td>*mode*=2:</td><td>output=w[r][p][q]</td></tr><tr><td>*mode*=3:</td><td>output=w[r][q][p]</td></tr><tr><td>*mode*=4:</td><td>output=w[q][r][p]</td></tr><tr><td>*mode*=5:</td><td>output=w[q][p][r]</td></tr></tbody></table>
|  | transposeVol is a non-layered function which requires that *w* be a proper 3D wave and not the result of another expression. |
| triDiag(*w1*,*w2*,*w3*) | Returns a tri-diagonal matrix where *w1* is the upper diagonal, *w2* the main diagonal and *w3* the lower diagonal. If *w2* has n points then *w1* and *w3* are expected to have n-1 points. The waves can be of any numeric type and the returned wave has a numeric type that accommodates the input. |
| uint8(*w*) | Converts the token *w* to 8-bit unsigned integer representation. See also the /NPRM flag below for more information. Added in Igor Pro 7.00. |
| uint16(*w*) | Converts the token *w* to 16-bit unsigned integer representation. See also the /NPRM flag below for more information. Added in Igor Pro 7.00. |
| uint32(*w*) | Converts the token *w* to 32-bit unsigned integer representation. See also the /NPRM flag below for more information. Added in Igor Pro 7.00. |
| varBeams(*w*) | Returns a matrix containing the variances of the beams of the real-valued 3D wave *w*. |
|  | varBeams was added in Igor Pro 9.00. |
|  | varBeams is a non-layered function which requires that *w* be a proper 3D wave and not the result of another expression. |
|  | When *w* consists of a single layer the returned variances are all NaN. |
| varCols(*w*) | Returns a (1 x cols) wave where each element contains the variance of the corresponding column in *w*. |
| waveX(*w*) | For pure wave argument *w*, waveX returns the X value for each point as determined by the wave's X scaling. |
|  | Added in Igor Pro 9.00. |
| waveY(*w*) | For pure wave argument *w*, waveY returns the Y value for each point as determined by the wave's Y scaling. |
|  | Added in Igor Pro 9.00. |
| waveZ(*w*) | For pure wave argument *w*, waveZ returns the Z value for each point as determined by the wave's Z scaling. |
|  | Added in Igor Pro 9.00. |
| waveT(*w*) | For pure wave argument *w*, waveT returns the T value for each point as determined by the wave's T scaling. |
|  | Added in Igor Pro 9.00. |
| waveIndexSet(*w1*,*w2*,*w3*) |  |
|  | Returns a matrix of the same dimensions as *w1* with values taken either from *w1* or from *w3* depending on values in *w2* using: |
|  | $$ \displaystyle \operatorname{out}[i][j]=\left\{\begin{array}{cc} w 1[i][j] & \text { if } w 2[i][j]<0 \\ \\ w 3[w 2[i][j]] & \text { otherwise } \end{array} .\right. $$ |
|  | *w1* and *w2* must have the same number of rows and columns. *w1* and *w3* must match in number type. *w2* cannot be unsigned. |
|  | Values from *w2* are used as point number indices into *w3* which is treated like a 1D wave regardless of its actual dimensionality. |
|  | An index value from *w2* is out-of-bounds if it is greater than or equal to the number of points in *w3*. In this case, the output value is taken from *w1* as if the index value were negative. |
| waveMap(*w1*,*w2*) | Returns an array of the same dimensions as *w2* containing the values *w1* [*w2* [i][j]]. The data type of the output is the same as that of *w1*. Values of *w2* are taken as 1D integer indices into the *w1* array. See also [IndexSort](/igorpro/commands/indexsort.md). |
| waveChunks(*w*) | Returns the number of chunks in the wave *w*. Added in Igor Pro 7.00. |
| waveLayers(*w*) | Returns the number of layers in the wave *w*. Added in Igor Pro 7.00. |
| wavePoints(*w*) | Returns the number of points in the wave *w*. Added in Igor Pro 7.00. |
| within(*w,low,high*[*,opt*]) |  |
|  | When the optional parameter *opt* is not used, the function returns an array of the same dimensions as *w* with the value 1, where the corresponding element of *w* is between low and high (low <= w[i][j] <=high) and zero otherwise. When *opt* is used, the function returns 1 for values within the specified range and *opt* otherwise. In particular, *opt* may be set to NaN to facilitate expressions of the form, e.g., |
|  | zapNaNs(within(*w,low,high*,NaN)) |
|  | The parameters *low* and *high* must be real and satisfy *low*<*high*. You can use *low*=-INF to remove the lower bound or *high*=INF to remove the upper bound. If *w* contains NaNs, the corresponding outputs are 0 (or *opt*). |
|  | The optional parameter *opt* was added in Igor 10.0 |
| zapINFs(*w*) | Returns a one-column wave containing the sequential data of *w* with all INF elements removed. The input w can be 1D or 2D but higher dimensions are not supported. |
|  | Added in Igor Pro 9.00. |
| zapNaNs(*w*) | Returns a one-column wave containing the sequential data of *w* with all NaN elements removed. The input w can be 1D or 2D but higher dimensions are not supported. |
|  | Added in Igor Pro 9.00. |
| zapZeros(*w*) | Returns a 1D wave having the same number type as *w* with all the zero entries removed. The input *w* may only be a 1D or a 2D wave. |
| zeroMat(*r,c,nt*) | Returns an (*r* x *c*) matrix of number type *nt* where all entries are set to zero. See [WaveType](/igorpro/commands/wavetype.md) for supported types. See also const above. |
|  | Added in Igor Pro 7.00. |

### *Trigonometric Transform Functions* {#trigonometric-transform-functions}

|  |  |
| --- | --- |
| FCT(*w*,*dir*) | Computes the fast, real to real cosine transform on 1D wave *w*. |
|  | Added in Igor Pro 8.00. |
|  | The forward transform (*dir*=1) is defined by: |
|  | $$ \displaystyle F(k)=\frac{1}{n}[f(0)+f(n) \cos (k \pi)]+\frac{2}{n} \sum_{i=1}^{n-1} f(i) \cos \left(\frac{i k \pi}{n}\right), \quad k=0, \ldots, n $$ |
|  | The number of intervals is n=numpnts(*w*)-1. |
|  | The inverse transform (*dir*=-1) is defined by: |
|  | $$ \displaystyle f(i)=\frac{1}{2}[F(0)+F(n) \cos (i \pi)]+\sum_{k=1}^{n-1} F(k) \cos \left(\frac{i k \pi}{n}\right), \quad i=0, \ldots n $$ |
|  | See ***Trigonometric Transforms*** below for more information. |
| FST(*w*,*dir*) | Computes the fast, real to real sine transform on 1D wave *w*. |
|  | Added in Igor Pro 8.00. |
|  | The forward transform (*dir*=1) is defined by: |
|  | $$ \displaystyle F(k)=\frac{2}{n} \sum_{i=1}^{n-1} f(i) \sin \left(\frac{i k \pi}{n}\right), \quad k=1, \ldots, n-1 $$ |
|  | where n=numpnts(*w*). |
|  | The inverse transform (*dir*=-1) is defined by: |
|  | $$ \displaystyle f(i)=\sum_{k=1}^{n-1} F(k) \sin \left(\frac{i k \pi}{n}\right), \quad i=1, \ldots, n-1 $$ |
|  | See ***Trigonometric Transforms*** below for more information. |
| FSST(*w*,*dir*) | Computes the fast, real to real staggered sine transform on 1D wave *w*. |
|  | Added in Igor Pro 8.00. |
|  | The forward direction (*dir*=1) is defined by: |
|  | $$ \displaystyle F(k)=\frac{1}{n} \sin \left(\frac{(2 k-1) \pi}{2}\right) f(n)+\frac{2}{n} \sum_{i=1}^{n-1} f(i) \sin \left(\frac{i(2 k-1) \pi}{2 n}\right), \quad k=1, \ldots, n $$ |
|  | where n=numpnts(*w*). |
|  | The inverse transform (*dir*=-1) is defined by: |
|  | $$ \displaystyle f(i)=\sum_{k=1}^{n} F(k) \sin \left(\frac{i(2 k-1) \pi}{2 n}\right), \quad i=1, \ldots n $$ |
|  | See ***Trigonometric Transforms*** below for more information. |
| FSCT(*w*,*dir*) | Computes the fast, real to real, staggered cosine transform on 1D wave *w*. |
|  | Added in Igor Pro 8.00. |
|  | The forward direction (*dir*=1) is defined by: |
|  | $$ \displaystyle F(k)=\frac{1}{n} f(0)+\frac{2}{n} \sum_{j=1}^{n-1} f(j) \cos \left(\frac{j \pi(2 k+1)}{2 n}\right), \quad k=0, \ldots, n-1 $$ |
|  | The inverse transform (*dir*=-1) is defined by: |
|  | $$ \displaystyle f(i)=\sum_{k=0}^{n-1} F(k) \cos \left(\frac{(2 k+1) i \pi}{2 n}\right), \quad i=0, \ldots, n-1 $$ |
|  | See ***Trigonometric Transforms*** below for more information. |
| FSST2(*w*,*dir*) | Computes the fast, real to real, staggered2 sine transform on 1D wave *w*. |
|  | Added in Igor Pro 8.00. |
|  | The forward direction (*dir*=1) is defined by: |
|  | $$ \displaystyle F(k)=\frac{2}{n} \sum_{i=1}^{n} f(i) \sin \left(\frac{(2 k-1)(2 i-1) \pi}{4 n}\right), \quad k=1, \ldots n $$ |
|  | The inverse transform (*dir*=-1) is defined by: |
|  | $$ \displaystyle f(i)=\sum_{k=1}^{n} F(k) \sin \left(\frac{(2 k-1)(2 i-1) \pi}{4 n}\right), \quad i=1, \ldots, n $$ |
|  | See ***Trigonometric Transforms*** below for more information. |
| FSCT2(*w*,*dir*) | Computes the fast, real to real, staggered2 cosine transform on 1D wave *w*. |
|  | Added in Igor Pro 8.00. |
|  | The forward direction (*dir*=1) is defined by: |
|  | $$ \displaystyle F(k)=\frac{2}{n} \sum_{i=1}^{n} f(i) \cos \left(\frac{(2 k-1)(2 i-1) \pi}{4 n}\right), \quad k=1, \ldots, n $$ |
|  | The inverse transform (*dir*=-1) is defined by: |
|  | $$ \displaystyle f(i)=\sum_{k=1}^{n} F(k) \cos \left(\frac{(2 k-1)(2 i-1) \pi}{4 n}\right), \quad i=1, \ldots, n $$ |
|  | See ***Trigonometric Transforms*** below for more information. |

### *Functions Using Quaternions* {#functions-using-quaternions}
These functions create and manipulate quaternion tokens or return quaternion results. They were added in Igor Pro 8.00. See [MatrixOp Quaternion Data Tokens](/igorpro/analysis/analysis.md#matrixop-quaternion-data-tokens) for background information on quaternions in MatrixOp.


|  |  |
| --- | --- |
| quat(*arg*) | Converts *arg* into a quaternion token. |
|  | *arg* can be: |
|  | • A scalar which is converted to a real quaternion |
|  | • A 1x3 or 3x1 wave which is converted to a pure imaginary quaternion |
|  | • The output from another quat call |
|  | Arithmetic on quaternion tokens obeys quaternion arithmetic rules. |
|  | *arg* must not be complex. The resulting quaternion token is not normalized by the quat function. |
|  | Added in Igor Pro 8.00. |
|  | See [MatrixOp Quaternion Data Tokens](/igorpro/analysis/analysis.md#matrixop-quaternion-data-tokens) for details. |
| quatFromSpherical(*theta*, *phi*) |  |
|  | Returns a 4-element 1D wave representing a MatrixOP quaternion token corresponding to the spherical polar angles *theta* and *phi*. |
|  | Added in Igor Pro 10.00. |
| quatInverse(*inQuat*) | Returns a 4-element 1D wave representing a MatrixOP quaternion token corresponding to the inverse of the input Quaternion. |
|  | Added in Igor Pro 10.00. |
| quatToMatrix(*qIn*) | Converts *qIn* into a quaterion token, if not already a quaterion token, normalizes it, and returns the equivalent 4x4 homogeneous rotation matrix. |
|  | Added in Igor Pro 8.00. |
| quatToAxis(*qIn*) | Converts *qIn* into a quaterion token, if not already a quaterion token, normalizes it, and returns the equivalent axis of rotation and rotation angle. The result is a 4-element wave in which the first three elements define the rotation axis and the last element is the rotation angle in radians. |
|  | Added in Igor Pro 8.00. |
| quatToEuler(*qIn*,*mode*) | Converts *qIn* into a quaterion token, if not already a quaterion token, and returns a 3x1 wave containing equivalent Euler angles expressed in radians. |
|  | The returned Euler angles are are phi (rotation about the X axis), theta (rotation about the Y axis), and psi (rotation about the Z axis). |
|  | The *mode* parameter defines the rotation sequence. The supported modes are: 121, 123,131, 132, 212, 213, 231, 232, 312, 313, 321 and 323. 1 designates the X axis, 2 the Y axis and 3 the Z axis. See, for example: [https://www.euclideanspace.com/maths/geometry/rotations/conversions/quaternionToEuler/quat_2_euler_paper_ver2-1.pdf](https://www.euclideanspace.com/maths/geometry/rotations/conversions/quaternionToEuler/quat_2_euler_paper_ver2-1.pdf) |
|  | Added in Igor Pro 8.00. |
| axisToQuat(*ax*) | *ax* is a 4-element wave with the axis of rotation in the first 3 elements and the rotation angle in radians as the last element. Returns a 4-element wave containing the quaternion components representing this rotation. |
|  | Added in Igor Pro 8.00. |
| slerp(*qIn1*,qIn2,*frac*) | Performs spherical linear interpolation between quaternion *qIn1* and quaternion *qIn2*. *frac* is a value between 0 and 1 representing the amount of desired rotation from *qIn1* to *qIn2*. |
|  | The function returns a 4-element wave containing the quaternion components that represent the rotated quaternion. This is useful, for example, in animating a sequence of rotations. |
|  | Added in Igor Pro 8.00. |

### *Wave Parameters* {#wave-parameters}
MatrixOp was designed to work with 2D waves (matrices), but also works with 1D, 3D and 4D waves. A 1D wave is treated like a 1-column matrix. 3D and 4D waves are treated on a layer-by-layer basis, as if each layer were a matrix.

You can reference subsets of waves in *expression*. Only two types of subsets are supported: those that evaluate to a single element, which are treated as scalars, and those that evaluate to one or more layers. For example:


|  |  |
| --- | --- |
| wave1d[*a*] | Scalar |
| wave2d[*a*][*b*] | Scalar |
| wave3d[*a*][*b*][*c*] | Scalar |
| wave3d[][][*a*] | Layer *a* from 3D wave |
| wave3d[][][*a*,*b*] | Layers *a* through *b* from 3D wave |
| wave3d[][][*a*,*b*,*c*] | Layers *a* through *b* from stepping by *c* from 3D wave |

You can pass waves of any dimensions as parameters to MatrixOp functions. For example:


```igor
Make/O/N=128 wave1d = x
MatrixOp/O outWave = powR(wave1d,2)
```

MatrixOp does not allow using the same 3D wave on both sides of the assignment:


```igor
MatrixOp/O wave3D = wave3D + 3	// Not allowed
```

See [MatrixOp Wave Data Tokens](/igorpro/analysis/analysis.md#matrixop-wave-data-tokens) for further discussion.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AT = *allocationType*</span> |  |
|  | /AT lets you control the method used to allocate memory in MatrixOP. It was added in Igor Pro 9.00. |
|  |<table class="nested-table"><tbody><tr><td>*allocationType*&nbsp;=&nbsp;0:</td><td>Generic memory allocation.</td></tr><tr><td>*allocationType*&nbsp;=&nbsp;1:</td><td>Intel scalable allocation.</td></tr><tr><td>*allocationType*&nbsp;=&nbsp;2:</td><td>Intel scalable and aligned allocation.</td></tr></tbody></table>
|  | By default MatrixOP uses scalable and aligned allocation. |
| <span class="table-cell-nowrap">/C</span> | Provides a complex wave reference for *destWave*. If omitted, MatrixOp creates a real wave reference for *destWave*. The wave reference allows you to refer to the output wave in a subsequent statement of a user-defined function. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. Allowed only in functions and only if a simple name or wave reference structure field is specified. |
|  | Requires Igor Pr 6.1 or later. For advanced programmers only. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
| <span class="table-cell-nowrap">/FS</span> | Forces the operation to execute serially instead of using automatic multithreading or vectorized implementation. |
| <span class="table-cell-nowrap">/KCLS</span> | Use this flag to extend the dimensionality of the output.  For example, an output matrix whose dimensions are (Mx1) will be saved a 2D wave with M rows and 1 column while by default it is saved as a 1D wave.  Similarly, when the output consists of a single layer matrix, say (M,N,1) it will be saved as a 3D wave instead of a 2D (M,N) wave. |
| <span class="table-cell-nowrap">/NTHR = *n*</span> | Sets the number of threads used to compute the results for 3D waves. Each thread computes the results for a single layer of the input. |
|  | If /NTHR is omitted the calculations are performed by the main thread only. |
|  |<table class="nested-table"><tbody><tr><td>*n*&nbsp;=&nbsp;0:</td><td>The operation uses as many threads you have processors on your computer.</td></tr><tr><td>*n*&nbsp;&gt;&nbsp;0:</td><td>*n* specifies the number of threads to use. More threads may or may not improve performance.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/NPRM</span> | Use /NPRM to restrict the automatic promotion of numeric data types in MatrixOp expressions. |
|  | By default, MatrixOp promotes numeric data types so that operations result in reasonable accuracy. In some situations you may want to keep the results as a particular data type even at the risk of truncation or overflow. If you include the /NPRM flag, MatrixOp creates the destination wave using the highest precision data type in the expression. For example, an expression A=B+C where B is 16-bit wave and C is an 8-bit wave results in a 16-bit wave A. |
|  | Unsigned number types can result only when all operands are unsigned. |
|  | /NPRM is ignored when data promotion is required. For example: |
|  | <code class="igor">Make/B/U wave2&#10;MatrixOp/O/NPRM wave1 = -wave2</code> |
|  | You can use MatrixOp functions such as int8, int16, etc., to precisely control the number type of any token. |
| Conversion of singular values from floating point to integer types obey the following rules: |  |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>NaN is converted to zero</td></tr><tr><td>2.</td><td>INF is converted to the largest value of the destination integer type.</td></tr><tr><td>3.</td><td>-INF is converted to the smallest value of the destination integer type.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/NV = *mode*</span> | Controls use of Intel MKL vectorized functions. /NV was added in Igor Pro 9.00. |
|  | By default, *mode*=0, which uses vectorized functions where possible. |
|  | Set *mode* to 1 to request non-vectorized execution. This option is useful, e.g., when vectorized code does not support complex inputs as in atan2().  This may also improve speed when MatrixOP is called in a preemptive thread by preventing spawning additional threads. |
| <span class="table-cell-nowrap">/O</span> | Overwrites *destWave* if it already exists. |
| <span class="table-cell-nowrap">/P = *printMode*</span> | Controls printing of the result of the MatrixOp evaluation. /P was added in Igor Pro 8.00. |
|  | /P is ignored if MatrixOp is not running in the main thread. |
|  | *printMode* is a value between 0 and 2: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>No printing is done (default).</td></tr><tr><td>1:</td><td>Prints the result from evaluating *expression* in layer-by-layer order to the history area of the command window and stores the result in the destination wave.</td></tr><tr><td>2:</td><td>Prints the result from evaluating *expression* in layer-by-layer order to the history area of the command window but does create or store the resulting values in the destination wave. If the destination wave may already exist, you must include the /O flag, even though the destination wave is not changed by the operation.</td></tr></tbody></table>
|  | Use /P=1 if you want MatrixOp to work normally and then to print the destination wave. |
|  | Use /P=2 if you want MatrixOp to print its result without creating or affecting any waves. |
|  | Values are printed sequentially using 16-digit precision. Output is not formatted to represent rows and columns. |
|  | When the operation's result is a 3D or 4D wave, the results are printed on a layer-by-layer basis. |
|  | See ***MatrixOp Printing Examples*** below. |
| <span class="table-cell-nowrap">/S</span> | Preserves the dimension scaling, units and wave note of a pre-existing destination wave in a MatrixOp/O command. This flag has no effect if the destination wave is free. |
| <span class="table-cell-nowrap">/T = k</span> | Displays results in a table. *k* specifies the behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr></tbody></table>

### *Details* {#details}
MatrixOp has the general form:


```igor
MatrixOp [flags] destWave = expression
```

*destWave* specifies the wave created by MatrixOp or overwritten by MatrixOp/O.

From the command line, *destWave* can be a simple wave name, a partial data folder path or a full data folder path. In a user-defined function it can be a simple wave name or, if /O is present, a wave reference pointing to an existing wave.

*expression* is a mathematical expression that consists of one or more data tokens combined with the built-in MatrixOp functions and MatrixOp operators listed above. MatrixOp does not support the p, q, r, s, or x, y, z, t symbols that are used in waveform assignment statements.

Data tokens include waves, variables and literal numbers.

You can use any combination of data types for operands. In particular, you can mix real and complex types in *expression*. MatrixOp determines data types of inputs and the appropriate output data type at runtime without regard to any type declaration such as Wave/C.

See [Using MatrixOp](/igorpro/analysis/analysis.md#using-matrixop) for more information.

### *Trigonometric Transforms* {#trigonometric-transforms}
The trigonometrics transform functions were added in Igor Pro 8.00.

FST, FCT, FSST, FSCT, FSST2 and FSCT2 are implemented using INTEL MKL library functions. The transforms may automatically execute in multiple threads.

The equations for the definitions of the forward and reverse transforms follow Intel's documentation (see [https://software.intel.com/en-us/mkl-developer-reference-c-trigonometric-transforms-implemented](https://software.intel.com/en-us/mkl-developer-reference-c-trigonometric-transforms-implemented)).

In MatrixOP's implementation, all input and output arrays are zero based. This is illustrated by the following example for the staggared2 cosine:


```igor
Function DoStaggered2Cosine(inWave)
	Wave inWave

	Variable n = dimsize(inWave,0)	
	Make/O/N=(n)/D outStaggered2CosTransform=0
	Variable i, k, theSum, frontFactor=2/n
	
	for(k=1; k<=n; k+=1)
		theSum=0
		for(i=1; i<=n; i+=1)
			theSum += inWave[i-1] * cos((2*k-1) * (2*i-1) * pi/(4*n))
		endfor
		outStaggered2CosTransform[k-1] = frontFactor * theSum
	endfor
End
```

### *Examples* {#examples}
In addition to these examples, see [MatrixOp Optimization Examples](/igorpro/analysis/analysis.md#matrixop-optimization-examples).


```igor
// The following matrices are used in these examples
Make/O/N=(3,3) r1=x,r2=y

// Matrix addition and matrix multiplication by a scalar.
MatrixOp/O outWave=r1+r2-3*r1

// Using the matrix Identity function.
MatrixOp/O outWave=Identity(3) x r1

// Create a persisting identity matrix for another calculation:
MatrixOp/O id4=Identity(4)

// Using the Trace function.
MatrixOp/O outWave=(Trace(r1)*identity(3) x r1)-3*r1

// Using matrix inverse function Inv() with matrix multiplication.
MatrixOp/O outWave=Inv(r2) x r2

// Using the determinant function Det().
MatrixOp/O outWave=Det(r1)+Det(r2)
	
// Using the Transpose postfix operator.
MatrixOp/O outWave=r1^t+(r2-r1)^t-r2^t

// Using mix of real and complex data.
Variable/C complexVar=cmplx(1,2)
MatrixOp/O outWave=complexVar*r2 - Cmplx(2,4)*r1

// Hermitian transpose operator.
MatrixOp/O outWave=Trace(complexVar*r2)^h -Trace(cmplx(2,4)*r1)^h

// In-place operation + conversion to complex:
MatrixOp/O r1=r1*cmplx(1,2)

// Image filtering using 2D spatial filter filterWave:
MatrixOp/O filteredImage=IFFT(FFT(srcImage,2)*filterWave,3)
// Positive shift
Make/O w={0,1,2,3,4,5,6}
MatrixOp/O w=shiftVector(w,2,77)
Print w
// w[0]= {77,77,0,1,2,3,4}
// Negative shift
Make/O w={0,1,2,3,4,5,6}
MatrixOp/O w=shiftVector(w,(-2),77)
Print w
// w[0]= {2,3,4,5,6,77,77}

// Using kronProd function to generate Hadamard matrices
Function HadamardMatrix(int N)	// N must be >= 2
	Make/FREE/N=(2,2) H2={{1,1},{1,-1}}
	Duplicate/FREE H2, tmp
	int i
	for(i=2; i<N; i+=1)
		MatrixOP/O/FREE tmp=kronProd(H2,tmp)
	endfor
	Duplicate/O tmp, Hadamard
End

// bitReverseCol
Make/N=8 index = p
MatrixOP/O/P=1 out = bitReverseCol(index,0,0)   // Direct binary reversal
                                                // Prints: out = {0,4,2,6,1,5,3,7}
MatrixOP/O/P=1 out = bitReverseCol(index,0,1)   // Hadamard order
                                                // Prints: out = {0,4,6,2,3,7,5,1}
MatrixOP/O/P=1 out = bitReverseCol(index,0,2)   // Dyadic/Paley/Gray order
                                                // Prints: out = {0,1,3,2,6,7,5,4}
```

### *MatrixOp Printing Examples* {#matrixop-printing-examples}

```igor
// Print a single-valued result
Make/O/N=(10,5) m2D=(p+1)*(q+1)  
MatrixOP/O/P=1 aa=sum(m2D)
  aa={825}

// Print a real 2D result
Make/O/N=(1,4) ddd=enoise(3)
MatrixOp/O/P=1 aa=ddd
aa={-2.273916482925415,-2.327789783477783,1.286988377571106,-0.8658701777458191}

// Print higher-dimension result layer-by-layer
Make/O/N=(3,4,3) ddd=z+1
MatrixOP/O/P=1 aa=mean(ddd)
aa={1} 	// Each layer results in a 1x1 value
aa={2}
aa={3}
```

### *References* {#references}
syncCorrelation and asyncCorrelation:

Noda, I., Determination of Two-Dimensional Correlation Spectra Using the Hilbert Transform, *Applied Spectroscopy* *54*, 994-999, 2000.

ChirpZ:

Rabiner, L.R., and B. Gold, *The Theory and Application of Digital Signal Processing*, Prentice Hall, Englewood Cliffs, NJ, 1975.

### *See Also* {#see-also}
[Using MatrixOp](/igorpro/analysis/analysis.md#using-matrixop)

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines

[FastOp](/igorpro/commands/fastop.md)

### *Demos* {#demos}
[Open FFT Swapping Demo](#igor-pxp/Examples/Analysis/FFT__Swapping__Demo.pxp)

[Open Kalman Filter Example](#igor-pxp/Examples/Analysis/KalmanFilterExample.pxp)