---
description: "The FakeData function puts fake data in the named wave, which must be single-precision float."
slug: /commands/fakedata
---

<div className="command-signature">

## <strong>FakeData</strong> (<em>waveName</em>) {#fakedata}

</div>

The FakeData function puts fake data in the named wave, which must be single-precision float. This is useful for testing things that require changing data before you have the source for the eventual real data. FakeData can be useful in a background task expression.

The FakeData function is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *Examples* {#examples}

```igor
Make/N=200 wave0; Display wave0
SetBackground FakeData(wave0)	// define background task
CtrlBackground period=60, start	// start background task

// observe the graph for a while
CtrlBackground stop	// stop the background task
```