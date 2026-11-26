# Igor Pro — Language syntax and common traps

Igor's procedure language looks like C/BASIC but differs in ways that generated code often gets
wrong. Read this before writing or fixing any `Function`. For waves/data folders/`$`/DFREF read
`wave-dfref.md`; for graphs read `graphs.md`.

## 1. Operations vs. functions

| | Operations | Functions |
|---|---|---|
| Examples | `Make`, `Display`, `WaveStats`, `CurveFit`, `SetScale`, `Duplicate` | `sin`, `numpnts`, `StringFromList`, `WaveExists` |
| Call syntax | `Name/FLAGS args` - **no parentheses** | `Name(args)` |
| Result | side effect; outputs in `V_`/`S_`/`W_` variables and waves | return value used in an expression |
| Can be inside an expression | **no** | yes |

```igor
WaveStats/Q w          // then use V_avg, V_sdev, V_npnts, V_min, V_max ...
Variable m = V_avg     // NOT: Variable m = WaveStats(w)
```
In a user function, the `V_`/`S_` outputs of an operation become local variables automatically.
`V_flag` is the usual success/status output - check it.

## 2. Flags

- Flags follow the operation name with `/`: `Make/O/D/N=100 w`.
- **A flag value that is an expression or a variable must be in parentheses**:
  `Make/O/D/N=(nPts) w`, `Display/W=(10,10,410,310)`. `Make/N=nPts` is a compile error.
- Flags that take a wave come after the wave they modify in some operations
  (`CurveFit line, yW /X=xW /W=wW /I=1 /D`) - check help for that operation.

## 3. Declarations and functions

```igor
Function/WAVE MakeQ(Variable qmin, Variable qmax, Variable n)   // /WAVE, /S, /DF, /C, or none = numeric
    Make/O/D/N=(n) qW
    qW = qmin * (qmax/qmin)^(p/(n-1))                             // log-spaced Q
    return qW
End
```
- Return type is on the `Function` line (`Function/S` string, `Function/WAVE`, `Function/DF`).
  A plain `Function` returns a number.
- Local types: `Variable`, `String`, `Variable/C`, `int`, `double`, `WAVE`, `WAVE/T`, `DFREF`,
  `NVAR`, `SVAR`. All plain numbers are double, so `7/2` is `3.5`.
- Optional params go in `[ ]` at the end; test with `ParamIsDefault(name)`.
- Do not write new `Macro`/`Proc`/`Window` procedures; use `Function`.
- Globals are created with `Variable/G` / `String/G` and read through `NVAR` / `SVAR`.

## 4. Control flow

```igor
if (a > 0 && b != 0)
    ...
elseif (a == 0)
    ...
else
    ...
endif

Variable i
for (i = 0; i < n; i += 1)        // `i += 1` always works; loop body closed by endfor, no braces
    ...
endfor

for (Variable v : someWave)      // range-based loop over wave values (Igor 9+)
    ...
endfor

do
    ...
while (cond)

switch (n)          // numeric; use strswitch for strings
    case 1:
        ...
        break
    default:
        ...
endswitch
```
No `{ }` blocks, no `then`, no `end if`. `break` / `continue` exist.

## 5. Operators and math traps

| Trap | Correct |
|---|---|
| `%` as modulo | `mod(a, b)` |
| `log(x)` meaning natural log | `log` is **base 10**; natural log is `ln(x)` |
| `x == NaN` | always false; use `numtype(x) == 2` (1 = inf) |
| `x**2` | `x^2` |
| string equality with `==` (`==` is for scalar numbers only) | `CmpStr(a, b) == 0` (case-insensitive by default; `CmpStr(a,b,1)` case-sensitive), or `StringMatch` |

## 6. Strings

- Double quotes only. Concatenate with `+`. Escapes: `\t`, `\r`, `\n`, `\"`, `\\`.
- **`num2str(x)` keeps only 5 significant digits** (`%.5g`). For full precision use
  `num2str(x, "%.15g")` or `sprintf s, "%.6e", x`.
- `str2num(s)` returns NaN on failure.
- Lists are strings: `ItemsInList(list, ";")`, `StringFromList(i, list, ";")`,
  `AddListItem`, `RemoveFromList`, `WhichListItem`.
- Keyword lists: `NumberByKey("KEY", s, ":", ";")`, `StringByKey`, `ReplaceNumberByKey`.

## 7. Waves in expressions

- **`Make` creates single-precision float by default. Use `/D`** for anything numeric that matters.
- Wave assignment is an implicit loop: `w = sin(x)`. Inside it:
  `p` = point index, `x` = **scaled X of the destination wave** (from `SetScale`) - it does
  **not** read a separate X wave. For XY data use the X wave explicitly: `yW = A*exp(-xW[p])`.
- `w[p]` (square brackets) = point index; `w(x)` (parentheses) = X-scaled, interpolated.
- Ranges: `w[0,9] = 0`, `w[10,] = 1`.
- Reading past the end of a wave returns the last point **and** raises an "index out of range"
  error - size waves to match (`numpnts(w)`, `DimSize(w,0)`), or index by X with `w2(x)`.
- 2D: `m[p][q]`, with `q` = column index in assignments; `DimSize(m,1)` for columns.
- `MatrixOP` is fast but has its own syntax (no `p`/`q`, no `x` scaling) - check its help.

## 8. Command line (Igor__execute_command) vs. inside a Function

- On the command line, waves can be named directly; inside a Function every wave/global must be
  declared with `WAVE`/`NVAR`/`SVAR` (see `wave-dfref.md`).
- Multiple statements on one line are separated by `;`. Comments start with `//`.
- Avoid `Execute "..."` in functions except when the command must be built as a string.
- `print` writes to the history; `Abort "message"` stops execution with an alert.

## Reference URLs
- https://docs.wavemetrics.com/igorpro/commands/num2str
- https://docs.wavemetrics.com/igorpro/commands/mod
- https://docs.wavemetrics.com/igorpro/commands/numtype
- https://docs.wavemetrics.com/igorpro/commands/cmpstr
