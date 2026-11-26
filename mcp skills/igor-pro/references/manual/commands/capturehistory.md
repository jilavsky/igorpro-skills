---
description: "The CaptureHistory function returns a string containing text from the history area of the command window since a matching call to the CaptureHistoryStart…"
slug: /commands/capturehistory
---

<div className="command-signature">

## <strong>CaptureHistory</strong> (<em>refnum</em>, <em>stopCapturing</em>) {#capturehistory}

</div>

The CaptureHistory function returns a string containing text from the history area of the command window since a matching call to the [CaptureHistoryStart](/igorpro/commands/capturehistorystart.md) function.

### *Parameters* {#parameters}
*refnum* is a number returned from a call to CaptureHistoryStart. It identifies the starting point in the history for the returned string.

Set *stopCapturing* to nonzero to indicate that no more history should be captured for the given refnum. Subsequent calls to CaptureHistory with the same *refnum* will result in an error.

Set *stopCapturing* to zero to retrieve history text captured so far. Further calls to CaptureHistory with the same reference number will return this text, plus any additional history text added subsequently.

### *Details* {#details}
You can have multiple captures active at one time. Each call to CaptureHistoryStart will return a unique reference number identifying a start point in the history. The capture corresponding to each reference number can be terminated at any time, regardless of the order of the CaptureHistoryStart calls.