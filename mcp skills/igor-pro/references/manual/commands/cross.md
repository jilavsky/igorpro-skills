---
description: "The Cross operation computes the cross products vectorA x vectorB and vectorA x (vectorB x vectorC). Each vector is a 1D real wave containing 3 rows."
slug: /commands/cross
---

<div className="command-signature">

## <strong>Cross</strong>  [ /DEST=<em>destWave</em>  /FREE /T /Z] <em>vectorA</em>, <em>vectorB</em>  [, <em>vectorC</em> ] {#cross}

</div>

The Cross operation computes the cross products *vectorA*  x *vectorB*  and *vectorA*  x (*vectorB* x *vectorC* ). Each vector is a 1D real wave containing 3 rows. Stores the result in the wave W_Cross in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Stores the cross product in the wave specified by *destWave* . |
|  | The destination wave is overwritten if it exists. |
|  | The destination wave must be different from the input waves. |
|  | The operation creates a wave reference for the destination wave if called in a user-defined function. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | If you omit /DEST, the operation stores the result in the wave W_Cross in the current data folder. |
|  | Requires Igor 7 or later. |
| <span class="table-cell-nowrap">/FREE</span> | When used with /DEST, the destination wave is created as a free wave. See [Free Waves](/igorpro/programming/programming.md#free-waves) for details on free waves. |
|  | /FREE is allowed in user-defined functions only. |
|  | Requires Igor 7 or later. |
| <span class="table-cell-nowrap">/T</span> | Stores output in a row instead of a column in W_Cross. |
| <span class="table-cell-nowrap">/Z</span> | Generates no errors if any inputs are unsuitable. |