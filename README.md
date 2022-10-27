## Supported Math Expressions

### Syntax supported

You can use the following operators

  - Unary:
      - `+` and `-`.
  - Binary:
      - `+`, `-`, `*`, `/`, `^`, and `_`.
  - Grouping:
      - `{...}`, and `(...)`.

And the following functions

  - Unary:
      - `\sqrt`, `\log`, `\sin`, `\cos`, `\tan`, `\cosh`, `\sinh`, and
        `\tanh`.

#### Notes

  - You can write '\sqrt' to represent the square root of a number. To
    represent a p-th root you can use `x^{1/p}`.
  - If you do `abc^5` it will be understood as `a*b*c^5`.
  - Complex numbers are not supported yet.
  - Since the numbers '\pi' and 'e' are so common in mathematical expressions they are treated as constant
numbers and not as names of variables.
  - If you write `log(x)` it will be interpreted as the natural logarithm
of `x`. If you write `\log_n(x)` it will be interpreted as the
logarithm of `x` with base `n`.


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


