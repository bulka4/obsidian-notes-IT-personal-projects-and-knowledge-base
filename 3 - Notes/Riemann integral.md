Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction
Riemann integral is used to approximate area under a curve of a function.
# Formal definition
For any:
- Function $f: [a, b] \rightarrow \mathbb{R}$ 
- Partition $P$ of $[a, b]$ into subintervals $a = x_0 < x_1 < \ldots < x_n = b$ 
- Points $\xi_i \in [x_{i-1}, x_i]$ 

Riemann sum is defined as:
$$
S(f, P, \xi) = \sum_{i=1}^n f(\xi) (x_i - x_{i-1})
$$
Then $f$ is Riemann integrable if the limit:
$$
\int_a^b f(x)dx = \lim_{|P| \rightarrow 0}S(f, P, \xi)
$$
exists and is the same for all partitions $P$ and choices of points $\xi_i$.
# Interpretation
We divide x-axis into intervals $[x_0, x_1], \ldots, [x_{n-1}, x_n]$ and for each interval we multiply that interval length by value of the function in that interval.

So we can say that we create a rectangle with one side on length $x_i - x_{i-1}$ and with the height $f(\xi)$.
# Related topics
1. [[Set]]
2. [[Sigma algebra]]
3. [[Measure]]
4. [[Measurable set]]
5. [[Measure space]]
6. [[Measurable function]]