---
description: "The SetWaveLock operation locks a wave or waves and protects them against modification."
slug: /commands/setwavelock
---

<div className="command-signature">

## <strong>SetWaveLock</strong>  <em>lockVal</em>, <em>waveList</em> {#setwavelock}

</div>

The SetWaveLock operation locks a wave or waves and protects them against modification. Such protection is not absolute, but it should catch most common attempts to change or kill a wave.

### *Parameters* {#parameters}
*lockVal* can be 0, to unlock, or 1, to lock the wave(s).

*waveList* is a list of waves or it can be allinCDF to act on all waves in the current data folder.

### *See Also* {#see-also}
[WaveInfo](/igorpro/commands/waveinfo.md) to check if a wave is locked.