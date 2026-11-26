---
description: "The DateTime function returns number of seconds from 1/1/1904 to the current local date and time."
slug: /commands/datetime
---

<div className="command-signature">

## <strong>DateTime</strong> {#datetime}

</div>

The DateTime function returns number of seconds from 1/1/1904 to the current local date and time.

To get the UTC date and time, subtract Date2Secs(-1,-1,-1) from the value returned by DateTime.

Unlike most Igor functions, DateTime is used without parentheses.

### *Examples* {#examples}

```igor
Variable localNow = DateTime
```

### *See Also* {#see-also}
[Secs2Date](/igorpro/commands/secs2date.md), [Secs2Time](/igorpro/commands/secs2time.md), [time](/igorpro/commands/time.md)