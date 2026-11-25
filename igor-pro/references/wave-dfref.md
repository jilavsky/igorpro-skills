# Igor Pro — WAVE and DFREF Reference Syntax

This document covers the reference system for waves, global variables, strings,
and data folders. These are the areas where AI-generated Igor code most commonly
contains subtle errors. Read this before generating any code involving waves
passed as parameters, data folder navigation, or free waves.

Official reference: https://docs.wavemetrics.com/igorpro/programming/programming

---

## 1. The Core Distinction: Wave vs. WAVE

Igor has two completely different things that look similar:

- **A wave** — an array of data stored in a data folder (a global object)
- **A WAVE reference** — a local variable inside a function that *points to* a wave

You never operate on a wave directly by name inside a function. You always
declare a WAVE reference first, then use that reference.

```igor
// WRONG — this does not work inside a function:
Function BadExample()
    myWave = myWave * 2       // Error: myWave is not declared
End

// CORRECT:
Function GoodExample()
    WAVE myWave               // declare reference to wave in current data folder
    myWave = myWave * 2       // now valid
End
```

---

## 2. WAVE Reference Declarations

### Basic forms

```igor
WAVE w                // reference to a real numeric wave
WAVE/C w              // reference to a complex wave
WAVE/T w              // reference to a text wave
WAVE/Z w              // reference that does NOT error if wave doesn't exist (w will be null)
WAVE/D w              // reference to a double-precision wave (rarely needed explicitly)
WAVE/I w              // reference to a 32-bit integer wave
WAVE/L w              // reference to a 64-bit integer wave (int64)
WAVE/L/U w            // reference to an unsigned 64-bit integer wave (uint64)
WAVE/B w              // reference to a byte (8-bit) wave
WAVE/W w              // reference to a 16-bit integer wave
```

### Referencing waves in other data folders

```igor
WAVE w = root:myData:myWave              // full absolute path
WAVE w = dfr:myWave                      // using a DFREF variable (see section 5)
WAVE w = $(pathString)                   // path constructed at runtime in a string
WAVE w = $("root:myData:" + waveName)   // dynamic name construction
```

### Checking if a reference is valid

Always use `/Z` and then check `WaveExists()` when the wave may not exist:

```igor
WAVE/Z w = root:myData:myWave
if (!WaveExists(w))
    Print "Wave not found"
    return
endif
```

**Never** assume a WAVE declaration succeeded without checking — if the wave
doesn't exist and you didn't use /Z, the function aborts with an error.

### Getting a wave reference from a name string

```igor
String name = "myWave"
WAVE w = $name                    // wave in current data folder
WAVE w = root:myData:$name        // wave in specific folder — WRONG syntax
WAVE w = $(   "root:myData:" + name)   // CORRECT: build full path in string
```

The `$` operator dereferences a string into a name. It cannot be used
mid-path — build the full path string first, then apply `$` once.

---

## 3. Passing Waves to and from Functions

### Passing waves as parameters

Waves are always passed by reference (the reference is copied, not the data):

```igor
// Declare parameter as WAVE in both the parameter list and declaration
Function ProcessWave(w)
    WAVE w                        // parameter declaration
    w = w * 2
End

// Inline parameter syntax (Igor 7+, preferred):
Function ProcessWave(WAVE w)
    w = w * 2
End

// Typed wave parameters:
Function ProcessTextWave(WAVE/T tw)
    Print tw[0]
End

Function ProcessComplexWave(WAVE/C cw)
    // ...
End
```

### Returning a wave reference from a function

Use `Function/WAVE` return type:

```igor
Function/WAVE MakeResultWave(Variable n)
    Make/O/N=(n) resultWave
    WAVE w = resultWave
    return w
End

// Calling it:
WAVE result = MakeResultWave(100)
```

Or use Multiple Return Syntax (Igor 8+):

```igor
Function [WAVE w] MakeResultWave(Variable n)
    Make/O/N=(n) resultWave
    WAVE w = resultWave
End

// Calling it:
[WAVE result] = MakeResultWave(100)
```

### Returning a wave reference to a wave in a specific data folder

```igor
Function/WAVE GetMyWave(DFREF dfr, String name)
    WAVE/Z w = dfr:$name
    if (!WaveExists(w))
        return $""             // return null wave reference
    endif
    return w
End

// Check for null on the receiving side:
WAVE result = GetMyWave(myDFR, "data")
if (!WaveExists(result))
    Abort "Wave not found"
endif
```

---

## 4. NVAR and SVAR — Global Variable References

Global numeric variables and global strings are **not** directly accessible
inside functions by name. You must declare a reference first.

```igor
// WRONG — globals are not automatically visible in functions:
Function BadGlobal()
    myGlobalVar = 42          // Error: not declared
End

// CORRECT:
Function GoodGlobal()
    NVAR myGlobalVar          // reference to global numeric variable in current DF
    myGlobalVar = 42
End

Function GoodGlobalString()
    SVAR myGlobalStr          // reference to global string in current DF
    myGlobalStr = "hello"
End
```

### Referencing globals in other data folders

```igor
NVAR v = root:Packages:MyPkg:settingValue
SVAR s = root:Packages:MyPkg:settingName
```

### Checking existence before use

```igor
NVAR/Z v = root:Packages:MyPkg:counter
if (!NVAR_Exists(v))
    Variable/G root:Packages:MyPkg:counter = 0
    NVAR v = root:Packages:MyPkg:counter
endif
```

Similarly for strings: `SVAR/Z s = ...` then `SVAR_Exists(s)`.

---

## 5. DFREF — Data Folder References

`DFREF` is a reference to a data folder, analogous to WAVE for waves.
It is the preferred way to write folder-aware code in Igor 7+.

### Declaring and obtaining a DFREF

```igor
DFREF dfr = root:myData                   // absolute path
DFREF dfr = :subFolder                    // relative to current DF
DFREF dfr = GetDataFolderDFR()            // current data folder
DFREF dfr = NewFreeDataFolder()           // anonymous free data folder (not in tree)
DFREF dfr = $("root:myData:" + name)      // dynamic path
```

### Checking if a DFREF is valid

```igor
DFREF dfr = root:mayNotExist
if (DataFolderRefStatus(dfr) == 0)
    Print "Data folder does not exist"
    return
endif
```

`DataFolderRefStatus` returns:
- `0` — invalid (folder doesn't exist)
- `1` — refers to a regular data folder
- `3` — refers to a free data folder

### Using DFREF to access waves and variables

```igor
DFREF dfr = root:myData
WAVE w = dfr:intensity           // wave in that folder
NVAR n = dfr:temperature         // global variable in that folder
SVAR s = dfr:sampleName         // global string in that folder
```

### Passing DFREF as a function parameter

```igor
Function AnalyzeFolder(DFREF dfr)
    WAVE/Z w = dfr:data
    if (!WaveExists(w))
        Abort "No data wave found"
    endif
    WaveStats/Q w
    Print "Mean =", V_avg
End
```

### Saving and restoring the current data folder

**Always** save and restore the current data folder if your function changes it:

```igor
Function DoSomethingInFolder(String path)
    DFREF saveDF = GetDataFolderDFR()        // save current DF
    SetDataFolder path
    // ... do work ...
    SetDataFolder saveDF                     // restore
End
```

Failure to restore the current data folder is one of the most common bugs
in Igor procedures. Use this pattern every time you call `SetDataFolder`.

### Returning a DFREF (Igor 10+)

```igor
Function [DFREF df] GetOrCreateFolder(String name)
    DFREF root = GetDataFolderDFR()
    NewDataFolder/O root:$name
    DFREF df = root:$name
End

// Calling:
[DFREF myDF] = GetOrCreateFolder("results")
```

---

## 6. Free Waves

Free waves exist only in memory, are not in any data folder, and are
automatically destroyed when no references point to them. They are ideal
for temporary intermediate results in functions.

### Creating free waves

```igor
// Make with /FREE flag:
Make/FREE/N=100 tempWave
Make/FREE/N=(n, m) tempMatrix

// Duplicate with /FREE:
Duplicate/FREE sourceWave, tempCopy

// NewFreeWave function:
WAVE tempWave = NewFreeWave(2, 100)   // type 2 = single precision float, 100 points
```

Wave type codes for `NewFreeWave`: 0=double, 1=complex, 2=single, 4=int8,
8=int16, 16=int32, 32=unsigned int, 64=int64, 128=unsigned int64, 512=text.
Add these together for combinations (e.g. 4+32=36 for unsigned int8).

### Free waves as temporary buffers (common pattern)

```igor
Function/WAVE ComputeResult(WAVE input)
    Duplicate/FREE input, temp
    temp = temp^2 + temp
    Smooth 5, temp
    // Return a permanent wave, not the free wave:
    Make/O/N=(numpnts(temp)) result = temp
    return result
End
```

### Key rules for free waves

- Free waves cannot be the target of `Display`, `AppendToGraph`, etc. (they
  have no name for Igor to reference in graph recreation macros). Create a
  permanent wave for anything that needs to be plotted persistently.
- Free waves **can** be passed to operations like `WaveStats`, `FFT`,
  `CurveFit` (with /NOINT or structure-based approaches), `MatrixOP`, etc.
- A free wave is destroyed as soon as the last WAVE reference to it goes
  out of scope (end of function, or explicitly set to `$""`).

---

## 7. Free Data Folders

Free data folders are in-memory containers not attached to the data folder
tree. Useful for bundling temporary waves inside a function.

```igor
DFREF freeDFR = NewFreeDataFolder()
Make/O freeDFR:tempWave/N=100
WAVE w = freeDFR:tempWave
w = gnoise(1)
// freeDFR and all its contents are destroyed when freeDFR goes out of scope
```

---

## 8. The $ Operator — Name-to-Reference Resolution

`$` converts a string expression into an Igor object reference. It is used
whenever the name of a wave, variable, or data folder is constructed at runtime.

```igor
String name = "myWave"
WAVE w = $name                    // resolve name to wave in current DF

String path = "root:myData:myWave"
WAVE w = $path                    // resolve full path

Make/O $(name + "_result")        // create wave with constructed name
WAVE result = $(name + "_result")
```

### $ in wave arithmetic (assignment to dynamically named wave)

```igor
String outName = "processedData"
Make/O/N=100 $outName
WAVE out = $outName
out = p^2
```

### $ cannot be used mid-path — build the full path string first

```igor
// WRONG:
WAVE w = root:myData:$waveName       // syntax error

// CORRECT:
WAVE w = $(  "root:myData:" + waveName)
// or:
DFREF dfr = root:myData
WAVE w = dfr:$waveName               // $ at the end of a dfr: prefix IS valid
```

---

## 9. WaveExists, DataFolderExists, NVAR_Exists, SVAR_Exists

Use these to check validity before using references. Never assume an object
exists without checking, especially in general-purpose functions.

```igor
// Waves:
if (WaveExists(w))          // w is a WAVE reference (use after WAVE/Z)
if (WaveExists($name))      // check by name in current DF
if (WaveExists($("root:myData:" + name)))  // check by full path

// Data folders:
if (DataFolderExists("root:myData"))       // string path — most common form
DFREF/Z dfr = root:myData
if (DataFolderRefStatus(dfr) != 0)         // using a DFREF

// Global variables:
NVAR/Z v = myGlobalVar
if (NVAR_Exists(v))

// Global strings:
SVAR/Z s = myGlobalStr
if (SVAR_Exists(s))
```

---

## 10. Common Patterns and Pitfalls

### Pattern: function that works in a given data folder

```igor
Function AnalyzeRun(DFREF runDF)
    // Check required waves exist
    WAVE/Z raw = runDF:rawData
    WAVE/Z q   = runDF:qVector
    if (!WaveExists(raw) || !WaveExists(q))
        Printf "Missing waves in %s\r", GetDataFolder(1, runDF)
        return
    endif

    // Save/restore current DF if any operations need current DF
    DFREF saveDF = GetDataFolderDFR()
    SetDataFolder runDF

    WaveStats/Q raw
    Variable mean = V_avg

    SetDataFolder saveDF

    // Store result back in runDF (not current DF)
    Variable/G runDF:meanIntensity = mean
End
```

### Pattern: iterate over waves in a data folder by name

```igor
Function ProcessAllWaves(DFREF dfr)
    Variable n = CountObjectsDFR(dfr, 1)   // type 1 = waves
    Variable i
    for (i = 0; i < n; i += 1)
        String name = GetIndexedObjNameDFR(dfr, 1, i)
        WAVE w = dfr:$name
        // process w...
    endfor
End
```

### Pattern: create output wave in the same folder as input wave

```igor
Function/WAVE ComputeResult(WAVE input)
    DFREF dfr = GetWavesDataFolderDFR(input)
    String outName = NameOfWave(input) + "_result"
    Make/O/N=(numpnts(input)) dfr:$outName
    WAVE result = dfr:$outName
    result = input * 2
    return result
End
```

### Pitfall: modifying the current data folder without restoring it

```igor
// WRONG — leaves current DF changed after function returns:
Function BadFolder()
    SetDataFolder root:myData
    WAVE w = intensity
    WaveStats/Q w
End

// CORRECT:
Function GoodFolder()
    DFREF saveDF = GetDataFolderDFR()
    SetDataFolder root:myData
    WAVE w = intensity
    WaveStats/Q w
    SetDataFolder saveDF
End
```

### Pitfall: using WAVE without /Z when wave may not exist

```igor
// WRONG — aborts with error if wave missing:
Function BadCheck(String name)
    WAVE w = $name
    WaveStats/Q w
End

// CORRECT:
Function GoodCheck(String name)
    WAVE/Z w = $name
    if (!WaveExists(w))
        Printf "Wave '%s' not found\r", name
        return
    endif
    WaveStats/Q w
End
```

### Pitfall: returning a free wave from a function

```igor
// DANGEROUS — free wave may be destroyed before caller uses it:
Function/WAVE BadReturn()
    Make/FREE/N=100 temp = gnoise(1)
    return temp    // temp reference goes out of scope here — wave destroyed!
End

// CORRECT — return a permanent wave:
Function/WAVE GoodReturn()
    Make/FREE/N=100 temp = gnoise(1)
    Make/O/N=100 permanentResult = temp
    return permanentResult
End
```

Actually: in Igor, returning a free wave from a function IS safe as long as the
caller immediately assigns it to a WAVE variable — Igor extends the lifetime.
But assigning to a permanent wave first is safer and more explicit.

### Pitfall: $ with a quoted liberal name

When building dynamic paths, do not include quotes inside the string:

```igor
// WRONG — single quotes are for Igor parsing, not for $ operator:
String name = "'my wave'"
WAVE w = $name      // looks for a wave literally named 'my wave' with quotes

// CORRECT — no quotes needed with $:
String name = "my wave"
WAVE w = $name      // correctly resolves to the wave named "my wave"
```

---

## 11. Quick Reference Table

| Goal | Syntax |
|---|---|
| Reference wave in current DF | `WAVE w = myWave` |
| Reference wave, don't error if missing | `WAVE/Z w = myWave` |
| Reference wave by string name | `WAVE w = $name` |
| Reference wave by full path string | `WAVE w = $("root:myData:" + name)` |
| Reference wave via DFREF | `WAVE w = dfr:myWave` or `WAVE w = dfr:$name` |
| Check wave exists | `WaveExists(w)` after `WAVE/Z` |
| Reference text wave | `WAVE/T tw = myTextWave` |
| Reference complex wave | `WAVE/C cw = myComplexWave` |
| Reference global variable | `NVAR v = myGlobalVar` |
| Reference global string | `SVAR s = myGlobalStr` |
| Reference global in other DF | `NVAR v = root:myData:myVar` |
| Get current DF as DFREF | `DFREF dfr = GetDataFolderDFR()` |
| Reference data folder | `DFREF dfr = root:myData` |
| Check data folder exists (string) | `DataFolderExists("root:myData")` |
| Check DFREF is valid | `DataFolderRefStatus(dfr) != 0` |
| Save/restore current DF | `DFREF save = GetDataFolderDFR()` ... `SetDataFolder save` |
| Create free wave | `Make/FREE/N=n tempWave` |
| Create free data folder | `DFREF fdfr = NewFreeDataFolder()` |
| Get DF containing a wave | `DFREF dfr = GetWavesDataFolderDFR(w)` |
| Get name of a wave | `String name = NameOfWave(w)` |
| Iterate waves in DF | `CountObjectsDFR(dfr,1)` + `GetIndexedObjNameDFR(dfr,1,i)` |
| Return wave from function | `Function/WAVE Foo()` ... `return w` |
| Return DFREF from function (Igor 10) | `Function [DFREF df] Foo()` ... |

---

## Reference URLs

| Topic | URL |
|---|---|
| Programming Overview (functions, parameters) | https://docs.wavemetrics.com/igorpro/programming/programming |
| Programming Techniques (DF patterns) | https://docs.wavemetrics.com/igorpro/programming/programming-techniques |
| WAVE keyword | https://docs.wavemetrics.com/igorpro/commands/wave |
| NewFreeWave | https://docs.wavemetrics.com/igorpro/commands/newfreewave |
| NewFreeDataFolder | https://docs.wavemetrics.com/igorpro/commands/newfreedatafolder |
| GetDataFolderDFR | https://docs.wavemetrics.com/igorpro/commands/getdatafolderdfr |
| GetWavesDataFolderDFR | https://docs.wavemetrics.com/igorpro/commands/getwavesdatafolderdfr |
| DataFolderRefStatus | https://docs.wavemetrics.com/igorpro/commands/datafolderrefstatus |
| WaveExists | https://docs.wavemetrics.com/igorpro/commands/waveexists |
| CountObjectsDFR | https://docs.wavemetrics.com/igorpro/commands/countobjectsdfr |
| GetIndexedObjNameDFR | https://docs.wavemetrics.com/igorpro/commands/getindexedobjnamedfr |
| NVAR_Exists | https://docs.wavemetrics.com/igorpro/commands/nvar_exists |
| SVAR_Exists | https://docs.wavemetrics.com/igorpro/commands/svar_exists |
