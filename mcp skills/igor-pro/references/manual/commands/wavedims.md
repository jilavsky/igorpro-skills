---
description: "The WaveDims function returns the number of dimensions used by the wave."
slug: /commands/wavedims
---

<div className="command-signature">

## <strong>WaveDims</strong> (<em>wave</em>) {#wavedims}

</div>

The WaveDims function returns the number of dimensions used by the wave.

Returns zero if wave reference is null. See [WaveExists](/igorpro/commands/waveexists.md) for a discussion of null wave references.

Also returns zero if wave has zero rows. A matrix will return 2.