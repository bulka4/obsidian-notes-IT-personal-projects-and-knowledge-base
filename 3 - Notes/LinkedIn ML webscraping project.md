Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
In this project, we:
- Create a dataset about job offers from LinkedIn using webscraping with the BeautifulSoup Python library
- Build a model for predicting years of experience required
- Create a recommendation system recommending jobs
# Code repository
Repository with project's code - [github.com](https://github.com/bulka4/linkedIn_ml_webscraping).
# Predicting years of experience
We predict required years of experience based on a job offer description.

Model:
- Takes as an input text (words are converted into numbers by assigning to them unique IDs).
- Is a neural network consisting of layers:
	- Embedding
	- GRU
	- LSTM
	- Dense
## Programming the model
We program the model using the `Sequential` Tensorflow function and the `model.fit()` method.
# Predicting whether a job is interesting
I added labels to some data samples indicating whether or not a job is interesting to me and tries to train a model which predicts that.

Model:
- Takes as an input text (words are converted into numbers by assigning to them unique IDs).
- Is a neural network consisting of layers:
	- Embedding
	- GRU
	- LSTM
	- Dense
# Recommendation system
We create a recommendation system which recommends jobs by:
- Converting job descriptions into vectors using TF-IDF ([[TF-IDF|link]])
- Comparing description vectors using cosine similarity
# Issues
There is an issue when webscraping data from LinkedIn. There is and authentication checking if we are a human and our script after getting data from a few job offers stops working.

Potentially we can use LinkedIn Rest API instead of webscraping to get its data.