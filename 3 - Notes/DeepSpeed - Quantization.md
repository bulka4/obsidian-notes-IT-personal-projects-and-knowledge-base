Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# Introduction
Quantization is the process of reducing the precision of numbers (tensors ([[Tensor|link]])) used in a model in order to save memory usage and compute cost.

It determines what numeric format (FP32, FP16, INT8 etc. ([[Numeric formats (precision)|link]])) will be used to represent numbers. Numeric format determines how many decimal places and how big numbers we can use.

For example:
- If we can use only 6 decimal places, then number 1.23456789 will be rounded to 1.234568
- If we can use 15 as the biggest number (that's the case when using INT4), then number 20 will be rounded to 15

Reducing precision results in lower accuracy of a model since calculations are less precise.
# Types of Quantization
## Post training quantization (PTQ)
Quantize a trained model for inference (making predictions).
## Quantization-aware training (QAT)
Use quantization during training a model. 

Precision is reduced only during a forward pass (calculating model's output), not during calculating gradients or updating model's parameters.
# Scaling factors
When converting float numbers (like FP32) into integers (INT8 or 4), we divide numbers by a scaling factor. That scaling factor is calculated based on numbers which we want to convert, for example:
$$
\text{scale} = \frac{\max \{|x|,\ x \in \text{fp32} \} } 
{ \max \{|x|,\ x \in \text{int} \} }
$$
where:
- fp32 - Set of numbers in the fp32 format which we want to convert into integers
- int - Set of all the numbers possible to represent in the integer format into which we want to convert numbers

Integer numeric formats have a range of numbers possible to represent, for example for INT 8 that is [-127, 127]. So we divide all the float numbers by a factor, which converts them into integers which fits into that range.

That can make parameters bigger, for example float parameters can have values from the range [-1, 1], and they will be converted into integers from the range [-127, 127].
## Scale per tensor vs channel
When converting float numbers into integers, we can use a different scale per tensor or per channel (i.e. per tensor dimension, for example per row in a matrix).
## Scaling activations
Quantization of weights is easier as their values are always the same (after training), while activations (outputs of activation functions) changes.

For calculating the scaling factor for converting float numbers into integers, we need to know the values we are converting (according to the formula for scaling factor we mentioned earlier). But we don't know values of activations until we calculate them.

There are two approaches:
- Static range: Calculate $\max \{|x|,\ x \in \text{fp32} \}$ ahead (based on a chosen calibration data)
- Dynamic range: Calculate $\max \{|x|,\ x \in \text{fp32} \}$ during calculating model's output

Dynamic range is more accurate but slower.

#DistributedComputing #MLEngineering 