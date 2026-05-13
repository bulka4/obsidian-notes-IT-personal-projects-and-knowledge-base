Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
A Fit Predictor is a tool which predicts dress sizes. It is used on many different websites which sales clothes.

In this project, we perform A/B testing to compare data related to the Fit Predictor from two different versions of websites selling clothes on which it was used.

We have here two websites:
- Partner A
- Partner B

And for each website there are two versions (test and control) for which we perform A/B testing.
# Code repository
A repository with code - []().
# Conversion rate calculations
- We calculate:
	- 95% confidence interval $[x, y]$ for CRU (conversion rate uplift):
	$$
	\large CRU = CR_{\text{test}} - CR_{\text{control}}
	$$
	- A conversion rate ("number of users who made an order" / "number of users who visited a website") for test and control datasets.