---
description: "The AddMovieAudio operation adds audio samples to the audio track of the currently open movie."
slug: /commands/addmovieaudio
---

<div className="command-signature">

## <strong>AddMovieAudio</strong>  <em>soundWave</em> {#addmovieaudio}

</div>

The AddMovieAudio operation adds audio samples to the audio track of the currently open movie.

### *Parameters* {#parameters}
*soundWave* contains audio samples with an amplitude from -128 to +127 and with the same time scale as the prototype *soundWave*  used to open the movie.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Suppresses error reporting. If you use /Z, check the V_Flag output variable to see if the operation succeeded. |

### *Details* {#details}
You can create movies with 16-bit and stereo sound by providing a sound wave in the appropriate format. To specify 16-bit sound, the wave type must be signed 16-bit integer (/W flag in [Make](/igorpro/commands/make.md) or [Redimension](/igorpro/commands/redimension.md)). To specify stereo, use a wave with two columns (or any other number of channels as desired).

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| V_Flag | Set to 0 if the operation succeeded or to a non-zero error code. |
|  | V_Flag is set only if you use the /Z flag. |

### *See Also* {#see-also}
[Movies](/igorpro/advanced-topics.md#movies), [NewMovie](/igorpro/commands/newmovie.md), [AddMovieFrame](/igorpro/commands/addmovieframe.md)