---
description: "The PlaySound operation plays the audio samples in the named wave. The various sound output parameters -- number of samples, sample rate, number of channels…"
slug: /commands/playsound
---

<div className="command-signature overload">

## <strong>PlaySound</strong>  [/A [=<em>a</em> ]] [/BITS=<em>bits</em>] <em>soundWave</em> {#playsound}

</div>

<div className="command-signature overload">

## <strong>PlaySound</strong>  [/A [=<em>a</em> ]] [/BITS=<em>bits</em>] \\{<em>soundWave1</em> [ , <em>soundWave2</em>, <em>soundWaveN</em>...]\\} {#playsound}

</div>

<div className="command-signature">

## <strong>PlaySound</strong>  [/STOP] [/PAUS] [/GO] {#playsound}

</div>

The PlaySound operation plays the audio samples in the named wave. The various sound output parameters -- number of samples, sample rate, number of channels, and number of bits of resolution -- are determined by the corresponding parameters of the wave.


### *Flags* {#flags}

| Flag         | Description
| ------------ | -----------
| /A[=*a* ]    | Plays sounds asynchronously so that sounds will continue to play after the command itself has executed.
|              | /A=0: ::Same as no /A flag.
|              | /A=1: ::Plays sounds asynchronously; same as /A.
|              | /A=2: ::Stop playing any current sound before starting this one (if any).
|              | /A=3: ::Return with user abort error if output buffers are full (rather than waiting.) Use [GetRTError](/igorpro/commands/getrterror.md)(1) to detect and clear the error condition.
| /BITS=*bits* | Controls the number of bits used for each sound sample sent to the sound output hardware.
|              | Use /BITS=24 with a 32-bit integer wave for 24-bit sound data capable of representing values from -8,388,608 to +8,388,607.
|              | If you omit /BITS or use /BITS=0, PlaySound uses the wave's data type and size to determine how many bits are used for each sound sample.
|              | The /BITS flag was added in Igor Pro 9.00.
| /GO          | Restart any sound paused by /PAUS.
|              | The /GO flag was added in Igor Pro 10.02. 
| /PAUS        | Pause playback of any sound(s) queued or already playing with /A.
|              | The /PAUS flag was added in Igor Pro 10.02.
| /STOP        | Stop any sound(s) queued or already playing with /A.
|              | The /STOP flag was added in Igor Pro 10.01.

### *Details* {#details}
The wave's time per point, as determined by its X scaling, must be a valid sampling interval corresponding to a sampling frequency of 5,000 to 192,000 Hz. A value of 1/44100 (CD standard) is typical.

Sound waves can be 8, 16, or 32-bit signed integer waves, or single-precision or double-precision floating point waves:

- 8-bit integer waves support a sample range of -128 to +127.
- 16-bit integer waves support a sample range of -32768 to +32767.
- 32-bit integer waves are used to hold both 24-bit and 32-bit audio.

    Use /BITS=24 to tell PlaySound that a 32-bit wave contains 24-bit values in the range of -8,388,608
 to +8,388,607 instead of 32-bit values that have a range of -2,147,483,648
 to +2,147,483,647.
- floating point waves support a range of -1 to +1.

Do not use complex waves with PlaySound.

To play a stereo sound, either:

- provide one two-column wave with the left channel in column 0.
- provide two 1D waves in a list inside braces.

PlaySound will attempt to play as many channels as there are columns in the two-dimensional wave (or as many 1D waves are listed inside braces), limited only by the smaller of the operating system's channel limit and PlaySound's limit of 64 channels or 20 waves.

If the /A flag is provided then the sound is played asynchronously (i.e., the command returns before the sound is finished). Multiple sounds can be queued with /A to play after the previous sound finishes playing.

If another PlaySound command without /A is issued before queued sound(s) are finished then the new command will wait until the last sound finishes playing.

It is OK to kill the sound wave immediately after PlaySound returns even if the /A flag is used.

### *Details for Igor 10.01+* {#details-for-igor-10-01}

Information about the sound output device's playback of the sound is returned in S_Info.

PlaySound/STOP can be used to stop playing any sounds currently playing and any others queued up after it.

> **Note**: Earlier versions of Igor lacking this feature can specify a very brief sound with /A=2 to accomplish the same thing.

When the audio samples have more channels than are supported by the audio output device, PlaySound mixes the additional audio channels into the available device channels using the ITU-R BS.775 coefficients while presuming that the channels use the standard WAVEFORMATEXTENSIBLE channel layout:

| Wave Column | Speaker Channel
| ----------- | --------------------
| 0           | Front Left (FL)
| 1           | Front Right (FR)
| 2           | Front Center (FC, 3)
| 3           | Subwoofer (LFE, 3.1)
| 4           | Back Left (BL, 5.1)
| 5           | Back Right (BR, 5.1)
| 6           | Side Left (SL, 7.1)
| 7           | Side Right (SR, 7.1)

Igor Pro 10.01 now uses the **Windows Audio Session API (WASAPI)** to play sounds, replacing the older waveOut API (part of the Windows Multimedia (winmm.dll) library, dating back to Windows 3.1).

WASAPI is the low-level audio interface built into Windows Vista and later that gives applications direct, low-latency access to the sound hardware through the Windows audio engine.

When you call PlaySound, Igor 10.01 opens a *shared-mode WASAPI session* with the default Windows audio output device - the same device you have selected in Windows Sound settings (typically your speakers or headphones). "Shared mode" means the Windows audio engine mixes Igor's audio with audio from other applications, so you do not need to close other programs or hold an exclusive lock on the hardware.

Igor keeps this WASAPI session open between PlaySound calls so that successive sounds can be queued and played back-to-back without a gap. The session is closed automatically after the audio device has been idle for a short period, or when you call `PlaySound/STOP`.

When the audio device's supported sampling rate differs from the audio wave's sampling rate, PlaySound will resample the audio to the device's rate; either by upsampling (interpolating) or by downsampling (with FIR lowpass filtering).

This rate conversion is evidenced by a difference in the number of audio "frames" in the wave (rows) and the number of frames rendered. For example, a 1000-row (frames) audio wave sampled at 44100 Hz and played through an audio device with a 48000 Hz sampling rate will render more than 1000 frames: 1000 * 48000 / 44100 = 1088.44. In actuality, PlaySound renders 1089 frames.

PlaySound returns information about the sound output device's playback state in `S_Info`. This keyword-packed information string consists of a sequence of sections with the following form: *keyword*:*value*;

You can pick a value out of a keyword-packed string using the [NumberByKey](/igorpro/commands/numberbykey.md) function. Here are the keywords for `S_Info`:

| Keyword                   | Value        | Description
| ------------------------- | ------------ | -----------
| `PlaySoundDeviceIsOpen`   | 0 or 1       | Whether the WASAPI audio device is currently open and the render thread is active.
| `AudioDeviceRunning`      | 0 or 1       | Whether the audio device is currently running.
| `RequestedChannels`       | integer      | Number of audio channels requested by the most recent `PlaySound` call (e.g., 1 = mono, 2 = stereo).
| `DeviceChannels`          | integer      | Number of channels the WASAPI device was opened with. May differ from `RequestedChannels` if the device only supports stereo. 0 when the device is closed.
| `RequestedRate`           | integer (Hz) | Sample rate requested by `PlaySound` (derived from the source sound wave's X scaling). 0 when the device is closed.
| `DeviceRate`              | integer (Hz) | Sample rate at which the WASAPI device is actually rendering audio. 0 when the device is closed.
| `ResampleRatio`           | float        | Ratio of device sample rate to source sample rate (`DeviceRate / RequestedRate`). 1.0 means no resampling; >1.0 means the source is being upsampled.
| `TotalFramesQueued`       | uint64       | Cumulative count of audio frames written to the queue since the device was last opened (or counters last reset). Incremented by the caller thread each time audio data is pushed.
| `FramesRendered`          | uint64       | Cumulative count of audio frames consumed from the queue by the render thread and delivered to WASAPI since the device was last opened (or counters last reset).
| `FramesQueuedNow`         | uint64       | Frames currently pending in the queue (`TotalFramesQueued - FramesRendered`). Represents audio yet to be played.
| `FramesPerRingBufferNode` | uint32       | Fixed capacity (in frames) of each buffer node. This is a compile-time constant.
| `DeviceIdleCount`         | integer      | Number of consecutive render-thread wake-ups where the queue was empty and silence was written. Resets to 0 each time real audio is queued. Used internally to trigger auto-close of the device after a period of inactivity.

### *Examples* {#examples}

```igor
Make/B/O/N=1000 sineSound           // 8 bit samples, 0.1 seconds worth
SetScale/P x,0,1e-4,"s",sineSound   // Set sample rate to 10 kHz
sineSound= 127*sin(2*Pi*1000*x)     // Create 1 kHz sinewave tone
PlaySound sineSound
```

The following example will create a rising pitch in the left channel and a falling pitch in the right channel:

```igor
Make/W/O/N=(20000,2) stereoSineSound        // 16 bit data, 2 seconds worth
SetScale/P x,0,1e-4,"s",stereoSineSound     // Set sample rate to 10 kHz
stereoSineSound= 30000*sin(2*Pi*(1000 + (1-2*q)*150*x)*x)
PlaySound/A stereoSineSound                 // 16 bit, asynchronous
```

Multichannel sounds as in the previous example but from multiple 1D waves:

```igor
Make/W/O/N=20000 stereoSineSoundL,stereoSineSoundR          // 16 bit data, 2 seconds worth
SetScale/P x,0,1e-4,"s",stereoSineSoundL,stereoSineSoundR   // Set sample rate to 10 kHz
stereoSineSoundL= 30000*sin(2*Pi*(1000 + 150*x)*x)          // rising pitch in left
stereoSineSoundR= 30000*sin(2*Pi*(1000 - 150*x)*x)          // falling in right
PlaySound/A {stereoSineSoundL,stereoSineSoundR}             // two 1D waves
```

Example starting a long duration sound asynchronously and stopping playback before finished (requires Igor 10.01+):

```igor
Variable fs = 8000      // Sampling rate 8 kHz
Variable n = 10 * fs    // 10 seconds worth
Make/B/O/N=(n) sound10  // 8 bit data
SetScale/P x, 0, 1/fs, "s", sound10 // Set sample rate to 8 kHz
// Sweep 0->1000 Hz for first half, then 1000->0 Hz for second half
Variable half = n / 2
sound10[0,half-1] = 127*sin(Pi*fs*x*p/n/4)
sound10[half,n-1] = -sound10[n-p-1]
PlaySound sound10       // Play entire sound and wait for it to complete
Say "Done"
PlaySound/A sound10     // Begin playing and immediately return
Sleep/S 5               // Pretend to do other work while the sound plays
PlaySound/STOP          // Play approximately the first half of the sound
Say "Done"
```

### *See Also* {#see-also}

[SoundLoadWave](/igorpro/commands/soundloadwave.md), [SoundSaveWave](/igorpro/commands/soundsavewave.md), [Say](/igorpro/commands/say.md)

[https://learn.microsoft.com/en-us/windows/win32/coreaudio/wasapi](https://learn.microsoft.com/en-us/windows/win32/coreaudio/wasapi)