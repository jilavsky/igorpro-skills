---
description: "ImageWindow multiplies srcWave by the specified window function. ImageWindow is useful in preparing an image for FFT analysis by reducing FFT artifacts…"
slug: /commands/imagewindow
---

<div className="command-signature">

## <strong>ImageWindow</strong>  [/I][/O][/P=<em>param</em> ] <em>method</em>  <em>srcWave</em> {#imagewindow}

</div>

ImageWindow multiplies *srcWave* by the specified window function. ImageWindow is useful in preparing an image for FFT analysis by reducing FFT artifacts produced at the image boundaries. By default, the operation saves the data in the wave M_WindowedImage in the current data folder.

ImageWindow is useful in preparing an image for FFT analysis by reducing FFT artifacts produced at the image boundaries.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave created by the operation. It is an error to specify the same wave as both *srcWave* and *destWave*. |
|  | When used in a function, the operation creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* (specified by /DEST) as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/I</span> | Creates only the output wave containing the windowing filter values that are used to multiply each pixel in *srcWave* . The source image is not filtered. |
| <span class="table-cell-nowrap">/O</span> | Overwrites the source image with the output image. If /O is not used, then the operation creates the M_WindowedImage wave containing the filtered source image. |
| <span class="table-cell-nowrap">/P = *param*</span> | Specifies the design parameter for the Kaiser window. |

### *Parameters* {#parameters}
*method* selects the type of windowing filter, which is one of the following:


|  |  |
| --- | --- |
| Hanning | $$ \displaystyle w(n)=\frac{1}{2}\left[1-\cos \left(\frac{2 \pi n}{L-1}\right)\right] \quad 0 \leq n \leq L-1 $$ |
| Hamming | $$ \displaystyle w(n)=0.54-0.46 \cos \left(\frac{2 \pi n}{L-1}\right) \quad 0 \leq n \leq L-1 $$ |
| Bartlett | $$ w(n)=\left\{\begin{array}{cc} \displaystyle \frac{2 n}{L-1} & 0 \leq n \leq \displaystyle \frac{L-1}{2} \\ \\ \displaystyle 2-\frac{2 n}{L-1} & \displaystyle \frac{L-1}{2} \leq n \leq L-1 \end{array}\right. $$ |
| Blackman | $$ \displaystyle w(n)=0.42-0.5 \cos \left(\frac{2 \pi n}{L-1}\right)+0.08 \cos \left(\frac{4 \pi n}{L-1}\right) \quad 0 \leq n \leq L-1 $$ |
| Kaiser | $$ \frac{I_{0}\left(\omega_{a} \sqrt{\left(\displaystyle \frac{L-1}{2}\right)^{2}-\displaystyle \left(n-\frac{L-1}{2}\right)^{2}}\right)}{\displaystyle I_{0}\left(\omega_{a}\left(\frac{L-1}{2}\right)\right)} \quad 0 \leq n \leq L-1 $$ |
|  | where I<sub>0</sub>{...} is the zeroth-order Bessel function of the first kind and ω<sub>a</sub> is the design parameter specified by /P=*param*. |
| KaiserBessel20: | *α* =2.0 |
| KaiserBessel25: | *α* =2.5 |
| KaiserBessel30: | *α* =3.0 |
|  | $$ w(n)=\frac{I_{0}\left(\pi \alpha \sqrt{1-\left(\displaystyle \frac{n}{L / 2}\right)^{2}}\right)}{I_{0}(\pi \alpha)} \quad 0 \leq\|n\| \leq \frac{L}{2} $$ |
|  | $$ \displaystyle I_{0}(x)=\sum_{k=0}^{\infty} \frac{\left(x^{2} / 4\right)^{k}}{(k!)^{2}}. $$ |

In the above equations, *L* is the number of columns or rows and *n* is the pixel column or row number.

### *Details* {#details}
The 1-dimensional window for each column is multiplied by the value of the corresponding row's window value. In other words, each point is multiplied by the both the row-oriented and column-oriented window value.

This means that all four edges of the image are decreased while the center remains at or near its original value. For example, applying the Bartlett window to an image whose values are all equal results in a trapezoidal pyramid of values:


|  |  |
| --- | --- |
|  | <img src="Images/ImageWindow/ImageWindow_0.png" width="100%"/> |

<img src="Images/ImageWindow/ImageWindow_1.png" width="100%"/>

The default output wave is created with the same data type as the source image. Therefore, if the source image is of type unsigned byte (/b/u) the result of using /I will be identically zero (except possibly for the middle-most pixel). If you keep in mind that you need to convert the source image to a wave type of single or double precision in order to perform the FFT, it is best if you convert your source image (e.g., [Redimension](/igorpro/commands/redimension.md)/S *srcImage*) before using the ImageWindow operation.

The windowed output is in the M_WindowedImage wave unless the source is overwritten using the /O flag.

The necessary normalization value (equals to the average squared window factor) is stored in V_value.

### *Examples* {#examples}
To see what one of the windowing filters looks like:


```igor
Make/N=(80,80) wShape		// Make a matrix
ImageWindow/I/O Blackman wShape		// Replace with windowing filter
Display;AppendImage wShape		// Display windowing filter
Make/N=2 xTrace={0,79},yTrace={39,39}	// Prepare for 1D section
AppendToGraph yTrace vs xTrace
ImageLineProfile srcWave=wShape, xWave=xTrace, yWave=yTrace
Display W_ImageLineProfile		// Display 1D section of filter
```

### *See Also* {#see-also}
[WindowFunction](/igorpro/commands/windowfunction.md) operation for information about 1D applications.

[Spectral Windowing](/igorpro/analysis/signal-processing.md#spectral-windowing). [Image Processing](/igorpro/analysis/image-processing.md) contains links to and descriptions of other image operations.

See [FFT](/igorpro/commands/fft.md) operation for other 1D windowing functions for use with FFTs.

[DSPPeriodogram](/igorpro/commands/dspperiodogram.md) uses the same window functions. See [Correlation](/igorpro/analysis/signal-processing.md#correlation).

[DPSS](/igorpro/commands/dpss.md)

### *References* {#references}
For further windowing information, see page 243 of William K. Pratt, *Digital Image Processing*, John Wiley, New York, 1991.