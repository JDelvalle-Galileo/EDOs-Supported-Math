## Supported LaTeX

Only a small subset of LaTeX expressions are suported so far. However,
these are enough to define a very wide set of mathematical functions.

### Greek letters supported

The following greek letters are supported as identifiers (variable
names).

``` r
latex2r:::get_pkg_data('GREEK_KEYWORDS')
#>  [1] "\\alpha"      "\\theta"      "\\tau"        "\\beta"       "\\vartheta"  
#>  [6] "\\pi"         "\\upsilon"    "\\gamma"      "\\varpi"      "\\phi"       
#> [11] "\\delta"      "\\kappa"      "\\rho"        "\\varphi"     "\\epsilon"   
#> [16] "\\lambda"     "\\varrho"     "\\chi"        "\\varepsilon" "\\mu"        
#> [21] "\\sigma"      "\\psi"        "\\zeta"       "\\nu"         "\\varsigma"  
#> [26] "\\omega"      "\\eta"        "\\xi"         "\\Gamma"      "\\Lambda"    
#> [31] "\\Sigma"      "\\Psi"        "\\Delta"      "\\Xi"         "\\Upsilon"   
#> [36] "\\Omega"      "\\Theta"      "\\Pi"         "\\Phi"
```

### Syntax supported

You can use the following operators

  - Unary:
      - `+` and `-`.
  - Binary:
      - `+`, `-`, `*`, `/`, `^`, and `_`.
  - Grouping:
      - `{...}`, `\left{...\right}`, `(...)`, and `\left(...\right)`.

And the following functions

  - Unary:
      - `\sqrt`, `\log`, `\sin`, `\cos`, `\tan`, `\cosh`, `\sinh`, and
        `\tanh`.
  - Binary:
      - `\frac{...}{...}`, `\cdot`, and `\times`.

#### Notes

  - The operator `_` is used to represent subscripts. While you can do
    \(5_2\) in LaTeX, it is not allowed in the package since a subscript
    on a number does not make sense.  
    Only variable names (such as `x` or `\\pi`) can have subscripts.
  - In latex you can write `\sqrt[p]{x}` to represent the p-th root.
    However this is not allowed in this package (at least for now). To
    represent a p-th root you can use `x^{1/p}`.

### Some remarks

#### Implicit multiplication

**tl;dr:** `xy` is understood as `x` times `y`.

A previous version of this package required multiplication to be
explicit. For example, `xy` would have been understood as an identifier
called `xy`. Now, all identifiers, except from special ones (greek
letters), are of one character only. If you do `abc^5` it will be
understood as `a*b*c^5`.

In addition, you can still pass an explicit multiplication operator such
as `*`, `\times` or `\cdot`.

#### Explicit grouping

Although something like `\sin5` renders as \(\sin5\) and we all
understand this means sine of 5, we require explicit grouping with `{}`
or `()` to avoid ambiguity in the function argument. What if I write
`\sin5a`? Does it mean a times the sine of 5 or the sine of 5 times a?
Explicit grouping is a simple solution to eliminate this ambiguity.

#### Special treatment for some characters

Since the numbers
<img src="https://render.githubusercontent.com/render/math?math=\pi">
and <img src="https://render.githubusercontent.com/render/math?math=e">
are so common in mathematical expressions they are treated as constant
numbers and not as names of variables.

In `R`
<img src="https://render.githubusercontent.com/render/math?math=\pi"> is
a built-in constant number and
<img src="https://render.githubusercontent.com/render/math?math=e"> is
obtained with `exp(1)`. See the next example

``` r
latex2r("\\sin{2 * \\pi * t}")
#> [1] "sin(2 * pi * t)"
latex2r("e * x")
#> [1] "exp(1) * x"
latex2r("e^{x + i * y}")
#> [1] "exp(x + i * y)"
```

But note that complex numbers are not supported (yet?).

#### Logarithm of different base

If you write `\\log(x)` it will be interpreted as the natural logarithm
of `x`. If you write `\\log_n(x)` it will be interpreted as the
logarithm of `x` with base `n`.

``` r
latex2r("\\log(x + 1)")
#> [1] "log(x + 1)"
latex2r("\\log_2(x + 1)")
#> [1] "log(x + 1, base = 2)"
```

### Examples

| LaTeX                                                          | R Code                                                           |
| :------------------------------------------------------------- | :--------------------------------------------------------------- |
| `x + y`                                                        | `x + y`                                                          |
| `\sin(x) + \cos(y)`                                            | `sin(x) + cos(y)`                                                |
| `\sin(x)^2 + \cos(y)^2`                                        | `sin(x)^2 + cos(y)^2`                                            |
| `\sqrt{2x\pi}`                                                 | `sqrt(2 * x * pi)`                                               |
| `\log(z)`                                                      | `log(z)`                                                         |
| `\log_a(\frac{x^5}{y})`                                        | `log((x^5) / y, base = a)`                                       |
| `\frac{1}{\sigma\sqrt{2\pi}}e^{\frac{(x - \mu)^2}{2\sigma^2}}` | `1 / (sigma * sqrt(2 * pi)) * exp(((x - mu)^2) / (2 * sigma^2))` |
| `\beta_1^{\frac{x+1}{x^2 \cdot y}}`                            | `beta_1^((x + 1) / (x^2 * y))`                                   |
