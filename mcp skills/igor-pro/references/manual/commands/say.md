---
description: "The Say operation speaks the text in sayThisStr with the default voice and speech settings, unless the speech settings are modified by the flags and parameters."
slug: /commands/say
---

<div className="command-signature">

## <strong>Say</strong>  [/A[= <em>async</em>] /PTCH=<em>pitch</em> /RATE=<em>rate</em> /VCE=<em>voiceStr</em> /VOL=<em>volume</em> /XML[= <em>isXML</em>] ] [ <em>sayThisStr</em> ] {#say}

</div>

The Say operation speaks the text in *sayThisStr* with the default voice and speech settings, unless the speech settings are modified by the flags and parameters.

The operation waits until the speaking completes before proceeding to the next command unless /A is set, in which case the command returns immediately after starting to speak the text. At present there is no way to interrupt asynchronous speech.

The Say operation was added for Igor Pro 10.

### *Parameters* {#parameters}
*sayThisStr* is text that is spoken. It is optional because you can use Say without any parameters to get the list of available voices in S_Voices.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A[ = *async* ]</span> | Asynchronous speech. /A or /A=1 starts speaking the text and the operation, then immediately returns. Otherwise the operation waits unitl all of the text is spoken. |
|  | <div><Admonition type="note"><p>When /A is used, S_voice will not return the chosen voice, only the default voice.</p></Admonition></div> |
| <span class="table-cell-nowrap">/PTCH = *pitch*</span> | *pitch* is an integer between -10 and +10, which represents a change in pitch from the default (*pitch* = 0). Values outside of this range are clipped to be within the range. |
| <span class="table-cell-nowrap">/RATE = *rate*</span> | *rate* is an integer between -10 and +10, which represents a change in the rate at which words are spoken from the default (*pitch* = 0). Positive values speak words more quickly. Values outside of this range are clipped to be within the range. |
| <span class="table-cell-nowrap">/VCE = *voiceStr*</span> | *voiceStr* selects one of the available SAPI[1] voices. *voiceStr* can be one of the values listed in the S_voices Output Variables (see below), or a partial match to the voice. |
|  | For example, *voiceStr* can be "david" to select the voice listed as "Microsoft David Desktop - English (United States)". |
|  | The voice which is selected by *voiceStr* (or the default voice) is returned in the S_voice Output Variable. |
| <span class="table-cell-nowrap">/VOL = *volume*</span> | *volume* is an integer between 0 and 100, which represents a percentage of maximum loudness. The default value is 100. If your computer's speaker volume slider is set to 50% of it's maximum, volume=100 will speak at that 50% volume; it will not be louder. |
| <span class="table-cell-nowrap">/XML[ = *isXML*]</span> | /XML or /XML=1 enables embedded XML SAPI commands to modify the spoken words. The default is /XML=0 unless /PTCH is specified, in which case XML is always enabled (the only way to change the pitch is to insert XML \<pitch\> text). |
|  | See SAPI TTS XML below. |
|  |<table class="nested-table"><tbody><tr><td>/XML=0:</td><td>Same as no /XML at all.</td></tr><tr><td>/XML=1:</td><td>Same as /XML alone.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z[ = *z*]</span> | /Z or /Z=1 prevents procedure execution from aborting if there is an error. Use /Z if you want to handle this case in your procedures, rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all. This is the default.</td></tr><tr><td>/Z=1:</td><td>Same as /Z alone.</td></tr></tbody></table>

### *SAPI TTS XML* {#sapi-tts-xml}
SAPI is Microsoft's Speech Application Programming Interface for speech recognition and speech synthesis.

SAPI Text-To-Speech can speak plain text and also XML-markup text to control voice, language, pitch, reading rate, and volume, as well as inserting silence:


|  |  |
| --- | --- |
| \<voice\> | Select a voice (e.g., \<voice required='Gender=Female'\>). |
| \<lang\> | Select a voice by language (e.g., \<lang langid='409'\>). |
|  | langid = 409 is US English, 411 is Japanese. |
| \<pitch\> | Adjusts pitch levels (e.g., \<pitch middle='-10'/\>). |
| \<rate\> | Controls speech speed (e.g., \<rate speed='-20'/\>). |
| \<volume\> | Modifies loudness (e.g., \<volume level='80'/\>). |
| \<spell\> | Forces spelling out words (e.g., \<spell\>hello\</spell\>). |
| \<pron\> | Specifies phonetic pronunciation (e.g., \<pron sym='HH EH L OW'/\>hello\</pron\>). |
| \<silence\> | Inserts pauses (e.g., \<silence msec='500'/\>). |

### *Output Variables* {#output-variables}
The Say operation sets these output variables:


|  |  |
| --- | --- |
| V_flag | Set to an error code, 0 otherwise. |
| S_voice | The voice used to speak the text. |
| S_voices | A semicolon-separated list of voice names available to the SAPI system. OneCore voices are not listed here unless the registry is edited to refer to them. |

### *Examples* {#examples}

```igor
// Simplest useful example
Say "The job is done!"

// Print a list of available voices and the current default voice
Say; Print S_voices; Print S_voice
Microsoft David Desktop - English (United States);Microsoft Zira Desktop - English (United States);Microsoft Haruka Desktop - Japanese;
Microsoft David Desktop - English (United States)

// Speak with the Zira voice (Zira is a female voice) and verify the chosen voice
Say/VCE="zira" "Hello, my name is Zira"; Print S_voice
Microsoft Zira Desktop - English (United States)

// Speak with a higher or lower-pitched voice, asynchronously
Say/A/PTCH=10 "this is a higher pitch than normal"
Say/A/PTCH=-10 "this is a lower pitch than normal"

// Speak slower or faster than normal
Say/RATE=-5 "this is slower than normal"
Say/RATE=5 "this is faster than normal"

// Speak more quietly than normal
Say/VOL=50 "this is quieter than normal"
Say/VOL=100 "this is maximum loudness"

// Use SAPI XML to spell out a word, insert silence.
Say/XML "Spell this <spell>word</spell> and pause <silence msec='500'/> and continue on."

// Use SAPI XML to choose a female voice. Note that the S_voice value does not reflect the matching voice.
Say/XML "<voice required='Gender=Female'>This is spoken with a female's voice.</voice>"; Print S_Voice
Microsoft David Desktop - English (United States)

// Use SAPI XML to choose a Japanese voice using <voice> instead of using /VCE
String str= "<voice required='Language=411'>\r"
str += "A Japanese voice should speak this: 日本語スタートガイド\r"
str += "</voice>\r"
Say/XML str

// Use SAPI XML to choose an English voice using <lang>
String str= "<lang langid='409'>\r"
str += "A U.S. English voice should speak this.\r"
str += "</lang>\r"
Say/XML str
```

### *References* {#references}
*XML TTS Tutorial (SAPI 5.3):*

[https://learn.microsoft.com/en-us/previous-versions/windows/desktop/ms717077(v=vs.85)](https://learn.microsoft.com/en-us/previous-versions/windows/desktop/ms717077(v=vs.85))

### *See Also* {#see-also}
[PlaySound](/igorpro/commands/playsound.md)