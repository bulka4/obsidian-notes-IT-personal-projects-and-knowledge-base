Tags: [[__Machine_Learning_Engineering]]

# Introduction
The .remote() function is asynchronous. So when we run it, it doesn’t block a Python script, further lines in code are being executed immediately without waiting for the .remote() to be finished.

The result_ref variable in the above example is not the output of the square function. We need to use ray.get(result_ref) to get that result.

#MLEngineering 