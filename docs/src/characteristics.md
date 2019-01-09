This package provides extended precision versions of `Float64`, `Float32`, `Float16`.

| type name   | significand precision | exponent precision | | base type |significand precision  | exponent precision |
|:------------|:---------------------:|:------------------:|-|:----------|:---------------------:|:------------------:|
| `Double64`  | 106 bits              | 11 bits            |◊| `Float64` | 53 bits               | 11 bits            |
| `Double32`  | &nbsp;48 bits         | &nbsp;8 bits       |◊| `Float32` | 24 bits               | &nbsp;8 bits       |
| `Double16`  | &nbsp;22 bits         | &nbsp;5 bits       |◊| `Float16` | 11 bits               | &nbsp;5 bits       |

----

- arithmetic (`+`, `-`, `*`, `/`) is exact
- elementary functions are quite accurate
- often better than C "double-double" libraries

----

For `Double64` arguments within 0.0..2.0   
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; _except tan(x), cot(x) as they approach ±Inf_
- expect the `abserr` of elementary functions to be 1e-30 or less
- expect the `relerr` of elementary functions to be 1e-28 or less

----

When used with reasonably sized values, expect successive DoubleFloat ops to add no more than 10⋅𝘂²
to the cumulative relative error (𝘂 is the relative rounding unit, usually `𝘂 = eps(x)/2`).
Relative error can accrue steadily. After 100_000 DoubleFloat ops with reasonably sized values,
the `relerr` could approach 100_000 * 10⋅𝘂². In practice these functions are considerably
more resiliant: our algorithms come frome seminal papers and extensive numeric investigation.

&nbsp;
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; _should you encounter a situation where either error grows
   strongly in one direction, please submit an issue_