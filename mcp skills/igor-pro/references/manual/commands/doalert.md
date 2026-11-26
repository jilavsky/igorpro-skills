---
description: "The DoAlert operation displays an alert dialog and waits for user to click a button."
slug: /commands/doalert
---

<div className="command-signature">

## <strong>DoAlert</strong>  [/T=<em>titleStr</em>] <em>alertType</em>, <em>promptStr</em> {#doalert}

</div>

The DoAlert operation displays an alert dialog and waits for user to click a button.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *alertType* = |<table class="nested-table"><tbody><tr><td>0:</td><td>Dialog with an OK button.</td></tr><tr><td>1:</td><td>Dialog with Yes and No buttons.</td></tr><tr><td>2:</td><td>Dialog with Yes, No, and Cancel buttons.</td></tr></tbody></table>
| *promptStr* | Text displayed in the alert dialog. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/T = *titleStr*</span> | Changes the title of the dialog window from the default title. |

### *Details* {#details}

|  |  |
| --- | --- |
| DoAlert sets the special variable |  |
| V_flag = |<table class="nested-table"><tbody><tr><td>1:</td><td>Yes clicked.</td></tr><tr><td>2:</td><td>No clicked.</td></tr><tr><td>3:</td><td>Cancel clicked.</td></tr></tbody></table>

As of Igor 10, *promptStr* can contain a subset of HTML 4. For a description of the supported HTML 4 subset, see [https://doc.qt.io/qt-6/richtext-html-subset.html](https://doc.qt.io/qt-6/richtext-html-subset.html)

### *Example* {#example}

```igor
Macro example()
	String msg= "<p style=\"color:red;\">This is red text.</p>"
	msg += "<p>Click <a href=\"https://www.wavemetrics.com/\">here to buy Igor</a>.</p>"
	DoAlert/T="Buy Igor!" 0, msg
End
```