---
description: "The WaveType function returns the type of data stored in the wave. If selector = 1, WaveType returns 0 for a null wave, 1 if numeric, 2 if text, 3 if the wave…"
slug: /commands/wavetype
---

<div className="command-signature">

## <strong>WaveType</strong> (<em>waveName</em> [,<em>selector</em>]) {#wavetype}

</div>

The WaveType function returns the type of data stored in the wave.

If *selector* = 1, WaveType returns 0 for a null wave, 1 if numeric, 2 if text, 3 if the wave holds data folder references or 4 if the wave holds wave references.

If *selector* = 2, WaveType returns 0 for a null wave, 1 for a normal global wave or 2 for a free wave or a wave that is stored in a free data folder.

If *selector* = 3, WaveType returns 0 for a null wave reference or a global wave, 1 for a free wave (a wave that is not stored in any data folder) or 2 for a local wave (a wave that is stored in a free data folder hierarchy).

If *selector* is omitted or zero, the returned value for numeric waves is a combination of bit values shown in the following table.


| Type | Bit # | Hex Value |
| --- | --- | --- |
| complex | 0 | 1 |
| 32-bit float | 1 | 2 |
| 64-bit float | 2 | 4 |
| 8-bit integer | 3 | 8 |
| 16-bit integer | 4 | 10 |
| 32-bit integer | 5 | 20 |
| 64-bit integer | 7 | 80  (Requires Igor Pro 7 or later) |
| unsigned | 6 | 40 |

The unsigned bit is used only with the integer types while the complex bit can be used with any numeric type. Set only one of bits 1-5 or bit 7 as they are mutually exclusive. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

The returned value for non-numeric waves (text waves, wave-reference waves and data folder-reference waves) is 0.

### *Examples* {#examples}

```igor
Variable waveIsComplex = WaveType(wave) & 0x01
Variable waveIs32BitFloat = WaveType(wave) & 0x02
Variable waveIs64BitFloat = WaveType(wave) & 0x04
Variable waveIs8BitInteger = WaveType(wave) & 0x08
Variable waveIs16BitInteger = WaveType(wave) & 0x10
Variable waveIs32BitInteger = WaveType(wave) & 0x20
Variable waveIs64BitInteger = WaveType(wave) & 0x80
Variable waveIsUnsigned = WaveType(wave) & 0x40
```

### *See Also* {#see-also}
For concepts related to selector = 1 or 2, see [Free Waves](/igorpro/programming/programming.md#free-waves), [Wave Reference Waves](/igorpro/programming/programming.md#wave-reference-waves) and [Data Folder Reference Waves](/igorpro/programming/programming.md#data-folder-reference-waves).