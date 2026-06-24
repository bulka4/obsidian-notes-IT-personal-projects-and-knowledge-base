Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
Encoding is a method of converting categorical variables into numeric ones ([[Converting categorical variables into numeric ones|link]]) so they can be used as an input for ML models.

A new numeric variable is either:
- Sparse vector ([[Sparse vs Dense vectors|link]]) indicating which category the value belongs to, e.g. one-hot encoding
- New numerical value derived from statistics - Which does reflect a relation between category and variable we are trying to predict (for example target / mean encoding)
# Examples
Example methods of encoding include:
- **One hot encoding** - Create one column per category with values 0 or 1 indicating what is a category for a data sample ([[Encoding categorical variables - One hot encoding|link]])
- **Target / mean** - Replace a category with an average of the target variable for data samples for that category ([[Encoding categorical variables - Target - mean encoding|link]])
- **Frequency encoding** - Replace a category with the number of samples with that category in the dataset ([[Encoding categorical variables - Frequency encoding|link]])
 