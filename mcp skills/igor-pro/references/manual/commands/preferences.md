---
description: "The Preferences operation sets or displays the state of user preferences."
slug: /commands/preferences
---

<div className="command-signature">

## <strong>Preferences</strong>  [/Q] [<em>newPrefsState</em> ] {#preferences}

</div>

The Preferences operation sets or displays the state of user preferences.

User preferences affect the creation of new graphs, panels, tables, layouts, notebooks, procedure windows, and the command window. They also affect the appearance of waves appended to graphs and tables, and objects appended to layouts.

### *Parameters* {#parameters}
| If *newPrefsState* is present, it sets the state of user preferences as follows: |  |
| --- | --- |
|  |<table class="nested-table"><tbody><tr><td>*newPrefsState*&nbsp;=&nbsp;0:</td><td>Turns user preferences off (use factory defaults).</td></tr><tr><td>*newPrefsState*&nbsp;=&nbsp;1:</td><td>Turns user preferences on.</td></tr></tbody></table>

If *newPrefsState* is omitted, the state of user preferences is printed in the history area.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | Flag disables printing to the history. |

### *Details* {#details}
The Preferences operation sets the variable V_flag to the state of user preferences that were in effect ***before*** the Preferences command executed: 1 for on, 0 for off.

You can also set the state of Preferences with the Misc menu.

Under most circumstances we want procedures to be independent of preferences so that a particular procedure will do the same thing regardless of the state of preferences. To achieve this, preferences are automatically off when you initiate procedure execution. When execution is complete, the state of preferences is restored to what it was before.

If you want preferences to be in effect during procedure execution, you must turn it on with the Preferences operation.

If the preferences setting is changed by a procedure, the effect of the call is propagated down the calling chain. If a macro changes the preferences setting, that change is undone when the macro returns. If a function changes the preferences setting, the change persists after the function returns. However, even with a function, the changed preferences state does not persist when Igor regains control.

### *Examples* {#examples}

```igor
Function Test()
	Variable oldPrefState
	Preferences 1; oldPrefState=V_flag  // remember prefs setting
	Make wave0=x
	Display wave0                       // Display uses preferences
	Preferences oldPrefState            // put prefs back, like a macro would
End
```

### *See Also* {#see-also}
[Preferences](/igorpro/igor-basics/using-igor.md#preferences)