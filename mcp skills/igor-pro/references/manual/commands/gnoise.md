---
description: "The gnoise function returns a random value drawn from a Gaussian distribution such that the standard deviation of an infinite number of such values would be…"
slug: /commands/gnoise
---

<div className="command-signature">

## <strong>gnoise</strong> (<em>num</em> [, <em>RNG</em>]) {#gnoise}

</div>

The gnoise function returns a random value drawn from a Gaussian distribution such that the standard deviation of an infinite number of such values would be *num*.

gnoise returns a complex result if *num* is complex or if it is used in a complex expression. See ***Use of gnoise With Complex Numbers*** below.

The random number generator is initialized using a seed derived from the system clock when Igor starts. This almost guarantees that you will never get the same sequence twice. If you want repeatable "random" numbers, use [SetRandomSeed](/igorpro/commands/setrandomseed.md).

The Gaussian distribution is achieved using a Box-Muller transformation of uniform random numbers.

The optional parameter *RNG* selects one of three pseudo-random number generators used to create the uniformly-distributed random numbers providing the input to the Box-Muller transformation.

If you omit the RNG parameter, gnoise uses RNG number 3, named "Xoshiro256\*\*". This random number generator was added in Igor Pro 9.00 and is recommended for all new code. In earlier versions of Igor, the default was 1 (Linear Congruential Generator).

The available random number generators are:


| RNG | Description |
| --- | --- |
| 1 | Linear Congruential Generator by L'Ecuyer with added Bayes-Durham shuffle. The algorithm is described in Numerical Recipes edition 2 as the function ran2(). This RNG has nearly 2<sup>32</sup> distinct values and the sequence of random numbers has a period in excess of 10<sup>18</sup>. |
|  | This RNG is provided for backward compatibility only. New code should use RNG=3 (Xoshiro256\*\*). |
| 2 | Mersenne Twister by Makoto Matsumoto and Takuji Nishimura. It is claimed to have better distribution properties and period of 2<sup>19937</sup>-1. See M. Matsumoto and T. Nishimura, "Mersenne Twister: A 623-dimensionally equidistributed uniform pseudorandom number generator", ACM Trans. on Modeling and Computer Simulation Vol. 8, No. 1, pp.3-30 1998. More information is available at |
|  | [http://en.wikipedia.org/wiki/Mersenne_twister](http://en.wikipedia.org/wiki/Mersenne_twister). |
|  | This RNG is provided for backward compatibility only. New code should use RNG=3 (Xoshiro256\*\*). |
| 3 | Xoshiro256\*\* by David Blackman and Sebastiano Vigna. It has a period of 2<sup>256</sup>-1, is 4 dimensionally equidistributed and passes all statistical tests at the time of writing. For technical details, see "Scrambled linear pseudorandom number generators", 2019 ([http://vigna.di.unimi.it/ftp/papers/ScrambledLinear.pdf](http://vigna.di.unimi.it/ftp/papers/ScrambledLinear.pdf)). |

### *Use of gnoise With Complex Numbers* {#use-of-gnoise-with-complex-numbers}
gnoise returns a complex result if *num* is complex or if it is used in a complex expression.


```igor
Function DemoGNoiseComplex()
	// enoise(rv) in a complex expression returns a complex result
	// and is equivalent to cmplx(gnoise(rv),gnoise(rv))
	Variable rv = 1	// A real variable
	SetRandomSeed 1
	Variable/C cv1 = gnoise(rv)	// Real parameter, complex result
	SetRandomSeed 1
	Variable/C cv2 = cmplx(gnoise(rv),gnoise(rv))	// Equivalent
	Print cv1, cv2
	
	// gnoise(cv) is equivalent to cmplx(gnoise(real(cv)),gnoise(imag(cv)))
	Variable/C cv = cmplx(1,1)	// A complex variable
	SetRandomSeed 1
	Variable/C cv3 = gnoise(cv)	// Complex parameter, complex result
	SetRandomSeed 1
	Variable/C cv4 = cmplx(gnoise(real(cv)),gnoise(imag(cv)))	// Equivalent
	Print cv3, cv4
End
```

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [enoise](/igorpro/commands/enoise.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)