Tags: [[__My_projects]]
#MyProjects 

# Introduction
When working for Transmission Dynamics, I have created a model which predicts how many people were walking on an escalator based on sensors measurements.
# Model
As a model I was using Recurrent Neural Networks (GRU, LSTM). Model:
- Takes as an input a series of measurements from an escalator (pressure mostly)
- Predicts how many people were walking on that escalator during the period when those measurements were made
# Model deployment
Model was integrated with a Python code which was processing data from sensors to:
- Make predictions during that processing
- Save them in a SQL database
# Technologies used
Technologies used in that project:
- Python, SQL, bash
- Tensorflow
- Protobuf (for working with a binary data from sensors)