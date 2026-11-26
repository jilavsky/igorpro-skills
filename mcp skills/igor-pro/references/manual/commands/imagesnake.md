---
description: "The ImageSnake operation creates or modifies an active contour/snake in the grayscale image srcWave."
slug: /commands/imagesnake
---

<div className="command-signature">

## <strong>ImageSnake</strong>  [<em>flags</em> ] <em>srcWave</em> {#imagesnake}

</div>

The ImageSnake operation creates or modifies an active contour/snake in the grayscale image *srcWave*.  The operation iterates to find the "lowest total energy" snake.  The energy is defined by a range of optional flags, each corresponding to an individual term in the total energy expression.  Iterations terminate by reaching the maximum number of iterations, when the snake does not move between iterations or when the user aborts the operation.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *alpha*</span> | Sets the coefficient of the energy term arising from the "tightness" of the snake. |
| <span class="table-cell-nowrap">/BETA = *beta*</span> | Sets the coefficient of the energy term corresponding to curvature of the snake.  A high value for *beta* makes the snake more rounded. |
| <span class="table-cell-nowrap">/DELT = *delta*</span> | Sets the coefficient of the repulsion energy.  A high value of *delta* keeps nonconsecutive snake points far from each other. |
| <span class="table-cell-nowrap">/EPS = *num*</span> | Sets the maximum number of vertices which are allowed to move in one iteration.  If the number of vertices which move during an iteration is smaller than *num* then iterations terminate. |
| <span class="table-cell-nowrap">/EXEF = *eta*</span> | Sets the coefficient of the optional external energy component.  By default this value is set to zero and there is no external energy contribution to the snakes energy.  Note, this component is referred to as "external" because it is completely up to the user to specify both its coefficient and the value associated with each pixel.  It should not be confused with what is called external snake energy in the literature, which usually applies to energy proportional to the gradient image (see /GAMM and /GRDI). |
| <span class="table-cell-nowrap">/EXEN = *wave*</span> | Specify a wave that contains energy values that will be added to the snakes energy calculation.  The wave must have the same dimensions as *srcWave* and must be single precision float.  Each pixel value corresponds to user defined energy which will be multiplied by the /EXEF coefficient and added to the sum which the snake minimizes.  Note that when /EXEF is set to zero this component is ignored.  An external energy wave may be useful, for example, if you want to attract the snake to the picture boundaries.  In that case you can set: |
|  | <code class="igor">Duplicate/O srcWave,extWave&#10;Redimension/S extWave&#10;Variable rows=DimSize(srcWave,0)-1&#10;Variable cols=DimSize(srcWave,1)-1&#10;extWave=(p==0 \|\| q==0 \|\| p==rows \|\| q==cols) ? 0:1</code> |
| <span class="table-cell-nowrap">/GAMM = *gamma*</span> | Sets the coefficient of the energy term corresponding to the gradient.  A high value of *gamma* makes the snake follow lines of high image gradient. |
| <span class="table-cell-nowrap">/GRDI = *gWave*</span> | Specify the gradient image.  This wave must have the same dimensions as *srcWave* and it must be single precision float.  The wave corresponds to the quantity abs(grad(gauss\*\**srcWave*)), where grad is the gradient operator and \*\* denotes convolution of the source wave with a Gaussian kernel.  It is best to run the operation the first time without specifying this wave.  When the operation executes, it creates the wave M_GradImage which can then be used in subsequent executions of this operation.  If you want to modify the wave to express some other form of energy that you want the operation to minimize, you should use the /EXEN and /EXEF flags. |
| <span class="table-cell-nowrap">/ITER = *iterations*</span> |  |
|  | Sets the maximum number of iterations.  Convergence can be achieved if the value specified by /EPS is met. You can also terminate the process earlier by pressing the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations). |
| <span class="table-cell-nowrap">/N = *snakePts*</span> | Specify the number of vertices in the snake or the number of snake points.  Note that if you are providing snake waves in /SX and /SY, you do not need to specify this flag.  If you do not specify this flag the default value is 40. |
| <span class="table-cell-nowrap">/SIG = *sigma*</span> | Sets the size of the Gaussian kernel that is used to convolve the input image when creating the gradient image.  Note that you do not need to use this flag if you provide a gradient image. *sigma* is 3 by default.  You can use larger odd integers for larger Gaussian kernels which would correspond to a stronger blur. |
| <span class="table-cell-nowrap">/STRT = *{ centerX, centerY, radius}*</span> |  |
|  | Sets the starting snake to be a circle with the given center and radius.  If you use this flag you should also provide the number of snake points using the /N flag. |
| <span class="table-cell-nowrap">/STEP = *pixels*</span> | Sets the maximum radius of search.  By default the radius of the search is 6 pixels and the search follows a clockwise pattern from radius of 1 pixel to maximum radius specified by this flag.  Note: the search radius should be smaller than the dimension of a typical feature in the image.  If the radius is larger the snake may encompass more than one object.  Larger radius is also less efficient because many of the pixels in that range would result in a snake that crosses itself and hence get rejected in the process. |
| <span class="table-cell-nowrap">/SX = *xSnake*</span> | Provide an X-wave for the starting snake.  You must also provide an appropriate Y-wave using /SY. |
| <span class="table-cell-nowrap">/SY = *ySnake*</span> | Provide a Y-Wave for the starting snake.  Must work in combination with /SX. |
| <span class="table-cell-nowrap">/UPDM = *mode*</span> | Sets the update mode using any combination of the following: |
|  |<table class="nested-table"><tbody><tr><td>**Value**</td><td>**Update**</td></tr><tr><td>0</td><td>Update will take place once when the operation terminates.</td></tr><tr><td>1</td><td>Update once at the end of every iteration.</td></tr><tr><td>2</td><td>Update once after every snake vertex moves.</td></tr><tr><td>4</td><td>Update once for every search position.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q</span> | Quiet mode; don't print information in the history. |
| <span class="table-cell-nowrap">/Z</span> | Don't report any errors. |

### *Details* {#details}
A snake is a two-dimensional, usually closed, path  drawn over an image.  The snake is described by a pair of XY waves consisting of N vertices (sometimes called "snake elements" or "snaksels").  In this implementation it is assumed that the snake is closed so that the last point in the snake is connected to the first.  Snakes are used in image segmentation, when you want to automatically select a contiguous portion of the plane based on some criteria.  Unlike the classic contours, snakes do not have to follow a constant level.  Their structure (or path) is found by associating the concept of energy with every snake configuration and attempting to find the configuration for which the associated energy is a minimum.  The search for a minimum energy configuration is usually time consuming and it strongly depends on the format of the energy function and the initial conditions (as defined by the starting snake).  The operation computes the energy as a sum of the following 5 terms:


1.  The coefficient alpha times a sum of absolute deviations from the average snake segment length.  This term tends to distribute the vertices of the snake at even intervals.


2.  The coefficient beta times a sum of energies associated with the curvature of the snake at each vertex.


3.  The coefficient gamma times a sum of energies computed from the negative magnitude of the gradient of a Gaussian kernel convolved with the image.  This term is usually referred to in the literature as the external energy and usually drives the snake to follow the direction of high image gradients.


4.  The coefficient delta times a repulsion energy.  Repulsion is computed as an inverse square law by adding contributions from all vertices except the two that are immediately connected to each vertex.  This energy term is designed to make sure that the snake does not fold itself into "valleys".


5.  The coefficient eta times the sum of values corresponding to the positions of all snake vertices in the wave you provide in /EXEN.

	The energy calculation skips all terms for which the coefficient is zero.  In addition there is a built-in scan which adds a very high penalty for configurations in which the snake crosses itself.