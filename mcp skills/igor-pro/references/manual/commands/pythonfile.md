---
description: "The PythonFile operation executes an entire.py file from top to bottom."
slug: /commands/pythonfile
---

<div className="command-signature">

## <strong>PythonFile</strong>  [/Z] <em>file</em> = <em>fileStr</em> [, <em>var</em> = {<em>pyVarStr</em>, <em>igorVar</em>}, <em>array</em> = {<em>pyArrayStr</em>, <em>igorWave</em>}, <em>args</em> = <em>argListStr</em>] {#pythonfile}

</div>

The *PythonFile* operation executes an entire *.py* file from top to bottom. Note, this does not import the file as a module, so a programmer can change the script and immediately run the new code without restarting the Python Interpreter.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">file = *fileStr*</span> | Python file to execute. This can either be the name of a file on the Python path, or the full path to the file. If you use a full path for *fileStr*, see Path Separators for details on forming the path. *fileStr* must include the file extension (.py). This keyword is required. |
| <span class="table-cell-nowrap">var = *{pyVarStr, igorVar}*</span> | Assigns the named Python numeric or string variable to the Igor numeric or string variable *igorVar*. *igorVar* cannot be the full path to a global variable. To assign to a global variable, you must first declare it locally using [NVAR](/igorpro/programming/keywords/object-reference-keywords.md#nvar) (numeric variables) or [SVAR](/igorpro/programming/keywords/object-reference-keywords.md#svar) (string variables). |
| <span class="table-cell-nowrap">array = *{pyArrayStr, igorWave}*</span> |  |
|  | Assigns the named Python array-like object to the Igor wave *igorWave*. |
|  | *igorWave* must already exist, and can be either a local wave reference or the full path to a wave. Both global and free waves are supported. See ***Returning Python variables to Igor*** below for more information. |
|  | Array-like objects include NumPy arrays, lists, tuples, or built in Python arrays (array.array). |
| <span class="table-cell-nowrap">args = *argListStr*</span> | String list specifying a list of arguments to provide to the Python script. |
|  | Individual arguments should be separated by whitespace (tabs or spaces). Each argument will be inserted as an entry in the *sys.argv* Python list, which can then be parsed in the Python script itself. Igor expressions or functions that return a string can also be used. Note, strings that contain numeric values must be converted back to numeric types after parsing them in the Python script. |

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

### *Details* {#details}
*PythonFile* is analogous to running a Python file from the system command prompt, as in:

```
python myScript.py
```

As such, *PythonFile* sets the Python global variable *\_\_name\_\_* to *'\_\_main\_\_'*, which can act as a guard for code that will only run when the script is executed by *PythonFile*, but not when it is imported as a module. See ***Examples***, which illustrate the difference between importing and executing a file.

### *Returning Python variables to Igor* {#returning-python-variables-to-igor}
If the *var* or *array* keyword was used, Igor attempts to assign a Python object to an existing Igor object. Igor will not create the new object for you. The Python and Igor types must be compatible for this to succeed. See [Python to Igor Type Conversions](/igorpro/python/python-overview.md#python-to-igor-type-conversions) for descriptions of compatible objects. See the *Returning Python variables to Igor* help section in [Python](/igorpro/commands/python.md) for an in-depth discussion and examples.

### *Object lifetime* {#object-lifetime}
Any global Python variables that are created during code execution will be persistent for the lifetime of the Igor instance. As a result, subsequent calls to the [Python](/igorpro/commands/python.md) and [PythonFile](/igorpro/commands/pythonfile.md) operations can use any previously created variables or imported libraries. Similarly, any code run through the Python Console will also have access to imported libraries or variables created from the operation, and vice versa.

When running a Python script, note that variables created within a method are garbage collected when execution returns, and thus cannot be returned to Igor. In order to return a Python variable to Igor, it must be created with global scope.

:::warning
If an new experiment is opened without restarting Igor, global Python objects from the `igorpro` module (`igorpro.wave`, `igorpro.variable`, `igorpro.string`, etc.) will be stale, since the underlying Igor objects no longer exist. Attempting to use those stale objects from Python will result in an error saying that the object no longer exists.
:::

### *Restarting the Python Interpreter* {#restarting-the-python-interpreter}
Opening a new Igor experiment without closing Igor will not reset the Python interpreter. In order to get a completely clean Python session, or to change Python environments, you must restart Igor.

### *Error handling* {#error-handling}
Errors that occur during Python code execution will be relayed to Igor as runtime errors. The error message will contain the Python traceback message, which is also printed to the [Python Console](/igorpro/python/python-overview.md#python-console). Like any other Igor runtime error, Python runtime errors can be caught in a [try-catch-endtry](/igorpro/programming/keywords/flow-control.md#try-catch-endtry) construct:

```python
# Python
# scriptThatContainsError.py
print('this is missing a parentheses'  # produces a runtime error
```

```igor
// Igor
try
	// Run a script that will produce a syntax error
	PythonFile file = "scriptThatContainsError.py"; AbortOnRTE
catch
	Print GetRTErrMessage()       // print the error message, which indicates SyntaxError
	Variable err = GetRTError(1)  // clear the error	
endtry
```

Any errors that occur during Python execution will be written to the Python Console, and also stored in the *S_PythonError* string.

*V_flag* is set to a non-zero error code if any errors occurred. This can be used to retrieve the traceback message from Python. For example:

```igor
// Run a script that will produce a syntax error
PythonFile/Z file = "scriptThatContainsError.py"
if (V_flag)
	Print S_PythonError
endif
```
### *Examples* {#examples}
Running a Python file with arguments:

```python
# Python
# myScript.py
import sys

def doAnalysis(arg):
	# do analysis routine...
	return arg * 2

if __name__ == '__main__':
	arg1 = float(sys.argv[1])  # convert the argument from a string to a float
	result = doAnalysis(arg1)  # 'result' is a global variable
```

```igor
// Igor	
Variable result
PythonFile file = "myScript.py", var = {"result", result}, args = "3.141"
Print result   // prints 6.282
```

Importing versus executing a Python file:

```python
# Python
# myScript.py
if __name__ == '__main__':
	print('executed script')
else:
	print('imported as a module')
```

```igor
// Igor	
Python execute = "import myScript"  // prints 'imported as a module'
PythonFile file = "myScript.py"     // prints 'executed script'
```

### *See Also* {#see-also}
[Python](/igorpro/commands/python.md), [PythonEnv](/igorpro/commands/pythonenv.md), [Python Overview](/igorpro/python/python-overview.md), [Python Module Reference](/igorpro/python/python-module-reference.md)