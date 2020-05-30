# <font color='red'>fdiv - Fixed Point Division for Shell Scripts</font>

#### <font color='green'>(c) Libor Spacek, 30th May 2020</font>

### Introduction

**fdiv** takes two integer arguments: numerator and denominator.
It returns a fixed point number division result to the best possible precision
 allowed by signed 64 bit integers, rounded to the nearest next digit.
 
### Installation

Simply place the script in any directory in your search path, such as $HOME/bin, /usr/local/bin, or specify its path when invoking it.
 
### Example Usage
   $(fdiv -2 3) returns -0.666666666666666667
   
### Features

- Checks arguments, generates errors if they are missing or not integers, or the divisor (denominator) is zero.

- When the numerator is zero, 0.0 is immediately returned.

- Automatically selects and calculates the maximum precision. Truncation error wil be less than 5E-19.

- When numerator > denominator, the answer is composed from integral numerator/denominator, followed by remainder/denominator after the decimal point. This further enhances the precision.

- When the denominator is divisible by 10, or its multiples, the decimal precision is further increased by the relevant number of decimal digits.

- Deals correctly with negative argument(s). 

See comments in the source for more details.
