Tags: [[__Machine_Learning]]

# Introduction
Encoding is a method of converting categorical variables into numeric ones ([[Converting categorical variables into numeric ones|link]]) so they can be used as an input for ML models.

A new numeric variable is either:
- Sparse vector ([[Sparse vs Dense vectors|link]]) indicating which category the value belongs to, e.g. one-hot encoding
- New numerical value derived from statistics - Which does reflect a relation between category and variable we are trying to predict (for example target / mean encoding)
# Examples
Example methods of encoding include:
- One hot encoding
	- For each category we create a column in which we have values 0 or 1
	- Number 1 in a column means that this record belongs to the category assigned to this column
- Target / mean
	- For each category, replace its value with the average of the variable we are trying to predict from samples for this category
- Frequency encoding
	- For each category, replace its value with the number of samples with that category in the dataset

#MachineLearning  