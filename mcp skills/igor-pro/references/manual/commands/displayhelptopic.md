---
description: "The DisplayHelpTopic operation displays a help topic as if a help link had been clicked in an Igor help file."
slug: /commands/displayhelptopic
---

<div className="command-signature">

## <strong>DisplayHelpTopic</strong>  [/K=<em>k</em>  /Z] <em>TopicString</em> {#displayhelptopic}

</div>

The DisplayHelpTopic operation displays a help topic as if a help link had been clicked in an Igor help file.

### *Parameters* {#parameters}
*TopicString*  is string expression containing the topic. It may be in one of three forms: \<topic name\>, \<subtopic name\>, \<topic name\>[\<subtopic name\>]. These forms are illustrated by the examples below.

Make sure that your topic string is specific in order to minimize the likelihood that Igor will find the topic in a help file other than the one you intended. To avoid this problem, it is best to use the \<topic name\>[\<subtopic name\>] form if possible.

### *Flags* {#flags}

|  |  |
| --- | --- |
| /K=*k* |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Leaves the help file open indefinitely (default). Use this if the help topic may be of interest in any experiment.</td></tr><tr><td>*k*&nbsp;=1:</td><td>If the found topic is in a closed help file, the help file closes with the current experiment. Use this if the help topic is tightly associated with the current experiment.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignore errors. If /Z is used, DisplayHelpTopic sets V_Flag to 0 if the help topic was found, or to a nonzero error code if it was not found. V_flag is set only when /Z is used. |

### *Details* {#details}
DisplayHelpTopic first searches for the specified topic in the open help files. If the topic is not found, it then searches all help files in the Igor Pro folder and subfolders.

If the topic is still not found, Igor then searches all help files in the current experiment's home folder, but not in subfolders. This puts a help file that is specific to a particular experiment in the experiment's home folder.

If the topic is still not found and if DisplayHelpTopic was called from an Igor procedure and if the procedure resides in a stand-alone file on disk (i.e., it is not in the built-in procedure window or in a packed procedure file), Igor then searches all help files in the procedure file's folder, but not in subfolders. This puts a help file that is specific to a particular set of procedures in the same folder as the procedure file.

If Igor finds the topic, it displays it. If Igor cannot find the topic, it displays an error message, unless /Z is used.

### *Examples* {#examples}

```igor
// This example uses the topic only.
DisplayHelpTopic "Modifying Traces"

// This example uses the subtopic only.
DisplayHelpTopic "Markers"

// This example uses the topic[subtopic] form.
DisplayHelpTopic "Modifying Traces[Markers]"
```

### *See Also* {#see-also}
[Igor Help Files](/igorpro/igor-basics/using-igor.md#igor-help-files)