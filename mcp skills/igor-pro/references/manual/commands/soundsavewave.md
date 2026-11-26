---
description: "The SoundSaveWave operation saves the named wave on disk primarily as a Microsoft WAVE sound file, or infrequently as an Audio Interchange File Format (AIFF-C)."
slug: /commands/soundsavewave
---

<div className="command-signature">

## <strong>SoundSaveWave</strong>  [ /BITS=<em>bits</em> /I /O /P=<em>pathName</em> /Q ] <em>typeStr</em>, <em>waveName</em> [ , <em>fileNameStr</em> ] {#soundsavewave}

</div>

The SoundSaveWave operation saves the named wave on disk primarily as a Microsoft WAVE sound file, or infrequently as an Audio Interchange File Format (AIFF-C).

### *Parameters* {#parameters}
*typeStr* must be either "AIFC" or "WAVE".

*fileNameStr* contains the name of the file in which the named wave is saved. If you omit *fileNameStr*, SoundSaveWave uses the wave name with the appropriate extension.

The file to be written is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If SoundSaveWave cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/BITS = *bits*</span> | Controls the number of bits used for each sound sample written to the file. |
|  | Use /BITS=24 with a 32-bit integer wave to save 24-bit sound data capable of representing values from -8,388,608 to +8,388,607. |
|  | If you omit /BITS or use /BITS=0, SoundSaveWave uses the wave's data type and size to determine how many bits are written for each sound sample. |
|  | The /BITS flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/I</span> | Presents a Save File dialog in which you can specify the file to be saved. |
| <span class="table-cell-nowrap">/O</span> | Overwrites the file if it already exists. |
|  | If you omit /O and the file exists, SoundSaveWave displays a Save File dialog. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to store the file in. *pathName* is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details. |
| <span class="table-cell-nowrap">/Q</span> | Suppresses the normal messages in the history area of the command window. At present nothing is written to the history even if /Q is omitted. |

### *Details* {#details}
The sound file is always an uncompressed AIFF-C or WAVE file, with as many channels as the wave contains columns.

The sound file format is determined by the wave's data type, *typeStr*, and the /BITS flag. Signed 8-, 16- and 24-bit integers are supported as are 32-bit and 64-bit floating point. When writing floating point waves, the wave data should be scaled to +/- 1.0 as full scale.

The SoundSaveWave operation was added in Igor Pro 7.00. 24-bit integer and 64-bit floating point support were added in Igor Pro 9.00.

### *Output Variables* {#output-variables}
SoundSaveWave sets these automatically created variables:


|  |  |
| --- | --- |
| V_flag | Set to 0 if the wave was successfully saved to the file or to a non-zero error code. |
| S_fileName | Set to the name of the saved file. |
| S_path | Set to the full path to the file's directory. |

### *Examples* {#examples}

```igor
// Create a simple sound (1000 Hz tone burst)
Make/O/N=10000 mySound                  // Single-precision wave, 10,000 values
SetScale/P x, 0, 1/8000, "" mySound     // 8000 Hz sampling frequency (1.25 seconds)
mySound= sin(2*pi*1000*x)               // 1000 Hz tone
Hanning mySound                         // Fade in and out

// Save it to a file, chosen from the Save File dialog
SoundSaveWave "AIFC", mySound, "my sound.aif"

// Create a floating point stereo frequency sweep
Make/O/N=(20000,2) stereoSineSoundF32   // 32-bit float data
SetScale/P x,0,1e-4,stereoSineSoundF32  // Set sample rate to 10KHz
stereoSineSoundF32= sin(2*Pi*(1000 + (1-2*q)*150*x)*x)
NewPath sound                           // Create a symbolic path via dialog
SoundSaveWave/P=sound/O "WAVE", stereoSineSoundF32
```

### *See Also* {#see-also}
[SoundLoadWave](/igorpro/commands/soundloadwave.md), [PlaySound](/igorpro/commands/playsound.md), [WaveType](/igorpro/commands/wavetype.md), [WaveInfo](/igorpro/commands/waveinfo.md)