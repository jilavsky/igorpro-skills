---
description: "The Secs2Time function returns a string containing a time. seconds is the number of seconds from 1/1/1904 to the time to be returned."
slug: /commands/secs2time
---

<div className="command-signature">

## <strong>Secs2Time</strong> (<em>seconds</em>, <em>format</em> [, <em>fracDigits</em> ]) {#secs2time}

</div>

The Secs2Time function returns a string containing a time.

### *Parameters* {#parameters}
*seconds* is the number of seconds from 1/1/1904 to the time to be returned.

*format* is a number between 0 and 5 which specifies how the time is to be constructed. It is interpreted as follows:

|  |  |
| --- | --- |
| 0: | Normal time, no seconds. |
| 1: | Normal time, with seconds. |
| 2: | Military time, no seconds. |
| 3: | Military time, with seconds and optional fractional seconds. |
| 4: | Elapsed time, no seconds. |
| 5: | Elapsed time, with seconds and optional fractional seconds. |


"Normal" formats (0 and 1) follow the preferred formatting of the short time format as set in the Regional and Language Options control panel.

"Military" means that the hour is a number from 0 to 23. Hours greater than 23 are wrapped.

"Elapsed" means that the hour is a number from -9999 to 9999. The result for hours outside that range is undefined.

The *fracDigits* parameter is optional and specifies the number of digits of fractional seconds. The default value is 0. The *fracDigits* parameter is ignored for format=0, 1, 2,and 4.

### *Examples* {#examples}

```igor
Print Secs2Time(DateTime,0)             // Uses "normal" format with no seconds (e.g., "1:07 PM").
Print Secs2Time(DateTime,1)             // Uses "normal" format with seconds (e.g., "1:07:28 PM").
Print Secs2Time(DateTime,2)             // Prints 13:07
Print Secs2Time(DateTime,3)             // Prints 13:07:29
Print Secs2Time(30*60*60+45*60+55,4)    // Prints 30:45
Print Secs2Time(30*60*60+45*60+55,5)    // Prints 30:45:55
```

### *See Also* {#see-also}
For a discussion of how Igor represents dates, see [Date/Time Waves](/igorpro/igor-basics/waves.md#date-time-waves).

[Secs2Date](/igorpro/commands/secs2date.md), [date](/igorpro/commands/date.md),  [date2secs](/igorpro/commands/date2secs.md), [DateTime](/igorpro/commands/datetime.md)