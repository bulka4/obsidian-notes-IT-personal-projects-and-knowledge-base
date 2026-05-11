Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
In this project we create a recommendation system using techniques such as:
- Collaborative filtering ([[Recommendation systems - Collaborative filtering|link]])
	- Find similar movies by calculating similarity between ratings they receive from users using:
		- Correlation
		- Cosine similarity
	- Find similar users by calculating cosine similarity between ratings they grant to movies
- SVD ([[Recommendation systems - SVD|link]])
# Project code repository
A repository with a code for this project is here - [github.com](https://github.com/bulka4/movies_recommendation).
# Environment setup to run the code
Environment setup to run the code:
```shell
# Clone the repo
git clone https://github.com/bulka4/movies_recommendation.git

# Go to the repos local folder
cd movies_recommendation

# create virtual environment
python -m venv venv

# activate venv (choose the commend for Windows or for Mac)

# for Windows
venv\Scripts\activate

# For Mac
source venv/bin/activate

# update pip and install requirements
python -m pip install --upgrade pip
pip install -r requirements.txt

# Run JupyterLab to open Jupyter Notebooks
jupyter-lab
```
# Data
We use data from CSV files about ratings users grant to movies included in the `data` folder.