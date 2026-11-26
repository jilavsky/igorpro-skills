---
description: "This operation is deprecated. The NeuralNetworkTrain operation trains a three-layer neural network."
slug: /commands/neuralnetworktrain
---

<div className="command-signature">

## <strong>NeuralNetworkTrain</strong>  [/Q/Z] [<em>keyword</em> = <em>value</em> ] ... {#neuralnetworktrain}

</div>

:::warning
This operation is deprecated.
:::

The NeuralNetworkTrain operation trains a three-layer neural network. The training produces two 2D waves that store the interconnection weights between the network neurodes.  Once you obtain the weights, you can use them with [NeuralNetworkRun](/igorpro/commands/neuralnetworkrun.md).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | Suppresses printing information in the History area. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Parameters* {#parameters}
*keyword* is one of the following:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">Input = *inWave*</span> | Specifies the input patterns for training. *inWave* is a 2D wave where each row corresponds to a single training event and each column corresponds to the input values. The number of rows in *inWave* (the number of training sets) and in the output wave must be equal. *inWave* must be single or double precision and all entries must be in the range [0,1]. |
| <span class="table-cell-nowrap">Iterations = *num*</span> | Specifies the number of iterations. The default is 10000. |
| <span class="table-cell-nowrap">MinError = *val*</span> | Terminates training when the total error drops below *val* (the default is 1e-8). The total error is normalized, and is defined as the sum of the squared errors divided by the number of training sets times outputs. |
| <span class="table-cell-nowrap">Momentum = *val*</span> | Specifies a coefficient used in the back-propagation algorithm. This coefficient adds to the change in a particular weight a contribution proportional to the error in a previous iteration. The default momentum is 0.075. |
| <span class="table-cell-nowrap">NHidden = *num*</span> | Specifies the number of hidden neurodes. You do not need to use the Structure keyword with NHidden because the network is completely specified by the training waves and NHidden. |
| <span class="table-cell-nowrap">NReport = *num*</span> | Specifies over how many iterations (default is 1000) to print the global RMS error to the history area. Ignored with /Q. |
| <span class="table-cell-nowrap">Output = *outWave*</span> | Specifies the expected outputs corresponding to the entries in the input wave. The number of rows in *outWave* (the number of training sets) and in the input wave must be equal. *outWave* must be single or double precision and all entries must be in the range [0,1]. |
| <span class="table-cell-nowrap">LearningRate = *val*</span> | Sets the network learning rate, which is used in the backpropagation calculation. The default is 0.15. |
| Restart | Allows specification of your own set of weights as the starting values. Use this to run the training and feed the output weights of one training session as the input for the next. |
| <span class="table-cell-nowrap">Structure = {*Ni, Nh, No*}</span> | Specifies the structure of the network. *Ni* is the number of neurodes at the input, *Nh* is the number of hidden neurodes, and *No* is the number of output neurodes. Structure is unnecessary when using NHidden is because the remaining numbers are determined by the sizes of the input and output waves. |
| <span class="table-cell-nowrap">WeightsWave1 = *w1*</span> | Specifies the weights for propagation from the first layer to the second. The 2D wave must be double precision and the dimensions must match the specified neurodes with the same numbers of rows and inputs and with matching numbers of columns and hidden neurodes. |
| <span class="table-cell-nowrap">WeightsWave2 = *w2*</span> | Specifies the weights for propagation from the second to the third layer. The 2D wave must be double precision and the dimensions must match the specified neurodes with the same numbers of rows and hidden neurodes and with matching numbers of columns and outputs. |

### *Details* {#details}
NeuralNetworkTrain is the first half of the implementation of a three-layer neural network in which both in inputs and outputs are taken as normalized quantities in the range [0,1]. Network training is based on back-propagation to iteratively minimize the error between the output and the expected output for any given training set. Training creates in two 2D waves that contain the interconnection weights between the neurodes. M_Weights1 contains the weights between the input layer and the hidden layer and M_Weights2 contains the weights between the hidden layer and the output layer. During the iteration stage, global error information can be printed in the history area.

The algorithm computes the output of the kth neurode by

$$
\displaystyle V_{k}=\left[1+\exp \left(-\sum_{i=1}^{n} w_{i} s_{i}\right)\right]^{-1},
$$

where w<sub>i</sub> is the weight corresponding to input i, s<sub>i</sub> is the signal corresponding to that input, and *n* is the number of inputs connected to the neurode.

The total error is defined as the sum (over all training sets and all outputs) of the squared differences between the network outputs and the expected values. The sum is normalized by the product of the number of training sets and the number of outputs. The history reports (see NReport parameter) the square root of the total error (RMS error). The square root of the error computed at the end of the last iteration is stored in the variable V_rms.

### *See Also* {#see-also}
[NeuralNetworkRun](/igorpro/commands/neuralnetworkrun.md)