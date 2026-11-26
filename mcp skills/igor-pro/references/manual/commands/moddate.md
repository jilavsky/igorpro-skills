---
description: "The ModDate function returns the modification date/time of the wave. The returned value is a double precision Igor date/time value, which is the number of…"
slug: /commands/moddate
---

<div className="command-signature">

## <strong>ModDate</strong> (<em>waveName</em>) {#moddate}

</div>

The ModDate function returns the modification date/time of the wave.

### *Details* {#details}
The returned value is a double precision Igor date/time value, which is the number of seconds from 1/1/1904. It returns zero for waves created by versions of Igor prior to 1.2, for which no modification date/time is available.

### *See Also* {#see-also}
[WaveModCount](/igorpro/commands/wavemodcount.md), [Secs2Date](/igorpro/commands/secs2date.md), [Secs2Time](/igorpro/commands/secs2time.md)