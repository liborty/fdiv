# Fdiv - Fixed Point Arithmetic in Shell Scripts [<img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/liborty/fdiv/HEAD?logo=github">](https://github.com/liborty/fdiv)

## Introduction

**fdiv** bash script takes two integer arguments: numerator and denominator.

It returns a fixed point number division result to the best possible precision
 allowed by signed 64 bit integers, rounded to the nearest next digit.

Saves having to use bulky external facilities in subshells, such as `awk,dc,bc`, for very simple calculations. 

**fadd** takes two positive fixed point numbers, such as produced by the above, and adds them up.

Other operators are still to come. 

## Installation

Simply place the **fdiv** and **fadd** scripts in any directory in your search path, such as $HOME/bin, /usr/local/bin, or specify its path when invoking it. Make sure that they have  execute permissions.
 
### Example Usage

```bash
   $(fdiv -2 3) returns -0.666666666666666667  
   $(fadd 9.876543 0.987) returns 10.863543
 ```
 
## Features

- Checks arguments, returns errors if they are missing or not integers or the divisor (denominator) is zero.

- When the numerator is zero, 0.0 is immediately returned.

- Automatically calculates with the maximum precision. Truncation error wil be less than 5E-19.

- When `numerator > denominator,` the answer is composed from integral numerator/denominator result, followed by `remainder/denominator < 1,` which gives the digits after the decimal point. This maintains the 5E-19 precision even when more significant digits are used.
 
	For example, `$( ./fdiv 500000 3 )` returns `166666.666666666666666667`

- When the denominator is divisible by 10, or its multiples, the decimal precision is further increased by the relevant number of decimal digits.

	For example, `$( ./fdiv 5 30000 )` returns `0.0001666666666666666667`, where the truncation error is now less than 5E-22

- Deals correctly with negative argument(s).

## References

See comments in the source of **fdiv** for more details.

Here is a [blog](https://oldmill.cz/2020-01-02-the-joy-of-bashing.html) describing the magic idea behind implementing this using only Bash integer arithmetic.
