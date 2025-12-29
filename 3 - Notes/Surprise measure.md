Tags: [[_Information_theory]], [[__Mathematics]]

# Introduction
Let's assume, that $q(x)$ is a probability distribution function ([[Probability distribution (density, mass) function|link]]) of a random variable $X$ ([[Random variable|link]]).

The measure of 'surprise' is formula $-\log(q(x))$, because:
- Less likely event has bigger 'surprise': $q(x_1) < q(x_2) \implies -\log(q(x_1)) > -\log(q(x_2))$ 
- Certain events has 0 'surprise': $q(x) = 1 \implies -\log(q(x)) = 0$ 

So value $-\log(q(x))$ can be used to measure how surprised we are, according to the probability distribution $q$, when observing the event $X = x$.

#InformationTheory #Mathematics 