Tags: [[_Computer_hardware]]

# Introduction
When performing calculations on numbers represented using numeric formats ([[Numeric formats (precision)|link]]), they are not perfect. Because those formats have a finite precision, some values are rounded or not taken into account what causes small errors.
# Overflow & underflow
Some numbers can get rounded:
- If a number is too big, it gets rounded into infinity (overflow)
- If a number is too small, it gets rounded into 0 (underflow)
# NaN values
Overflow and underflow can cause receiving NaN values, for example when we get:
- 0/0
- inf - inf
- inf / inf
# Adding numbers of different magnitude
When we add very small number to a very big number, for example:
$$
10^6 + 10^{-3}
$$
then that value gets rounded and small number doesn't make any effect, so we receive $10^6$ .
# Non-associative adding
Adding is not associative (order in which we add numbers matters):
$$
(a + b) = c \neq a + (b + c)
$$

#ComputerHardware 