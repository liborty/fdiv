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
fdiv -2 3
-0.666666666666666667  
fdiv 355 113
3.14159292035398230
fadd 9.876543 0.987
10.863543
```

## Features

- Checks arguments, returns errors if they are missing or not integers or the divisor (denominator) is zero. Deals correctly with negative argument(s).

- When the numerator is zero, 0.0 is immediately returned.

- Automatically calculates with the maximum precision. Truncation error wil be less than 5E-19.

- When `numerator > denominator,` then the answer is composed from numerator/denominator integer division, followed by the decimal point and then the upscaled remainder divided by the denominator, which gives the digits after the decimal point. This maintains the 5E-19 guaranteed precision even for some  quite large numbers. For example:

```bash
fdiv $((2**63-1)) 3
3074457345618258602.333333333333333333
```

- When the denominator is divisible by 10, or its multiples, then the decimal precision can be also increased, this time by the relevant number of zeroes inserted after the decimal point. For example, here the truncation error is now less than 5E-22:

```bash
fdiv 5 30000
0.0001666666666666666667
```

Note that this is not like Bignum package using an unlimited number of words and storage size, so barring the mod 10 trick, there are natural limits to the precision obtained: namely two 64 bit words. Still, that is quite a lot better than the 52 bits of the 'double precision' floating point standard.

## References

See comments in the source of `fdiv` for more details.

Here is a [blog](https://oldmill.cz/2020-01-02-the-joy-of-bashing.html) describing the magic idea behind implementing this using only Bash integer arithmetic.
