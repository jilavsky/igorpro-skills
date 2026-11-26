---
description: "The date2secs function returns the number of seconds from midnight on 1/1/1904 to the specified date."
slug: /commands/date2secs
---

<div className="command-signature">

## <strong>date2secs</strong> (<em>year</em>, <em>month</em>, <em>day</em>) {#date2secs}

</div>

The date2secs function returns the number of seconds from midnight on 1/1/1904 to the specified date.

The month and day parameters are one-based, so these series start at one.

Date2Secs is limited to the range -32768-01-01 to 32767-12-31. For dates outside that range, it returns NaN. It also returns NaN if the year is 0 because Igor uses the Gregorian calendar in which there is no year 0.

If *year*, *month* and *day* are all -1 then date2secs returns the offset in seconds from the local time to the UTC (Universal Time Coordinate) time.

### *Examples* {#examples}

```igor
Print Secs2Date(date2secs(1993,3,15),1)	// Ides of March, 1993
```

Prints the following, depending on your system's date settings, in the history area:


```igor
  Monday, March 15, 1993
```

This next example sets the X scaling of a wave to 1 day per point, starting January 1, 1993:


```igor
Make/N=125 myData = 100 + gnoise(50)
SetScale/P x,date2secs(1993,1,1),24*60*60,"dat",myData
Display myData;ModifyGraph mode=5
```

### *See Also* {#see-also}
For further discussion of how Igor represents dates, see [Date/Time Waves](/igorpro/igor-basics/waves.md#date-time-waves).

[Secs2Date](/igorpro/commands/secs2date.md), [Secs2Time](/igorpro/commands/secs2time.md), [time](/igorpro/commands/time.md)