---
name: "IgorWaveDFRefReference"
description: "Provides a comprehensive reference for WAVE and DFREF syntax, including wave declarations, passing waves to functions, NVAR/SVAR usage, and data folder management."
parameters: {}
---

# Instructions
You are an Igor Pro expert specializing in data structures. When this skill is invoked, use the following reference to assist with generating or debugging code involving waves, variables, and data folders:

1. **Wave vs. WAVE:** Always ensure that when operating on a wave inside a function, a `WAVE` reference is declared first. Never use a wave name directly without a declaration.
2. **Declarations:** Use the appropriate flags for declarations (e.g., `/Z` for optional existence, `/T` for text, `/C` for complex).
3. **Dynamic Names:** When constructing names at runtime using strings, use the `$` operator on the *full* path string (e.g., `WAVE w = $("root:folder:" + name)`).
4. **Function Parameters:** When passing waves to functions, declare them as `WAVE` in the parameter list (e.g., `Function MyFunc(WAVE w)`).
5. **Global Variables:** Remind users that `NVAR` and `SVAR` must be declared inside functions to access global numeric or string variables.
6. **Data Folders (DFREF):** Use `DFREF` for folder-aware code. Always follow the "Save and Restore" pattern when using `SetDataFolder` to prevent side effects.
7. **Free Waves/Folders:** Use `/FREE` for temporary objects that should be destroyed when they go out of scope.
8. **Validation:** Always recommend checking existence using `WaveExists()`, `DataFolderExists()`, `NVAR_Exists()`, or `SVAR_Exists()` when working with dynamic or optional objects.

---

# Igor Pro — WAVE and DFREF Reference Syntax

This document covers the reference system for waves, global variables, strings, and data folders.

**Official Reference:** https://docs.wavemetrics.com/igorpro/programming/programming

---

## 1. The Core Distinction: Wave vs. WAVE

- **A wave** — an array of data stored in a data folder (a global object).
- **A WAVE reference** — a local variable inside a function that *points to* a wave.

```igor
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
WAVE w                // real numeric wave
WAVE/C w              // complex wave
WAVE/T w              // text wave
WAVE/Z w              // optional (null if not exists)
WAVE/I w              // 32-bit integer
WAVE/L w              // 64-bit integer (int64)
WAVE/L/U w            // unsigned 64-bit integer (uint64)
WAVE/B w              // byte (8-bit)
WAVE/W w              // 16-bit integer
```

### Referencing waves in other data folders
```igor
WAVE w = root:myData:myWave              // absolute path
WAVE w = dfr:myWave                      // using a DFREF variable
WAVE w = $(pathString)                   // path from string
WAVE w = $("root:myData:" + waveName)   // dynamic construction
```

---

## 3. Passing Waves to and from Functions

### Parameters
```igor
// Preferred (Igor 7+)
Function ProcessWave(WAVE w)
    w = w * 2
End

// Typed parameters
Function ProcessTextWave(WAVE/T tw)
    Print tw[0]
End
```

### Returning Waves
```igor
// Using Function/WAVE return type
Function/WAVE MakeResultWave(Variable n)
    Make/O/N=(n) resultWave
    WAVE w = resultWave
    return w
End

// Using Multiple Return Syntax (Igor 8+)
Function [WAVE w] MakeResultWave(Variable n)
    Make/O/N=(n) resultWave
    WAVE w = resultWave
End
```

---

## 4. NVAR and SVAR — Global Variable References

```igor
Function GoodGlobal()
    NVAR myGlobalVar          // reference to global numeric variable
    myGlobalVar = 42
End

Function GoodGlobalString()
    SVAR myGlobalStr          // reference to global string
    myGlobalStr = "hello"
End
```

---

## 5. DFREF — Data Folder References

```igor
DFREF dfr = root:myData                   // absolute path
DFREF dfr = GetDataFolderDFR()            // current data folder
DFREF dfr = NewFreeDataFolder()           // anonymous free data folder

// Accessing via DFREF
WAVE w = dfr:intensity           
NVAR n = dfr:temperature         
SVAR s = dfr:sampleName         

// Save and Restore Pattern (CRITICAL)
Function DoSomethingInFolder(String path)
    DFREF saveDF = GetDataFolderDFR()        // 1. Save current DF
    SetDataFolder path                       // 2. Change DF
    // ... do work ...
    SetDataFolder saveDF                     // 3. Restore original DF
End
```

---

## 6. Free Waves and Folders

### Free Waves (Temporary)
```igor
Make/FREE/N=100 tempWave        // Created in memory, destroyed when out of scope
Duplicate/FREE sourceWave, tempCopy
```

### Free Data Folders (Temporary)
```igor
DFREF freeDFR = NewFreeDataFolder()
Make/O freeDFR:tempWave/N=100
// Destroyed when freeDFR goes out of scope
```

---

## 7. The $ Operator — Name-to-Reference Resolution

The `$` operator converts a string into an object reference. It cannot be used mid-path.

```igor
// CORRECT: Build full path first, then dereference once
String name = "myWave"
WAVE w = $("root:myData:" + name)

// CORRECT: Using DFREF prefix
DFREF dfr = root:myData
WAVE w = dfr:$name               // Valid!
```

---

## 8. Validation Checks

| Object Type | Check Command |
|-------------|--------------|
| Wave        | `WaveExists(w)` (after `WAVE/Z w`) |
| Data Folder | `DataFolderExists("path")` or `DataFolderRefStatus(dfr) != 0` |
| Global Var  | `NVAR/Z v = ...; NVAR_Exists(v)` |
| Global Str  | `SVAR/Z s = ...; SVAR_Exists(s)` |
