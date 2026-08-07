---
name: "IgorPythonIntegration"
description: "Provides reference for writing Python code that communicates with Igor Pro 10 using the `igorpro` module."
parameters: {}
---

# Instructions
You are an Igor Pro Python integration expert. When this skill is invoked, use the following reference to assist the user in writing bidirectional Python code for Igor Pro 10:

1. **Constraint Check:** Always remind the user that the `igorpro` module can ONLY be used from within Igor Pro itself (via `Python`, `PythonFile`, or the Python Console).
2. **Execution Methods:** Use the "Three Ways to Run Python from Igor" section to guide users on how to launch their scripts.
3. **Environment Setup:** Refer to the "Setup" section for virtual environment activation and VSCode autocomplete configuration.
4. **API Usage:** 
   - Use `igorpro.execute()` for general Igor commands.
   - Use `igorpro.wave` for all wave operations (creation, reading, modifying).
   - Use `igorpro.folder` for data folder navigation and management.
   - Use `igorpro.variable` and `igorpro.string` for global variable/string access.
   - Use `igorpro.fn` to call Igor built-in, XOP, or user-defined functions from Python.
5. **Data Types:** Ensure users understand the mapping between NumPy dtypes and Igor types (e.g., `float64` to `igorpro.float64`).
6. **Safety:** Warn users that Python crashes will crash the entire Igor Pro application.

---

# Igor Pro — Python Integration (`igorpro` module) Reference

This skill covers writing Python code that communicates with Igor Pro 10 using the `igorpro` module.

**Official docs:**
- https://docs.wavemetrics.com/igorpro/python/python-overview
- https://docs.wavemetrics.com/igorpro/python/python-module-reference

---

## 1. Three Ways to Run Python from Igor

```igor
// Inline statement
Python "import numpy as np"

// Run a .py file
PythonFile file = "MyProject/analysis.py"

// With path symbolic name
NewPath/O scriptPath, "/path/to/scripts/"
PythonFile/P=scriptPath file = "analysis.py"
```

---

## 2. Setup & Environment

**Supported versions:** Python 3.11–3.14 (standard only).

### Activating Virtual Environments
```igor
NewPath/O envPath, "path/to/parent/"
PythonEnv/P=envPath activate = "myEnv"
```
*Note: Environment changes require an Igor restart to take effect.*

### VSCode Autocomplete Configuration
Add this to `settings.json` to resolve the `igorpro` module:
```json
"python.analysis.extraPaths": [
    "C:/Program Files/WaveMetrics/Igor Pro 10 Folder/IgorBinaries_x64/Python"
]
```

---

## 3. Core API Reference

### Top-Level Commands
```python
import igorpro

igorpro.execute("Make/O/N=100 myWave")
igorpro.print("Analysis complete")   # prints to Igor history
igorpro.version()
```

### `igorpro.wave` (Wave Management)
**Accessing/Creating:**
```python
w = igorpro.wave('root:myWave')                # Access existing
w = igorpro.wave.create('newWave', 100)        # Create new (float32 default)
w = igorpro.wave.createfrom('qWave', np_arr)   # From NumPy array
```

**Reading/Modifying:**
```python
arr   = w.asarray()       # Returns numpy ndarray (copies data)
shape = w.shape()         # e.g. (200,) or (256,256)
val   = w[10, 20]         # 2D indexing [row, col]

w.set_data(np.sqrt(w.asarray())) # Update data
w.set_scale('x', 0.0, 1.0, 'range')
w.set_units('x', '1/A')
w.redimension((500, 500))
```

**Statistics:**
```python
s = w.stats()                    # Returns dict: {'V_avg': ..., 'V_sdev': ...}
s = w.stats((0.01, 0.1))         # Stats within x-range
```

### `igorpro.folder` (Data Folder Management)
```python
df = igorpro.folder('root:data')
sub = df.subfolder('fits')
waves = df.waves()               # list[igorpro.wave]

df.set()                         # Set as current DF (use with caution)
df.kill(ignoreErrors=True)       # Delete folder
```

### `igorpro.fn` (Calling Igor Functions from Python)
Calls built-in, XOP, or user-defined functions. Case-insensitive.

```python
# Built-ins
val = igorpro.fn.sqrt(2.0)
res = igorpro.fn.sortlist('x;c;e;g;d;a', ';', 1)

# User-defined
result = igorpro.fn.MyAnalysisFunc(w, 0.01)
```

**Limitations:** Cannot call functions with pass-by-reference parameters, Structure parameters, or Multiple Return Syntax.

---

## 4. Stability & Safety

- **Crash Risk:** A Python crash will terminate the Igor Pro process immediately. Always enable Igor's auto-save.
- **Object Lifetime:** Deleting an `igorpro.wave` object in Python does NOT delete the wave in Igor; it only removes the Python reference.
- **Data Types:** `numpy.float16` is NOT supported; convert to `float32` before passing to Igor.
- **GUI:** Avoid importing `Qt` in Python scripts, as it conflicts with Igor's internal Qt implementation.
