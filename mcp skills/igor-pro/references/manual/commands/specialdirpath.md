---
description: "The SpecialDirPath function returns a full path to a file system directory specified by dirIDStr and domain."
slug: /commands/specialdirpath
---

<div className="command-signature">

## <strong>SpecialDirPath</strong> (<em>dirIDStr</em>, <em>domain</em>, <em>flags</em>, <em>createDir</em>) {#specialdirpath}

</div>

The SpecialDirPath function returns a full path to a file system directory specified by *dirIDStr* and *domain*. It provides a programmer with a way to access directories of special interest, such as the preferences directory and the desktop directory.

The path returned always ends with a separator character which may be a colon, backslash or forward slash depending on the operating system and the *flags* parameter.

SpecialDirPath depends on operating system behavior. The exact path returned depends on the locale, the operating system, the specific installation, the current user and possibly other factors.

### *Parameters* {#parameters}
*dirIDStr* is one of the following strings:


|  |  |
| --- | --- |
| "Packages" | A place for advanced Igor programmers to put preferences for their procedure packages. |
| "Documents" | OS-defined place for users to put documents. |
| "Preferences" | OS-defined place for applications to put preferences. |
| "Desktop" | The desktop. |
| "Temporary" | OS-defined place for applications to put temporary files. |
| "Igor Application" | The Igor installation folder. This is typically: |
|  | `C:\Program Files\WaveMetrics\Igor Pro X Folder` |
|  | where "X" is the major version number. |
|  | Use only with domain=0 (the current user). |
| "Igor Executable" | The folder containing the current Igor executable. |
|  | Use only with domain=0 (the current user). |
|  | Requires Igor Pro 7.00 or later. |
| "Igor Preferences" | The folder in which Igor's own preference files are stored. |
| "Igor Pro User Files" | A guaranteed-writable folder for the user to store their own Igor files, and to activate extensions, help, and procedure files by creating shortcuts in the appropriate subfolders. Use only with *domain* = 0 (the current user). |
|  | This is the folder opened using the Show Igor Pro User Files menu item in the Help menu. |
| "Igor Diagnostics" | Location where crash reports and other diagnostics for Igor are saved. This directory is currently created only when Igor needs to write to it, so if *createDir* is set to 0, it is possible that the directory will not exist. |

Requires Igor Pro 10.00 or later.

*domain* permits discriminating between, for example, the preferences folder for all users versus the preferences folder for the current user. It is supported only for certain *dirIDStrs*. It is one of the following:

|  |  |
| --- | --- |
| 0: | The current user (recommended value for most purposes) |
| 1: | All users (may generate an error or return the same path as 0) |
| 2: | System (may generate an error or return the same path as 1) |

*flags* a bitwise parameter:


|  |  |
| --- | --- |
| Bit 0: | If set, the returned path is Windows-style. If cleared, the returned path is a Macintosh-style path regardless of the current platform. In most cases you should set this bit to zero since Igor accepts Macintosh-style paths on all operating systems. You must set this bit to one if you are going to pass the path to an external script. |

All other bits are reserved and must be set to zero.

See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

*createDir* is 1 if you want the directory to be created if it does not exist or 0 if you do not want it to be created. This flag will not work if the current user does not have sufficient privileges to create the specified directory. In almost all cases it is not needed, you can't count on it, and you should pass 0.

### *Details* {#details}
The *domain* parameter has no effect in most cases. In almost all cases you should pass 0 (current user) for this parameter. For values other than 0, SpecialDirPath might return an error which you must be prepared to handle.

In the event of an error, SpecialDirPath returns an empty string ("") and sets a runtime error code. You can check for an error like this:


```igor
String fullPath = SpecialDirPath("Packages", 0, 0, 0)
if (stringIsNull(fullpath))
	Print "SpecialDirPath returned error."
else
	Print fullPath
endif
```

Here is sample output from SpecialDirPath("Packages", 0, 0, 0):

```
C:Users:<user>:AppData:Roaming:WaveMetrics:Igor Pro X:Packages:
```

where *\<user\>* is the current user and "X" is the major version number.

### *Example* {#example}
For an example using SpecialDirPath, see [Saving Package Preferences](/igorpro/advanced-topics.md#saving-package-preferences).