---
description: "The Python operation executes single Python statements from Igor. If the var or array keyword was used, Igor attempts to assign a Python object to an existing…"
slug: /commands/python
---

<div className="command-signature">

## <strong>Python</strong>  [/Z] <em>execute</em> = <em>codeStr</em> [, <em>var</em> = {<em>pyVarStr</em>, <em>igorVar</em>}, <em>array</em> = {<em>pyArrayStr</em>, <em>igorWave</em>}] {#python}

</div>

The *Python* operation executes single Python statements from Igor.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">execute = *codeStr*</span> | Python code to execute. |
| <span class="table-cell-nowrap">var = *{pyVarStr, igorVar}*</span> | Assigns the named Python numeric or string variable to the Igor numeric or string variable *igorVar*. *igorVar* cannot be the full path to a global variable. To assign to a global variable, you must first declare it locally using [NVAR](/igorpro/programming/keywords/object-reference-keywords.md#nvar) (numeric variables) or [SVAR](/igorpro/programming/keywords/object-reference-keywords.md#svar) (string variables). |
| <span class="table-cell-nowrap">array = *{pyArrayStr, igorWave}*</span> | Assigns the named Python array-like object to the Igor wave *igorWave*. *igorWave* must already exist, and can be either a local wave reference or the full path to a wave. Both global and free waves are supported. See ***Returning Python variables to Igor*** below for more information. |
|  | Array-like objects include *NumPy* arrays, lists, tuples, or built in Python arrays (array.array). |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Do not report any errors. Error messages will still be printed to the Python Console and stored in *S_PythonError*. |

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| V_flag | Error code, set to zero if there was no error. |
| S_PythonError | If a Python error occurred, this string will be set to Python's traceback message. |
|  | Only Python errors will set this string, an Igor-related error will not. For example, syntax errors in the Python code being executed will set *S_PythonError*. However, if a variable or wave doesn't exist while using the *var* or *array* keywords, it will not be set since that is not a Python error, but an Igor error. |

### *Returning Python variables to Igor* {#returning-python-variables-to-igor}

If the *var* or *array* keyword was used, Igor attempts to assign a Python object to an *existing* Igor object. Igor will not create the new object for you. The Python and Igor types must be compatible for this to succeed. See [Python to Igor Type Conversions](/igorpro/python/python-overview.md#python-to-igor-type-conversions) for descriptions of compatible objects. Complex numbers can only be assigned to complex Igor variables. Similarly, arrays that contain complex numbers can only be assigned to complex waves.

For Python array-like objects (*lists*, *tuples*, built-in *array.arrays*, and *NumPy arrays*), Igor generally expects the array to contain a single basic type. For instance, a list that contains both integers and strings will throw a Python exception during the conversion, since Igor waves must be of a single type. However, if multiple types are present that can be safely converted between without data loss, Igor will convert each data point to the larger type. For example, a Python list containing both integers and floats will convert each data point to a float during the assignment to an Igor wave.

```igor
Make/O floatWave // 32 bit floating point wave

// The data will be converted to floating point during the assignment
// resulting in {3.0, 3.141, 5.0, 6.282}
Python execute = "mixedList = [3, 3.141, 5, 6.282]", array = {"mixedList", floatWave}
```

However, the Igor wave will *not* change its type to accomodate the incoming data from Python. In the previous example, if we instead assigned the mixed Python list to an integer wave in Igor, the data will ultimately be truncated to accomodate the type of the Igor wave:

```igor
Make/O/I integerWave // integer wave

// The Python data will still be converted to floating point
// But the Igor wave it is being assigned to is an integer type, so the
// resulting data will be truncated as {3, 3, 5, 6}
Python execute = "mixedList = [3, 3.141, 5, 6.282]", array = {"mixedList", integerWave}
```

An Igor wave will change its size/shape to reflect the data of that is being assigned to it. For example:

```igor
// 'data' starts as a 10 point, 1D wave
Make/O/N=10 data

// 'data' will have 2 rows and 3 columns after the assignment
Python execute = "array2D = [[1, 2, 3], [4, 5, 6]]", array = {"array2D", data}
```

Python array-like objects that are being assigned to Igor waves can contain at most 4 dimensions, since that is the maximum dimensionality of an Igor wave.

Although the size/shape of the wave will be changed to accomodate the data, other wave attributes such as scaling, units, and notes are not altered.

### *Object Lifetime* {#object-lifetime}

Any global Python variables that are created during code execution will be persistent for the lifetime of the Igor instance, or until they are explicitly deleted. As a result, subsequent calls to the [Python](/igorpro/commands/python.md) and [PythonFile](/igorpro/commands/pythonfile.md) operations can use any previously created variables or imported libraries. Similarly, any code run through the [Python Console](/igorpro/python/python-overview.md#python-console) will also have access to imported libraries or variables created from the operations, and vice versa.

:::warning
If an new experiment is opened without restarting Igor, global Python objects from the `igorpro` module (`igorpro.wave`, `igorpro.variable`, `igorpro.string`, etc.) will be stale, since the underlying Igor objects no longer exist. Attempting to use those stale objects from Python will result in an error saying that the object no longer exists.
:::

### *Restarting the Python Interpreter* {#restarting-the-python-interpreter}

Opening a new Igor experiment without closing Igor will not reset the Python interpreter. In order to get a completely clean Python session, or to change Python environments, you must restart Igor.

### *Error handling* {#error-handling}

Any error that occurs during Python code execution will be relayed to Igor as a runtime error. The error message will contain the Python traceback message, which is also printed to the [Python Console](/igorpro/python/python-overview.md#python-console). Like any other Igor runtime error, Python runtime errors can be caught in a [try-catch-endtry](/igorpro/programming/keywords/flow-control.md#try-catch-endtry) construct:


```igor
try
	Python execute = "var = 1/0"; AbortOnRTE
catch
	// Print the error message, which indicates a ZeroDivisionError
	Print GetRTErrMessage()

	// Clear the error	
	Variable err = GetRTError(1)	
endtry
```

Any errors that occur during Python execution will be written to the Python Console, and also stored in the *S_PythonError* string.

*V_flag* is set to a non-zero error code if any errors occurred. This can be used to retrieve the traceback message from Python. For example:

```igor
// This time the error is ignored, due to the /Z flag
Python execute = "var = 1/0"
if (V_flag)
	print S_PythonError
endif
```

### *Examples* {#examples}

Executing a simple Python statement:

```igor
Python execute = "a = 5*5"
```

Assigning a Python variable to an Igor variable after executing code:

```igor
Variable varA

// This syntax says: after executing this code, assign the Python variable called
// 'a' to the Igor variable varA.
Python execute = "a = somePythonFunction()", var = {"a", varA}
```

Assigning a Python variable to an Igor variable without any code execution:

```igor
Variable varA
Python var = {"a", varA}
```

Importing and using a third-party library to create a *NumPy* array, then assigning the array to a wave:

```igor
Python execute = "import numpy as np"
Make/O waveA	// Make a new wave

// Creates a random 250 point array using numpy, assign it to waveA
Python execute = "arr = np.random.rand(250)", array = {"arr", waveA}
```

Assigning an array-like object to a free wave:

```igor
// Creates a 32 bit float free wave with zero points
Make/FREE/N=0 freeWaveA
Python execute = "ls = [float(x) for x in range(25)]", array = {"ls", freeWaveA}
```

A simple script for averaging all the waves in a folder, using *NumPy*:

```python
# averaging.py
import igorpro
import numpy as np

# Input a path to an Igor data folder
def averageFolder(path: str):

	# Retrieve a reference to the data folder from Igor	
	folder = igorpro.folder(path)
	
	# Retrieve a list of all the waves in the folder
	waves = folder.waves()		
	
	# Create an array to hold the average. Here we're assuming that each wave
	# is the same size as the first wave in the folder.
	size = waves[0].points()
	average = np.zeros(size)

	# Iterate through each wave in the folder, adding it to the average
	for wave in folder.waves():
		# Converts each wave to a numpy array before adding it to the average
		average += wave.asarray()
	
	average /= folder.num_waves()
	return average
```

```igor
// In Igor, first import the file and then run the function, 
// assigning the output array to an Igor wave
Python execute = "import averaging as avg"

NewDataFolder/O/S root:average
Make/O/D avg
Python execute = "a = avg.averageFolder('root:')", array = {"a", avg}
```

### *See Also* {#see-also}
[PythonEnv](/igorpro/commands/pythonenv.md), [PythonFile](/igorpro/commands/pythonfile.md), [Python Overview](/igorpro/python/python-overview.md), [Python Module Reference](/igorpro/python/python-module-reference.md)