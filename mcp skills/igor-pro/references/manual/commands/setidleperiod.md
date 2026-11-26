---
description: "The SetIdlePeriod operation changes and reports the period of Igor's main idle loop. The units of period are milliseconds."
slug: /commands/setidleperiod
---

<div className="command-signature">

## <strong>SetIdlePeriod</strong>  <em>period</em> {#setidleperiod}

</div>

The SetIdlePeriod operation changes and reports the period of Igor's main idle loop. The units of *period* are milliseconds. Setting *period* to zero does not change the period.

SetIdlePeriod was added in Igor Pro 8.00.

The default idle period is 20 milliseconds. Setting the period higher may make a slight improvement in the performance of some computation-heavy tasks.

Setting the period lower can make some parts of Igor more responsive. In particular, background tasks can be made to run more often, as the minimum period between runs of a background task is determined by Igor's idle period. Reducing the period too far increases the likelihood that your background task will run too long. Setting the period to very low values can make Igor very sluggish.

### *Output Variables* {#output-variables}
SetIdlePeriod creates the output variable V_value and sets it to the idle period before the call was made. You can use this value to restore the idle period after temporarily changing it. If *period* is zero, the idle period is not changed, but the current value is returned in V_value.

### *See Also* {#see-also}
[Background Tasks](/igorpro/advanced-topics.md#background-tasks)