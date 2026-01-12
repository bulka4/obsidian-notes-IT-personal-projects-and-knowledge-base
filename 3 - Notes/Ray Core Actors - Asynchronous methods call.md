Tags: [[__Machine_Learning_Engineering]]

# Introduction
When we call actor’s method using the .remote() method, then that actor’s method is being executed asynchronously ([[Asynchronous functions in Python|link]]).

That means, that it doesn’t return a result immediately, it runs in a background and it doesn’t block our Python code. After running .remote() method, our Python code goes immediately to the next line of code.

In order to get the actual result of the actor’s method we called used using .remote(), we need to use the ray.get() function.

#MLEngineering 