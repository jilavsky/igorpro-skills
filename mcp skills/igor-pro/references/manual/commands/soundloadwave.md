---
description: "The SoundLoadWave operation loads sound data from the named file into a wave. Mono, stereo, surround-sound, and high-resolution sound formats are supported."
slug: /commands/soundloadwave
---

<div className="command-signature">

## <strong>SoundLoadWave</strong>  [ /I [= <em>filterStr</em>] /O /P=<em>pathName</em>  /Q /S=(<em>startT</em>,<em>endT</em> ) ] <em>waveName</em>  [ ,<em>fileNameStr</em>  ] {#soundloadwave}

</div>

The SoundLoadWave operation loads sound data from the named file into a wave. Mono, stereo, surround-sound, and high-resolution sound formats are supported.

The SoundLoadWave operation was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*waveName* is the name of the wave to load the sound into.

If *fileNameStr* is omitted or is "", SoundLoadWave displays an Open File dialog.

The file to be loaded is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If SoundLoadWave cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to choose the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I [ = *filterStr* ]</span> | Force interactive mode. Use optional filter string to limit allowable file extensions. See [Open File Dialog File Filters](/igorpro/programming/interacting-with-the-user.md#open-file-dialog-file-filters). |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing waves in case of a name conflict. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to load the file from. *pathName* is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:" or "C:\\\\Folder1\\". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details. |
| <span class="table-cell-nowrap">/Q</span> | Quiet: Doesn't print message to history area, and doesn't abort, if the sound cannot be loaded. V_Error is set to the returned error code, which will be zero if there was no error. |
| <span class="table-cell-nowrap">/S = (*startT*,*endT*)</span> | Load a subrange of the sound resource. *startT* and *endT* are in seconds, clipped to the duration of the loaded sound. |
| <span class="table-cell-nowrap">/TMOT = *timeOut*</span> | Aborts load if *timeOut* , in seconds, is exceeded. |

### *Details* {#details}
SoundLoadWave uses Qt framework calls. Note that some files cannot be loaded due to digital rights managment issues even though they can be played.

If *waveName* specifies a wave that does not exist, it is created. The wave is redimensioned to a wave type that maintains the numeric precision of the sound data. If the wave cannot be created or resized to fit the loaded data then SoundLoadWave returns an error.

If *waveName* does exist, the wave is overwritten only if the /O flag is specified. Without the /O flag SoundLoadWave returns an error.

Multi-channel audio is loaded into sequential columns of the destination wave.

SoundLoadWave uses the smallest Igor wave data type that preserves the number of bits in the audio. Igor doesn't have a 24-bit data type, so these values are stored in a 32-bit integer wave.

### *Output Variables* {#output-variables}
SoundLoadWave sets these output variables:


|  |  |
| --- | --- |
| V_flag | Set to 1 if a sound is loaded and fits into available memory, 0 otherwise. |
| V_Error | Set if /Q is specified, V_Error is set to a non-zero error code if something went wrong or to zero on success. Negative returned codes are system-dependent, positive are Igor-defined errors. |
|  | V_Error = 1 means there wasn't enough memory to load the (uncompressed) sound. |
| S_path | Set to the full file path of the loaded file, not including the file name. |
| S_fileName | Set to the name of the loaded file. |
| S_waveNames | Set to the name of loaded wave. |
| S_info | Information about the loaded sound. |

If the sound file exists, SoundLoadWave sets the string variable S_info to:


```igor
"FILE:nameOfFile;FORMAT:soundFileFormat;CHANNELS:numChannels;CHANNEL_LAYOUT:channelLayoutDescription;"
"CHANNEL_ORDER:channelsList;BITS:numBits;SAMPLES:numSamples;RATE:samplesPerSec;"
```

The *channelsList* value is a comma-separated list of channel names, always in English abbreviations, such as "L,R" or "L,R,C,LFE,Ls,Rs". The meaning of the abbrevations:


|  |  |
| --- | --- |
| **channelList Abbreviation** | **Channel or Speaker Names** |
| L | Front Left |
| R | Front Right |
| C | Front Center |
| LFE | Low Frequency Effects |
| Ls | Left Surround (Back Left) |
| Rs | Right Surround (Back Right) |
| Lc | Left Center (Front Left of Center) |
| Rc | Right Center (Front Right of Center) |
| Cs | Center Surround (Back Center) |
| Lsd | Left Surround Direct (Side Left) |
| Rsd | Right Surround Direct (Side Right) |
| Ts | Top Center Surround (Top Center) |
| Vhl | Vertical Height Left (Top Front Left) |
| Vhc | Vertical Height Center (Top Front Center) |
| Vhr | Vertical Height Right (Top Front Right) |
| Rls | Rear Left Surround (Top Back Left) |
| Rcs | Rear Center Surround (Top Back Center) |
| Rrs | Rear Right Surround (Top Back Right) |

### *Examples* {#examples}

```igor
// Display an Open File dialog and load the chosen file. 
// Use the file's name for the wave, overwrite any pre-existing wave, print information to history
SoundLoadWave/O myDestWave

// SoundLoadWave stores the following in S_Info and prints it to the history area of the command window
FILE:<file name>;FORMAT:MPEG Layer 3;CHANNELS:2;BITS:0;SAMPLES:524416;RATE:44100;

// Rename the wave to a cleaned up version of the file name
Rename myDestWave, $CleanupName(S_fileName,1)
```

### *See Also* {#see-also}
[SoundSaveWave](/igorpro/commands/soundsavewave.md), [PlaySound](/igorpro/commands/playsound.md)