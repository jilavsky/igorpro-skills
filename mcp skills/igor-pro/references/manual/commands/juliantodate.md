---
description: "The JulianToDate function returns a date string containing the day, month, and year. The input julianDay is truncated to an integer."
slug: /commands/juliantodate
---

<div className="command-signature">

## <strong>JulianToDate</strong> (<em>julianDay</em>, <em>format</em>) {#juliantodate}

</div>

The JulianToDate function returns a date string containing the day, month, and year.  The input *julianDay* is truncated to an integer.

### *Parameters* {#parameters}
*julianDay* is the Julian day to be converted.

*format* specifies the format of the returned date string.

| format | Date String |
| --- | --- |
| 0 | mm/dd/year |
| 1 | dd/mm/year |
| 2 | Tuesday November 15, 2002 |
| 3 | year mm dd |
| 4 | year/mm/dd |

### *See Also* {#see-also}
[dateToJulian](/igorpro/commands/datetojulian.md)

For more information about the Julian calendar see:

[http://www.tondering.dk/claus/calendar.html](http://www.tondering.dk/claus/calendar.html).