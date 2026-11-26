---
description: "The HDF5DumpErrors operation dumps information about HDF5 library errors encountered by Igor."
slug: /commands/hdf5dumperrors
---

<div className="command-signature">

## <strong>HDF5DumpErrors</strong>  [ /CLR=<em>clear</em> /Q ] {#hdf5dumperrors}

</div>

The HDF5DumpErrors operation dumps information about HDF5 library errors encountered by Igor. This information, which will make sense mostly to HDF5 experts, may help debug difficult problems. It is not needed in most cases.

When the HDF5 library returns an error to Igor, Igor stores a general description of the error and further information provided by the HDF5 library's H5E interface. This information is dumped by HDF5DumpErrors.

Starting with Igor Pro 9.00, if you include the /Z flag with an HDF5 operation, errors are not recorded for dumping by HDF5DumpErrors.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | If /Q is omitted, then the output is dumped to Igor's history area and to the S_HDF5ErrorInfo variable. If /Q is present, then output is dumped only to the S_HDF5ErrorInfo variable. |
| /CLR=*clear* |<table class="nested-table"><tbody><tr><td>*clear*&nbsp;=0:</td><td>The error information is not cleared after the dump. This is the default behavior.</td></tr><tr><td>*clear*&nbsp;=1:</td><td>The error information is cleared after the dump.</td></tr></tbody></table>

### *Output Variables* {#output-variables}
HDF5DumpErrors sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
| S_HDF5ErrorInfo | Set to the dump text. |