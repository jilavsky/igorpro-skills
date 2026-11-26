---
description: "The Secs2Date function returns a string containing a date. With format values 0, 1, and 2, the formatting of dates depends on operating system settings…"
slug: /commands/secs2date
---

<div className="command-signature">

## <strong>Secs2Date</strong> (<em>seconds</em>, <em>format</em> [, <em>sep</em> ]) {#secs2date}

</div>

The Secs2Date function returns a string containing a date.

With *format* values 0, 1, and 2, the formatting of dates depends on operating system settings entered in the Region control panel. These date formats do not work with dates before 0001-01-01 in which case Secs2Date returns an empty string.

If *format* is -1, the format is independent of operating system settings. The fixed-length format is "*day* /*month* /*year* (*dayOfWeekNum* )", where *dayOfWeekNum* is 1 for Sunday, 2 for Monday... and 7 for Saturday.

If *format* is -2, the format is YYYY-MM-DD.

The optional *sep* parameter affects format -2 only. If *sep* is omitted, the separator character is "-". Otherwise, *sep* specifies the separator string. An empty string results in no separator; you may use as many characters as you wish.

### *Parameters* {#parameters}
*seconds* is the number of seconds from 1904-01-01 to the date to be returned.

*seconds* is limited to the range -1094110934400 (-32768-01-01) to 973973807999 (32767-12-31). For *seconds* outside that range, Secs2Date returns an empty string.

*format* is a number between -2 and 2 which specifies how the date is to be constructed.

### *Examples* {#examples}

```igor
Print Secs2Date(DateTime,-2)        // 1993-03-14
Print Secs2Date(DateTime,-2,"/")    // 1993/03/14
Print Secs2Date(DateTime,-2,"---")  // 1993---03---14
Print Secs2Date(DateTime,-2,"")     // 19930314
Print Secs2Date(DateTime,-1)        // 15/03/1993 (2)
Print Secs2Date(DateTime,0)         // 3/15/93 (depends on system settings)
Print Secs2Date(DateTime,1)         // Monday, March 15, 1993 (depends on system settings)
Print Secs2Date(DateTime,2)         // Mon, Mar 15, 1993 (depends on system settings)
```

### *See Also* {#see-also}
For further discussion of how Igor represents dates, see [Date/Time Waves](/igorpro/igor-basics/waves.md#date-time-waves).

[date](/igorpro/commands/date.md),  [date2secs](/igorpro/commands/date2secs.md), [DateTime](/igorpro/commands/datetime.md)