Tags: [[_Computer_hardware]]

# Introduction
There are different numeric formats used to represent numbers. Each format has different precision, that is how precisely it can represent numbers.

They determine how many bits are used to represent different parts of numbers:
- Sign
- Exponent
- Decimal places (fraction / mantissa)

There are different types of formats, for example:
- FP32
- FP16
- BF16
- INT8
- INT4
# Representing different parts of a number using bits
As described here - [[Exponential notation|link]], we can write a number using an exponential notation:
$$
\large
+ / - 1 \cdot \text{fraction} \cdot 10^\text{exponent}
$$
Numeric formats determine how many bits we use for each component in an exponential notation of a number:
- 1 bit for the sign
- N bits for the exponent
- M bits for the fraction (decimal places)

That implies:
- The more bits we can use for the exponent -> the bigger number we can represent
- The more bits we can use for the fraction -> the more decimal places we can represent
## Example
So for example, if we have a number:
$$
123.456 = 1.23456 \cdot 10^2
$$
then we will use:
- 1 bit to represent the sign
- N bits to represent the number 2
- M bits to represent the number 1.23456
## Sign
- Number 0 means positive
- Number 1 means negative
# Number of bits used by formats
Below table describes how many bits different formats use for different parts of a number:

| Format | Sign | Fraction | Exponent | Comment                  |
| ------ | ---- | -------- | -------- | ------------------------ |
| FP32   | 1    | 23       | 8        | Represents real numbers  |
| FP16   | 1    | 10       | 5        | Represents real numbers  |
| INT8   | -    | 8        | -        | Represents only integers |
# Errors caused by numeric formats
Since we can't represent all the numbers using numeric formats, errors can happen during calculations like described here - [[Numeric formats (precision) - Calculation errors]]

#ComputerHardware 