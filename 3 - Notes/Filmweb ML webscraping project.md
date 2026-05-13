Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
In this project, we:
- Prepare a dataset about movies by webscraping filmweb.pl website using the BeautifulSoup Python library
- Build a recommendation system for movies
- Predict a rating of a movie
# Code repository
Repository with project's code - [github.com](https://github.com/bulka4/filmweb_ml_webscraping).
# Models
We predict a rating of a movie (it is a real number between 0-10). We create two models:
- For classification
	- Round a rating of a movie to an integer
	- Use a decision tree
- For regression
	- Predict an exact rating (a real number)
	- Use a Support Vector Regression model (a regression version of the Support Vector Machine model).

We use `sklrean` module to create and train those models.
# Recommendation system
We build a content based recommendation system ([[Recommendation systems - Content based system|link]]) for movies. This system:
- Finds movies with similar features 
- Uses cosine similarity to measure how similar those features are
## Creating movie feature vectors to compare
To create movie feature vectors that we will be comparing when making recommendations, we:
- Concatenate different features into a single string (to create so called "soup"): genre, actors, director, screenwriter and studio
- Use count vectorization ([[Count Vectorization|link]]) to convert the soup (a set of features) into vectors
	- We create a vector where each number (0 or 1) indicates whether or not a given feature (e.g. actor, screenwriter) appears in a data sample
	- Created vectors are the movie feature vectors to compare
## Choosing model parameters with the GridSearchCV function
To choose the best parameters for models, we use the `GridSearchCV` function.
# Data preparation
## Webscraping data from filmweb.pl
To prepare a training dataset, we webscrape data from filmweb.pl website using the BeautifulSoup Python library.
## Encoding categorical variables
We use one hot encoding ([[Encoding categorical variables - One hot encoding|link]]) to convert categorical variables into discrete ones (numeric).
# Environment setup to run the code
To prepare an environment to run this code, run the below commands:
```shell
# Clone the git repo
git clone https://github.com/bulka4/filmweb_project.git

# Go to the repository local folder
cd filmweb_project

# create virtual environment
python -m venv venv

# Activate virtual environment - use a proper command either for Windows or Mac
# activating venv for Windows:
venv\Scripts\activate
# activating venv for Mac:
source venv/bin/activate

# update pip and install requirements
python -m pip install --upgrade pip
pip install -r requirements.txt

# Start JupyterLab to review Jupyter Notebooks
jupyter-lab
```
