---
description: "The igorpro Python module provides access to Igor objects and data structures such as waves, data folders, strings, and variables."
slug: /python/python-module-reference
---

# Python Module Reference {#python-module-reference}

The *igorpro* Python module provides access to Igor objects and data structures such as waves, data folders, strings, and variables. Each Igor object type has an associated Python class:

- [igorpro.wave](#igorpro-wave)
- [igorpro.folder](#igorpro-folder)
- [igorpro.variable](#igorpro-variable)
- [igorpro.string](#igorpro-string)

The [igorpro.fn](#igorpro-fn) submodule allows users to directly call and return values from built-in, external, and user-defined Igor functions.

## Methods {#methods}

The following are top-level methods in the *igorpro* Python module:

<div className="command-signature python-method">

## <strong>igorpro.execute</strong> (<em>code</em>, <em>ignoreErrors</em> = <em>False</em>) {#igorpro-execute}

</div>

Executes arbitrary Igor code as if it had been typed in Igor's command line. Equivalent to [Execute](/igorpro/commands/execute.md).

### *Parameters* {#execute-parameters}

|  |  |
| --- | --- |
| *code* | Igor code to execute as a string. |
| *ignoreErrors* | Optional. If True, errors are not fatal and error dialogs are suppressed. |

<div className="command-signature python-method">

## <strong>igorpro.print</strong> (<em>str</em>) {#igorpro-print}

</div>

Prints the input *str* to Igor's command history.

### *Parameters* {#print-parameters}

|  |  |
| --- | --- |
| *str* | String to print. |

<div className="command-signature python-method">

## <strong>igorpro.version</strong> () {#igorpro-version}

</div>

Prints the current build version of the Igor Pro application.

## igorpro.wave {#igorpro-wave}

*igorpro.wave* is the Python representation of an Igor wave object, which is a data array in Igor (see [Waves](/igorpro/igor-basics/waves.md)). This class provides access to various wave-related functions, and allows conversions between Igor waves and other analogous Python types, such as NumPy arrays.

In order to access a pre-existing wave in Igor, use the **igorpro.wave** constructor. If you wish to create a new Igor wave, use [igorpro.wave.create](#igorpro-wave-create) or [igorpro.wave.createfrom](#igorpro-wave-createfrom).

Every *igorpro.wave* has an underlying Igor wave as its source. A *igorpro.wave* doesn't hold a copy of the underlying wave data, only a reference to it, so any changes to the Igor wave will be automatically tracked by the *igorpro.wave*.

Killing an Igor wave out from under Python is permitted, which will result in an exception if Python attempts to use the dead wave. However, deleting the *igorpro.wave* itself has no effect on the underlying Igor wave.

<div className="command-signature python-method">

### <strong>igorpro.wave</strong> (<em>path</em>, <em>folder</em> = <em>None</em>) {#igorpro-wave}

</div>

Constructs a new *igorpro.wave* that refers to an existing Igor wave at *path*.

#### *Parameters* {#wave-parameters}

|  |  |
| --- | --- |
| *path* | Full or relative Igor path to the wave. |
| *folder* | Optional. Parent *igorpro.folder* to retrieve the Igor wave from. If *path* is a relative path, it is based off of this folder. If no data folder is provided, *folder* is interpreted as the current data folder. |

#### *Details* {#wave-details}

Free waves are currently not supported.

#### *Examples* {#wave-examples}

```python
# Getting a reference to an existing Igor wave in the current data folder
foo = igorpro.wave('root:foo')

# Getting a reference to an existing Igor wave (root:data:bar) using folder argument 
dataFolder = igorpro.folder('root:data')
bar = igorpro.wave('bar', dataFolder)
```

<div className="command-signature python-method">

### <strong>igorpro.wave.create</strong> (<em>name</em>, <em>shape</em> = (,), <em>value</em> = <em>None</em>, <em>type</em> = <em>igorpro</em>.<em>float32</em>, <em>folder</em> = <em>None</em>, <em>overwrite</em> = <em>False</em>) {#igorpro-wave-create}

</div>

Creates a new Igor wave relative to the current data folder, and returns a *igorpro.wave*. See [Make](/igorpro/commands/make.md).

#### *Parameters* {#wave-create-parameters}

|  |  |
| --- | --- |
| *name* | Name of the wave. This can include a full or relative path, in order to create the Igor wave in a specific location. Otherwise, it will be created in the current data folder. |
| *shape* | Optional. Tuple containing the size of each dimension, or a single number specifying the number of points for a 1D wave. Default is a 1D, 128 point wave. |
| *value* | Optional. Value to fill the new wave with. Default is *None*, which will resolve to 0 for numeric waves, an empty string for text waves, or a null wave for wave reference and data folder reference waves. |
| *type* | Optional. Data type for the wave. If not specified, the wave type will be inferred from the *value* argument. If *value* was not specified either, the wave type will default to 32 bit floating point. |
| *folder* | *igorpro.folder* to create the wave in. If *name* is a relative path, it is based off of this folder. If no data folder is provided, *folder* it is interpreted as the current data folder. |
| *overwrite* | Optional. Overwrite the wave if it already exists. |

#### *Details* {#wave-create-details}
This method is static, and thus is intended to be called without an instance of *igorpro.wave*. Calling it from an existing *igorpro.wave* instance will have no effect on the wave creation or parameters.

The wave type will be inferred if it isn't specified using the *type* argument. In this case, if *value* was specified, the wave type will be the same as *value*. If neither type nor value was specified, the wave will be a 32 bit floating point wave. 

#### *Examples* {#wave-create-examples}

```python
# Create an Igor wave with default settings
# 128 points, 32 bit float
w = igorpro.wave.create('defaultWave')

# Create an Igor 2D wave 100 x 200, filled with the value 3.141, as a 64 bit float wave type
w = igorpro.wave.create('customWave', (100,200), 3.141, igorpro.float64)

# Overwriting an existing wave, 50 x 100, filled with the value 100
w = igorpro.wave.create('customWave', (50,100), value = 100, overwrite = True)
```

<div className="command-signature python-method">

### <strong>igorpro.wave.createfrom</strong> (<em>name</em>, <em>source</em>, <em>folder</em> = <em>None</em>, <em>overwrite</em> = <em>False</em>) {#igorpro-wave-createfrom}

</div>

Creates a new Igor wave from a source array-like object. Acceptable array-like objects include Python arrays, NumPy arrays, lists, and tuples. The array data is copied into a new Igor wave, which will then be accessible in the data browser.

#### *Parameters* {#wave-createfrom-parameters}

|  |  |
| --- | --- |
| *name* | Name of the wave. This can include a full or relative path, in order to create the Igor wave in a specific location. Otherwise, it will be created in the current data folder. |
| *source* | Source array-like object. Can be a *numpy* array, built-in Python array (*array.array*), *list*, or *tuple*. Lists, tuples, and NumPy object arrays may contain *igorpro.wave* or *igorpro.folder* objects. |
| *folder* | *igorpro.folder* to create the wave in. If *name* is a relative path, it is based off of this folder. If no data folder is provided, *folder* it is interpreted as the current data folder. |
| *overwrite* | Optional. Overwrite the wave if it already exists. |

#### *Details* {#wave-createfrom-details}
The underlying data types of the input array will be converted into the most appropriate Igor wave type, or raise an exception if the data type cannot be converted. A collection of *igorpro.wave* objects creates a wave reference wave, and a collection of *igorpro.folder* objects creates a data folder reference wave. Arrays with mixed data types are not supported.

An *igorpro.wave* or *igorpro.folder* whose underlying Igor object no longer exists, including an unsupported free object, is stored as a null reference.

For creating a NumPy array from an Igor wave, see [asarray](#asarray).

#### *Examples* {#wave-createfrom-examples}

```python
import numpy as np

# Create a wave from a NumPy array of a sine wave 
sinwave = np.sin([2 * x * np.pi/256 for x in range(256)])
w = igorpro.wave.createfrom('data', sinwave)

# Create a wave reference wave from a list of Igor waves
sourceWaves = [igorpro.wave.create(f'source{x}') for x in range(3)]
waveRefs = igorpro.wave.createfrom('waveRefs', sourceWaves)

# Create a data folder reference wave from a NumPy object array
sourceFolders = np.array([igorpro.folder('root'), igorpro.folder.create('data')], dtype=object)
folderRefs = igorpro.wave.createfrom('folderRefs', sourceFolders)
```

### Methods {#igorpro-wave-methods}
<div className="command-signature python-method">

### <strong>asarray</strong> () → <em class=returnType>numpy</em>.<em class=returnType>ndarray</em> {#asarray}

</div>

Creates a NumPy array from the Igor wave, with the same dimensionality and data type.

#### *Details* {#asarray-details}
Since the NumPy array holds a copy of the wave data, any subsequent change to the Igor wave will have no effect on the new NumPy array. However, the NumPy array will not carry any of the Igor wave's meta-data, such as it's scaling, units, or note.

:::warning
*asarray()* only works for numeric and text waves.
:::


For creating an Igor wave from a NumPy array, see [igorpro.wave.createfrom](#igorpro-wave-createfrom).

#### *Examples* {#wave-examples}

```python
import numpy as np

# Get a reference to an existing Igor wave in the current data folder
foo = igorpro.wave('root:foo')

# Create a numpy array copy from the Igor wave
fooCopy = foo.asarray()
```

<div className="command-signature python-method">

### <strong>dims</strong> () → <em class=returnType>int</em> {#dims}

</div>

Returns the number of dimensions in the Igor wave. See [WaveDims](/igorpro/commands/wavedims.md).

<div className="command-signature python-method">

### <strong>exists</strong> () → <em class=returnType>bool</em> {#exists}

</div>

Returns the truth that the underlying Igor wave exists. See [WaveExists](/igorpro/commands/waveexists.md).

<div className="command-signature python-method">

### <strong>kill</strong> () → <em class=returnType>None</em> {#kill}

</div>

Kills the Igor wave if it isn't in use.

<div className="command-signature python-method">

### <strong>labels</strong> (<em>dimension</em>) → <em class=returnType>list</em> {#labels}

</div>

Returns a list of the wave's dimension labels for the specified dimension. See [GetDimLabel](/igorpro/commands/getdimlabel.md).

#### *Parameters* {#labels-parameters}

|  |  |
| --- | --- |
| *dimension* | Dimension number to get the dimension labels for (0-3). The characters 'x', 'y', 'z', and 't' are also accepted. To get the labels for the overall dimension, use -1 or 'd'. |

<div className="command-signature python-method">

### <strong>name</strong> () → <em class=returnType>str</em> {#name}

</div>

Returns the name of the Igor wave as a string, without its path.

<div className="command-signature python-method">

### <strong>note</strong> () → <em class=returnType>str</em> {#note}

</div>

Returns the Igor wave's note as a string. See [Functions[note]](/igorpro/commands/note_function.md).

<div className="command-signature python-method">

### <strong>path</strong> () → <em class=returnType>str</em> {#path}

</div>

Returns the full path to the Igor wave as a string, without the name. See [GetWavesDataFolder](/igorpro/commands/getwavesdatafolder.md).

<div className="command-signature python-method">

### <strong>points</strong> () → <em class=returnType>int</em> {#points}

</div>

Returns the number of points in the Igor wave. See [numpnts](/igorpro/commands/numpnts.md)

<div className="command-signature python-method">

### <strong>redimension</strong> (<em>shape</em>) → <em class=returnType>None</em> {#redimension}

</div>

Changes the shape of the Igor wave. See [Operations[Redimension]](/igorpro/commands/redimension.md).

#### *Parameters* {#redimension-parameters}

|  |  |
| --- | --- |
| *shape* | Requested dimensions for the wave. This can be either a tuple of numbers that specify the number of points in each dimension of a multi-dimensional wave, or a single number specifying the number of points in a 1D wave. |

<div className="command-signature python-method">

### <strong>scale</strong> (<em>dimension</em>) → <em class=returnType>tuple</em> {#scale}

</div>

Returns a tuple containing the scaling offset (start value) and delta for the indicated *dimension*.

#### *Parameters* {#scale-parameters}

|  |  |
| --- | --- |
| *dimension* | Dimension number to set the scale of. The characters 'x', 'y', 'z', and 't' are also accepted. |

<div className="command-signature python-method">

### <strong>set_data</strong> (<em>source</em>) → <em class=returnType>None</em> {#set_data}

</div>

Sets the wave data as *source*.

#### *Parameters* {#set-data-parameters}

|  |  |
| --- | --- |
| *source* | Data source to set the wave with. This can be another *igorpro.wave*, or a supported array-like object (*NumPy* array, built-in Python array (*array.array*), *list*, or *tuple*). Lists, tuples, and NumPy object arrays may contain *igorpro.wave* or *igorpro.folder* objects. |

#### *Details* {#set-data-details}
If an array-like object is used as *source*, the wave data (including the dimensions) will be set to that of the *source* as long as the *source* data and the wave have compatible types (See [Python to Igor type conversions](/igorpro/python/python-overview.md#python-to-igor-type-conversions)). For example, conversions between text waves and numeric arrays will throw an exception. Complex waves, real numeric waves, text waves, wave reference waves, and data folder reference waves generally do not inter-convert. However, conversions between numeric types, such as unsigned 8 bit integer to 64 bit floating point, are allowed. 
In these cases, the wave data type will never change to accomodate the *source* data. Instead, the *source* data will be converted into the destination wave's data type. 

A collection of *igorpro.wave* objects can be assigned to a wave reference wave, and a collection of *igorpro.folder* objects can be assigned to a data folder reference wave. The collection must contain only one object type. An object whose underlying Igor object no longer exists, including an unsupported free object, is stored as a null reference.

If an *igorpro.wave* is used as *source*, the same rules apply for converting the *source* data into the destination wave's data type.

#### *Example* {#set-data-example}

```python
import numpy as np
# Create a default 1D wave
w = igorpro.wave.create('dd')

# Create a 2D NumPy array of random values
a = np.random.rand(128, 128)

# Set the wave's data to the NumPy array
w.set_data(a)

# Set the wave's data to a list
w.set_data([np.sin(2 * np.pi * x/50) for x in range(50)])

# Set a wave reference wave from a list of Igor waves
sourceWaves = [igorpro.wave.create(f'source{x}') for x in range(3)]
waveRefs = igorpro.wave.create('waveRefs', 3, type=igorpro.wref)
waveRefs.set_data(sourceWaves)
```
<div className="command-signature python-method">

### <strong>set_label</strong> (<em>dimension</em>, <em>index</em>, <em>label</em>) → <em class=returnType>None</em> {#set_label}

</div>

Sets the wave's dimension label at the specified *dimension* and *index*. See [SetDimLabel](/igorpro/commands/setdimlabel.md).

#### *Parameters* {#set-label-parameters}

|  |  |
| --- | --- |
| *dimension* | Dimension number (0-3). The characters 'x', 'y', 'z', and 't' are also accepted. |
| *index* | Index along the specified *dimension* to set the label. Use -1 to set the overall dimension label. |
| *label* | Label string to set. |

<div className="command-signature python-method">

### <strong>set_note</strong> (<em>note</em>, <em>append</em> = <em>False</em>) → <em class=returnType>None</em> {#set_note}

</div>

Sets the Igor wave's note. See [Operations[Note]](/igorpro/commands/note_operation.md).

#### *Parameters* {#set-note-parameters}

|  |  |
| --- | --- |
| *note* | Note string to set. |
| *append* | Optional. If True, appends the new note to the existing note. Otherwise, the existing note is replaced. |

<div className="command-signature python-overload overload">

### <strong>set_scale</strong> (<em>dimension</em>, <em>start</em>, <em>value</em>, <em>mode</em> = '<em>default</em>') → <em class=returnType>None</em> {#set_scale}

</div>

<div className="command-signature python-method">

### <strong>set_scale</strong>  (<em>wave</em>, <em>mode</em>) → <em class=returnType>None</em> {#set_scale}

</div>

Sets the wave scaling for the indicated dimension or given wave. See [SetScale](/igorpro/commands/setscale.md) and [CopyScales](/igorpro/commands/copyscales.md).

#### *Parameters* {#set-scale-parameters}

|  |  |
| --- | --- |
| *dimension* | Dimension number to set the scale of. The characters 'x', 'y', 'z', and 't' are also accepted. |
| *start* | Start value (offset) for the dimension scaling. |
| *value* | End value or delta value for the dimension scaling, depending on the *mode*. |
| *mode* | *'range'* : *value* is the end value for the *dimension*.<br>*'delta'* : *value* is the delta value between points for the *dimension*. |
| *wave* | Source *igorpro.wave*. The wave scaling for all dimensions are copied from the provided wave. |

#### *Details* {#set-scale-details}
*mode = 'range'* corresponds to the Igor procedure code *SetScale /I*, whereas *mode = 'delta'* corresponds to *SetScale /P*. If *mode = 'range'*, the delta value between points will be automatically calculated. 

<div className="command-signature python-overload overload">

### <strong>set_units</strong> (<em>dimension</em>, <em>unit</em>) → <em class=returnType>None</em> {#set_units}

</div>

<div className="command-signature python-method">

### <strong>set_units</strong> (<em>wave</em>) → <em class=returnType>None</em> {#set_units}

</div>

Sets the wave's unit string for the indicated dimension. See [SetScale](/igorpro/commands/setscale.md).

#### *Parameters* {#set-units-parameters}

|  |  |
| --- | --- |
| *dimension* | Dimension number to set the unit string for (0-3). The characters 'x', 'y', 'z', and 't' are also accepted. To set the unit string for the data dimension, use -1 or 'd'. |
| *unit* | Unit string to set. |
| *wave* | Source *igorpro.wave*. The unit strings for all dimensions are copied from the source wave. |

<div className="command-signature python-method">

### <strong>shape</strong> () → <em class=returnType>tuple</em> {#shape}

</div>

Returns a tuple with the size of each dimension in the Igor wave.

<div className="command-signature python-method">

### <strong>stats</strong> (<em>xRange</em>, <em>yRange</em>, <em>zRange</em>, <em>tRange</em>) → <em class=returnType>dict</em> {#stats}

</div>

Returns the statistics of the Igor wave as a dictionary. See [WaveStats](/igorpro/commands/wavestats.md).

#### *Parameters* {#stats-parameters}

|  |  |
| --- | --- |
| *xRange* | Optional. List or tuple containing the start and end points in the range for the x dimension. |
| *yRange* | Optional. List or tuple containing the start and end points in the range for the y dimension. |
| *zRange* | Optional. List or tuple containing the start and end points in the range for the z dimension. |
| *tRange* | Optional. List or tuple containing the start and end points in the range for the t dimension. |

#### *Details* {#stats-details}
Each range argument can either be a tuple () or a list []. If a tuple is used, this method will treat the range as scaled values for the given dimension. If a list is used, this method treats the range values as point indices. Omit all arguments to calculate the statistics of the entire wave. Use an '...' ellipsis input to specify the boundary of any dimension.

#### *Example* {#stats-example}

```python
# Performs stats() on all rows up to and including row 3,
# for columns 5-10, inclusive.
stats = igorpro.stats([..., 3],[5, 10])
```

<div className="command-signature python-method">

### <strong>type</strong> () → <em class=returnType>igorpro</em>.<em class=returnType>WaveType</em> {#type}

</div>

Returns the Igor wave type as a *WaveType* enumerator. See [igorpro.WaveType](#igorpro-wavetype)

<div className="command-signature python-method">

### <strong>units</strong> (<em>dimension</em>) → <em class=returnType>str</em> {#units}

</div>

Returns the unit string for the specified dimension.

#### *Parameters* {#units-parameters}

|  |  |
| --- | --- |
| *dimension* | Dimension number (0-3). The characters 'x', 'y', 'z', and 't' are also accepted. To set the unit string for the data dimension, use -1 or 'd'. |

### Indexing {#indexing}

**[ row, column, layer, chunk ]**  *→ object*

Subscript operator. Returns the contained value at the given index.

**[ row, column, layer, chunk ]** *= value*

Subscript assignment operator. Assigns *value* to given index.

## igorpro.WaveType {#igorpro-wavetype}

Enumeration of the possible data types for an *igorpro.wave*:

|  |  |
| --- | --- |
| *none* | Invalid type |
| *text* | Text wave |
| *float32* | 32 bit floating point |
| *float64* | 64 bit floating point |
| *int8* | 8 bit signed integer |
| *uint8* | 8 bit unsigned integer |
| *int16* | 16 bit signed integer |
| *uint16* | 16 bit unsigned integer |
| *int32* | 32 bit signed integer |
| *uint32* | 32 bit unsigned integer |
| *complex64* | 32 bit floating point, complex |
| *complex128* | 64 bit floating point, complex |
| *wref* | Wave reference |
| *dfref* | Data folder reference |

These can be accessed as, for example:
```python
igorpro.float32
```
or
```python
igorpro.WaveType.float32
```

## igorpro.folder {#igorpro-folder}

*igorpro.folder* is the Python representation of an Igor data folder (see [Data Folders](/igorpro/igor-basics/data-folders.md)). This class allows users to access all Igor objects within a data folder, and provides methods for navigating through Igor's folder hierarchy (see [The Data Browser](/igorpro/igor-basics/data-folders.md#the-data-browser)).

<div className="command-signature python-method">

### <strong>igorpro.folder</strong> (<em>path</em>, <em>folder</em> = <em>None</em>) → <em class=returnType>igorpro</em>.<em class=returnType>folder</em> {#igorpro-folder}

</div>

Constructs a new *igorpro.folder* that refers to an existing Igor data folder at *path*.

#### *Parameters* {#folder-parameters}

|  |  |
| --- | --- |
| *path* | Full or relative Igor path to the data folder. |
| *folder* | Optional. Parent *igorpro.folder* to retrieve the Igor data folder from. If *path* is a relative path, it is based off of this folder. If no data folder is provided, *folder* is interpreted as the current data folder. |

#### *Details* {#folder-details}
*igorpro.folder* provides access to an existing Igor data folder and its contents. Free data folders are currently not supported. The existence of a *igorpro.folder* does not prevent its underlying Igor data folder from being deleted. If a *igorpro.folder* attempts to use a data folder that has been deleted, it will raise an exception. A *igorpro.folder* doesn't directly hold the underlying data folder data, so any changes to the Igor data folder will be tracked by the *igorpro.folder*.

<div className="command-signature python-method">

### <strong>igorpro.folder.create</strong> (<em>path</em>, <em>overwrite</em> = <em>False</em>) → <em class=returnType>igorpro</em>.<em class=returnType>folder</em> {#igorpro-folder-create}

</div>

Creates a new Igor data folder at *path*. See [NewDataFolder](/igorpro/commands/newdatafolder.md).

#### *Parameters* {#folder-create-parameters}

|  |  |
| --- | --- |
| *path* | Full or relative Igor path to the data folder. |
| *overwrite* | Optional. Overwrite the folder if it already exists. Note, setting *overwrite* to *True* won't delete the contents of the folder. |

#### *Details* {#folder-create-details}
This method is static, and thus is intended to be called without an instance of *igorpro.folder*. Calling it from an existing *igorpro.folder* instance will have no effect on the folder creation or parameters.

<div className="command-signature python-method">

### <strong>igorpro.folder.current</strong> () → <em class=returnType>igorpro</em>.<em class=returnType>folder</em> {#igorpro-folder-current}

</div>

Gets the current data folder and returns it as a *igorpro.folder*.

### Methods {#igorpro-folder-methods}

<div className="command-signature python-method">

### <strong>exists</strong> ()  → <em class=returnType>bool</em> {#exists}

</div>

Returns the truth that the underlying Igor data folder exists. See [DataFolderExists](/igorpro/commands/datafolderexists.md).

<div className="command-signature python-method">

### <strong>kill</strong> (<em>ignoreErrors</em> = <em>False</em>)  → <em class=returnType>None</em> {#kill}

</div>

Kills the Igor data folder, if possible. See [KillDataFolder](/igorpro/commands/killdatafolder.md).

#### *Parameters* {#kill-parameters}

|  |  |
| --- | --- |
| *ignoreErrors* | If True, ignores errors if the folder doesn't exist. |

<div className="command-signature python-method">

### <strong>name</strong> ()  → <em class=returnType>str</em> {#name}

</div>

Returns the name of the Igor data folder.

<div className="command-signature python-method">

### <strong>num_subfolders</strong> ()  → <em class=returnType>int</em> {#num_subfolders}

</div>

Returns the number of subfolders inside the Igor data folder.

<div className="command-signature python-method">

### <strong>num_waves</strong> ()  → <em class=returnType>int</em> {#num_waves}

</div>

Returns the number of waves inside the Igor data folder.

<div className="command-signature python-method">

### <strong>parent</strong> ()  → <em class=returnType>igorpro</em>.<em class=returnType>folder</em> {#parent}

</div>

Returns the parent *igorpro.folder*.

#### *Details* {#parent-details}
Calling *parent()* on the root directory will return the root directory itself.

<div className="command-signature python-method">

### <strong>path</strong> ()  → <em class=returnType>str</em> {#path}

</div>

Returns the full path to the Igor data folder.

<div className="command-signature python-method">

### <strong>set</strong> ()  → <em class=returnType>None</em> {#set}

</div>

Sets the Igor data folder as the current data folder.

<div className="command-signature python-method">

### <strong>subfolder</strong> (<em>name</em>)  → <em class=returnType>igorpro</em>.<em class=returnType>folder</em> {#subfolder}

</div>

Returns the named subfolder in the Igor data folder as a *igorpro.folder*, if it exists.

<div className="command-signature python-method">

### <strong>subfolders</strong> ()  → <em class=returnType>list</em> {#subfolders}

</div>

Returns a list of the immediate subfolders in the Igor data folder as a list of *igorpro.folders*.

<div className="command-signature python-method">

### <strong>waves</strong> ()  → <em class=returnType>list</em> {#waves}

</div>

Returns a list of the waves inside the Igor data folder as a list of *igorpro.waves*.

## igorpro.string {#igorpro-string}

*igorpro.string* is the Python representation of an Igor string variable. This class provides methods for reading and writing to global Igor string variables.

<div className="command-signature python-method">

### <strong>igorpro.string</strong> (<em>path</em>, <em>folder</em> = <em>None</em>) {#igorpro-string}

</div>

Constructs a new *igorpro.string* that refers to an existing Igor string variable at *path*.

#### *Parameters* {#string-parameters}

|  |  |
| --- | --- |
| *path* | Full or relative Igor path to the string variable, including its name. |
| *folder* | Optional. Parent *igorpro.folder* to retrieve the Igor string variable from. If *path* is a relative path, it is based off of this folder. If no data folder is provided, *folder* is interpreted as the current data folder. |

<div className="command-signature python-method">

### <strong>igorpro.string.create</strong> (<em>path</em>, <em>value</em>, <em>folder</em> = <em>None</em>, <em>overwrite</em> = <em>False</em>) {#igorpro-string-create}

</div>

Creates a new Igor string at *path*, and returns a *igorpro.string*. See [String](/igorpro/commands/string.md).

#### *Parameters* {#string-create-parameters}

|  |  |
| --- | --- |
| *path* | Full or relative Igor path to the string variable, including its name. |
| *value* | String to set the variable to. |
| *folder* | Optional. *igorpro.folder* to create the string variable in. If *name* is a relative path, it is based off of this folder. If no data folder is provided, *folder* it is interpreted as the current data folder. |
| *overwrite* | Optional. Overwrite the string variable if it already exists. |

#### *Details* {#string-create-details}
This method is static, and thus is intended to be called without an instance of *igorpro.string*. Calling it from an existing *igorpro.string* instance will have no effect on the string creation or parameters.

### Methods {#igorpro-string-methods}

<div className="command-signature python-method">

### <strong>exists</strong> () → <em class=returnType>bool</em> {#exists}

</div>

Returns the truth that the underlying Igor string variable exists. See [SVAR_Exists](/igorpro/commands/svar_exists.md).

<div className="command-signature python-method">

### <strong>name</strong> () → <em class=returnType>str</em> {#name}

</div>

Returns the name of the Igor string variable.

<div className="command-signature python-method">

### <strong>path</strong> () → <em class=returnType>str</em> {#path}

</div>

Returns the full path to the Igor string variable.

<div className="command-signature python-method">

### <strong>set</strong> (<em>str</em>) → <em class=returnType>None</em> {#set}

</div>

Sets the value of the Igor string variable.

#### *Parameters* {#string-set-parameters}

|  |  |
| --- | --- |
| *str* | New value for the Igor string variable. |

<div className="command-signature python-method">

### <strong>value</strong> () → <em class=returnType>str</em> {#value}

</div>

Returns the value of the string.

## igorpro.variable {#igorpro-variable}

*igorpro.variable* is the Python representation of an Igor numeric variable. This class provides methods for reading and writing to global Igor numeric variables.

<div className="command-signature python-method">

### <strong>igorpro.variable</strong> (<em>path</em>, <em>folder</em> = <em>None</em>) {#igorpro-variable}

</div>

Constructs a new *igorpro.variable* that refers to an existing Igor numeric variable at *path*.

#### *Parameters* {#variable-parameters}

|  |  |
| --- | --- |
| *path* | Full or relative Igor path to the numeric variable, including its name. |
| *folder* | Optional. Parent *igorpro.folder* to retrieve the Igor numeric variable from. If *path* is a relative path, it is based off of this folder. If no data folder is provided, *folder* is interpreted as the current data folder. |

<div className="command-signature python-method">

### <strong>igorpro.variable.create</strong> (<em>path</em>, <em>value</em>, <em>folder</em> = <em>None</em>, <em>overwrite</em> = <em>False</em>) {#igorpro-variable-create}

</div>

Creates a new Igor numeric variable at *path*, and returns a *igorpro.variable*. See [Variable](/igorpro/commands/variable.md).

#### *Parameters* {#variable-create-parameters}

|  |  |
| --- | --- |
| *path* | Full or relative Igor path to the numeric variable, including its name. |
| *value* | Real or complex number to set the variable to. If a complex number is provided, a complex Igor variable will be created. Otherwise, a non-complex variable is created. |
| *folder* | Optional. *igorpro.folder* to create the numeric variable in. If *name* is a relative path, it is based off of this folder. If no data folder is provided, *folder* it is interpreted as the current data folder. |
| *overwrite* | Optional. Overwrite the variable if it already exists. |

#### *Details* {#variable-create-details}
This method is static, and thus is intended to be called without an instance of *igorpro.variable*. Calling it from an existing *igorpro.variable* instance will have no effect on the variable creation or parameters.

### Methods {#igorpro-variable-methods}

<div className="command-signature python-method">

### <strong>exists</strong> () → <em class=returnType>bool</em> {#exists}

</div>

Returns the truth that the underlying Igor numeric variable exists. See [NVAR_Exists](/igorpro/commands/nvar_exists.md).

<div className="command-signature python-method">

### <strong>imag</strong> () → <em class=returnType>int</em> | <em class=returnType>float</em> {#imag}

</div>

Returns the imaginary part of the complex number.

<div className="command-signature python-method">

### <strong>iscomplex</strong> () → <em class=returnType>bool</em> {#iscomplex}

</div>

Returns the truth that the Igor numeric variable is a complex type.

<div className="command-signature python-method">

### <strong>name</strong> () → <em class=returnType>str</em> {#name}

</div>

Returns the name of the Igor numeric variable.

<div className="command-signature python-method">

### <strong>path</strong> () → <em class=returnType>str</em> {#path}

</div>

Returns the full path to the Igor numeric variable.

<div className="command-signature python-method">

### <strong>real</strong> () → <em class=returnType>int</em> | <em class=returnType>float</em> {#real}

</div>

Returns the real part of the complex numberic variable.

#### *Details* {#real-details}
If the variable is not complex, this method returns *value()*.

<div className="command-signature python-method">

### <strong>set</strong> (<em>value</em>) → <em class=returnType>None</em> {#set}

</div>

Sets the value of the Igor numeric variable.

#### *Parameters* {#variable-set-parameters}

|  |  |
| --- | --- |
| *value* | New value for the Igor numeric variable, which can be a real or a complex number. |

#### *Details* {#variable-set-details}
If the variable is complex, but *value* is not, the real part will be set to *value*, and the imaginary part will be set to 0. If the variable is not complex, but *value* is complex, an *invalid data type* exception will be thrown.

<div className="command-signature python-method">

### <strong>value</strong> () → <em class=returnType>int</em> | <em class=returnType>float</em> {#value}

</div>

Returns the value of the Igor numeric variable.


## igorpro.fn {#igorpro-fn}

`igorpro.fn` is a submodule in the `igorpro` Python module. It is used for calling built-in, external, or user-defined Igor functions directly from Python. Using this submodule, you can take advantage of Igor's vast library of functionality while using natural Python syntax.

For example, to use Igor's built-in [SortList](/igorpro/commands/sortlist.md) function:

```python
# Descending sort. 'sorted' will hold: 'a;c;d;e;g;x;'
sorted : str = igorpro.fn.sortlist('x;c;e;g;d;a', ';', 1)
```

:::note
Although Python is case-sensitive, Igor is not, so function calls made through `igorpro.fn` do not need to be case-sensitive. 
For example, the following calls to Igor's SortList function are equivalent:
:::

```python
sorted : str = igorpro.fn.SortList('x;c;e;g;d;a', ';', 1)
sorted : str = igorpro.fn.sortlist('x;c;e;g;d;a', ';', 1)
```

#### Arguments {#arguments}

The arguments to an Igor function can be provided normally, as if a Python method were being called. These arguments are interpreted according to their Python type. For instance, arguments that are an `igorpro.wave` are passed to Igor as wave references, so the following code is acceptable:

```python
import numpy as np

# Create a wave with random data
w = igorpro.wave.createfrom('randomValues', np.random.rand(100))

# Pass in the igorpro.wave directly to call Igor's built-in 'median' function
medianValue = igorpro.fn.median(w)
```

Here, the return type `medianValue` is a Python `float` and can be used directly.

If an `igorpro.folder` is provided as an argument, it is interpreted as a data folder reference (see [DFREF](/igorpro/programming/keywords/object-reference-keywords.md#dfref)), while the `igorpro.string` and `igorpro.variable` classes are passed in using their underlying values.

#### Return values {#return-values}

Igor functions are capable of returning real or complex numeric values, strings, wave references, and data folder references. `igorpro.fn` allows users to return these types back to Python.

For example, you might use Igor's [TraceNameToWaveRef](/igorpro/commands/tracenametowaveref.md) function to return a wave reference to the named trace on a graph:

```python
# Assuming a graph name 'Graph0' exists with a trace called 'yWave'
traceWave = igorpro.fn.traceNameToWaveRef('Graph0', 'yWave')
```

Here, since the Igor function returns a wave reference, an `igorpro.wave` instance is returned to Python. Similarly, data folder references are returned to Python as `igorpro.folder` instances. Strings and variables are returned as their native Python types, whether that be `str`, `float`, or `complex`. For example, Igor's `cmplx` function returns a complex number to Python:

```python
# 'c' is <class 'complex'>, and holds (3-4j)
c = igorpro.fn.cmplx(3, -4)
```

#### Errors {#errors}

If the Igor function does not exist, it will return an `IgorException` explaining that the function could not be found.

#### Calling User Functions {#calling-user-functions}

Consider the Igor user function:

```igor
function displayWaves(Wave xWave, Wave yWave)
    Display yWave vs xWave
end
```

This can be called from Python with:

```python
import numpy as np

# Create some example data to plot
xWave = igorpro.wave.createfrom('xWave', [x for x in range(100)])
yWave = igorpro.wave.createfrom('yWave', np.random.rand(100))

# Call the Igor function with igorpro.wave as the arguments
igorpro.fn.displayWaves(xWave, yWave)
```

#### Calling User Functions inside Igor modules {#calling-user-functions-inside-igor-modules}

Since Igor Pro 10.03, user functions that are defined in regular or independent modules can also be called directly from Python. For the example independent module function:

```igor
#pragma independentModule = Analysis

function processData()
    ... // process data
    return result
end
```

This can be called in Python using:

```python
result = igorpro.fn.analysis.processData()
```

Regular module functions that are defined inside an independent module can also be called in a similar way. For example:

```igor
#pragma independentModule = Analysis
#pragma moduleName = Imaging

static function processImageData()
    ... // process data
    return result
end
```

This can be called in Python using:

```python
result = igorpro.fn.analysis.imaging.processImageData()
```

See [Procedure Modules](/igorpro/advanced-topics.md#procedure-modules)

#### Optional Arguments in User Functions {#optional-arguments-in-user-functions}

When calling optional arguments in a user function, you must use `keyword = value` syntax, just like you would if you were executing the function using Igor code. Consider the following Igor user function:

```igor
// This Igor function takes in one required argument, and a second optional argument
function greet(String name, [String optionalPlace])
    if (ParamIsDefault(optionalPlace))
        print "Hello " + name + "!"
    else
        print "Hello " + name + " from " + optionalPlace + "!"
    endif
end
```

To call this with or without the optional argument from Python:

```python
# Not using optional argument
igorpro.fn.greet('Igor')  # prints 'Hello Igor!'

# Using optional argument with keyword = value syntax
igorpro.fn.greet('Igor', optionalPlace = 'WaveMetrics') # prints 'Hello Igor from WaveMetrics!'
```

#### Limitations {#limitations}

- `igorpro.fn` cannot call Igor functions that take in [Object Names](/igorpro/igor-basics/using-igor.md#object-names), [Pass-By-Reference](/igorpro/programming/programming.md#pass-by-reference) variables, Structures (see [Structures In Functions](/igorpro/programming/programming.md#structures-in-functions)), or use [Multiple Return Syntax](/igorpro/programming/programming.md#multiple-return-syntax). For example, the [CsrInfo](/igorpro/commands/csrinfo.md) function takes in an object name, which is distinct from a string object, so currently this is not permitted:

    ```python
    info = igorpro.fn.CsrInfo(A)
    ```

- Calling Igor functions that take in `FUNCREF` arguments are not supported.

- Python can't hold references to free waves or free data folders. Calling Igor functions that return these will either throw an exception or result
in an empty `igorpro.wave` or `igorpro.folder`, which may be unexpected behavior. 

- Any Igor code that is not callable via Igor's command line will not be callable through the `igorpro.fn` module.

- The Igor functions [p](/igorpro/commands/p.md), [q](/igorpro/commands/q.md), [r](/igorpro/commands/r.md), [s](/igorpro/commands/s.md), [x](/igorpro/commands/x.md), [y](/igorpro/commands/y.md), [z](/igorpro/commands/z.md), [t](/igorpro/commands/t.md) cannot be used, since they can only be used inside a wave assignment loop.

- `igorpro.fn` cannot call Igor operations directly. To do this, either wrap the operation call in an Igor function, or use [igorpro.execute](#igorpro-execute)