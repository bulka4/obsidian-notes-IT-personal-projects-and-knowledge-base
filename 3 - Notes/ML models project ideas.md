Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Project ideas
Zebrac w jedno miejsce wszystkie materialy, z ktorych sie uczylem i zrobic chatbota, ktory bedzie odpowiadal na podstawie tych materiałów
# 1) **Projects for stationary shops:**
**A**) predicting number of given product sales based on which store is selling it, holidays, oil price, store location. We can use it to plan supplies.

Websites:
- [https://towardsdatascience.com/machine-learning-for-store-demand-forecasting-and-inventory-optimization-part-1-xgboost-vs-9952d8303b48](https://towardsdatascience.com/machine-learning-for-store-demand-forecasting-and-inventory-optimization-part-1-xgboost-vs-9952d8303b48)
- https://www.kaggle.com/competitions/favorita-grocery-sales-forecasting

**B**) finding which products are often bought together using data about transactions and association rule or cosine similarity. Using that we can place products which are often bought together on shelfs close to each other or make promotions.

Websites:
- https://www.kaggle.com/code/evrenermis/association-rule-based-learning-explained/notebook

**C)** choose the best price, promotion or shop to locate a product by using a model to predict a profit or sales for given price, promotion or location

Websites:
- [https://towardsdatascience.com/market-response-models-baf9f9913298](https://towardsdatascience.com/market-response-models-baf9f9913298)
# **2)** **Projects for e-commerce:**
**A)** churn model:
model which gives probability that client will stop buying from given shop. Accuracy is not good metric, better is recall and precision (because there is few clients who leave, let’s say about 10%). When you know which clients are propably to leave you can reach out to those clients with for example marketing, discounts. If you know that someone has annual revenue 100pln, and their propability of leaving is 10%, then their future expected revenue is 90pln, and you want to do something in order to increase their propability of not leaving by 5%, then you know that you can spend on it max 5pln to make it worth. We need to find out which clients left a website and what were their behaviours before they left.

**B)** sentimental analysis:
get data from people comments and surveys and label them as positive, neutral or negative and and try to learn what people like and what don’t.

**C)** customer lifetime value:
based on rfm (how often client was buying in a shop, what is the difference between first and last transaction and mean value of transactions) we can predict what profit customer will bring in given time period in the future and their future rfm. Thanks to knowing CLV you can suit products to the best customers or decide how much spend to acquire new customers or retain existing ones.
# **3)** **Content distribution**
where and to whom show your audio and video.

Websites:
- [https://medium.com/the-mission/the-garyvee-content-strategy-how-to-grow-and-distribute-your-brands-social-media-content-35dd15e67b3f](https://medium.com/the-mission/the-garyvee-content-strategy-how-to-grow-and-distribute-your-brands-social-media-content-35dd15e67b3f)
# **4)** **Customer insights / segmentation**
classification of customers based on their activity, how much they spent, for how long they are company customers, how often they buy etc.

Websites:
- [https://www.kaggle.com/code/mgmarques/customer-segmentation-and-market-basket-analysis](https://www.kaggle.com/code/mgmarques/customer-segmentation-and-market-basket-analysis)
# **5)** **Customer jurney**
- Understanding how customers’ experience with a company looks like.

Websites:
- [https://medium.com/choice-hacking/how-to-create-a-customer-journey-map-ffbd580284d7](https://medium.com/choice-hacking/how-to-create-a-customer-journey-map-ffbd580284d7)
# **6)** **Marketing analytics**
- Check how different customers are propably to accept the offer from campaign.

Websites:
- [https://www.kaggle.com/datasets/jackdaoud/marketing-data](https://www.kaggle.com/datasets/jackdaoud/marketing-data)
- [https://www.kaggle.com/datasets/rodsaldanha/arketing-campaign](https://www.kaggle.com/datasets/rodsaldanha/arketing-campaign)
- https://www.kaggle.com/datasets/harrimansaragih/dummy-advertising-and-sales-data
- [https://www.youtube.com/watch?v=g7hEPopJ4MY](https://www.youtube.com/watch?v=g7hEPopJ4MY) (data is in a link in a description)
- predict which customers are the most likely to stop buying from the company and target ads to them
- predict customer lifetime value and use this information to decide how much we can spend on a marketing and target most valuable customers
- Market basket analysis:
Check which products are often bought together so we can recommend next products to buy for a customer

Websites:
- [https://www.kaggle.com/code/mgmarques/customer-segmentation-and-market-basket-analysis](https://www.kaggle.com/code/mgmarques/customer-segmentation-and-market-basket-analysis)
- segment customers so you can create different ads for different groups of people

Websites:
- [https://www.kaggle.com/datasets/vetrirah/customer](https://www.kaggle.com/datasets/vetrirah/customer)
- [https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python](https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python)
- [https://www.kaggle.com/code/mgmarques/customer-segmentation-and-market-basket-analysis](https://www.kaggle.com/code/mgmarques/customer-segmentation-and-market-basket-analysis)
- check effectiveness of compaigns

Websites:
- [https://towardsdatascience.com/data-science-project-marketing-analytics-data-driven-solutions-72d050084642](https://towardsdatascience.com/data-science-project-marketing-analytics-data-driven-solutions-72d050084642)
# **7)** **HR analytics**
Try to use data about employees in order to understand why some of them leave a job and some of them stay,

what are characteristic features of better performing employees or predict performance, what trainings are efective, if employees make progress after finishing them

Websites:
- [https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)
- create a digital assistant which do repetitive tasks, gives employees information they need, help scheduling meeting by showing calendars, scheduling leaves

Websites:
- [https://chatbotslife.com/what-is-a-digital-hr-assistant-and-why-does-it-matter-dafa728e16a](https://chatbotslife.com/what-is-a-digital-hr-assistant-and-why-does-it-matter-dafa728e16a)
- predicting demand on employees
- predict how likely employees are to quit the job
# **8)** **A/B tests**
Websites:
- [https://towardsdatascience.com/a-b-testing-statistics-true-and-estimated-value-of-conversion-rate-b7a77db6f60e](https://towardsdatascience.com/a-b-testing-statistics-true-and-estimated-value-of-conversion-rate-b7a77db6f60e)
# **9)** **Predicting which films I will like**
# 10) DeepSpeed - Distributed training and inference
- Train some simple model using
- Distributed inference for a RAG system
# 11) Program reinforcement learning from scratch
- Use only low level function for math (like multiply matrixes, calculate gradients)
- Train either transformer or some simpler model using reinforcement learning
- Later on run it on DeepSpeed
# 12) Reinforcement learning with a dynamic environment
- Model learning with reinforcement learning in environment that changes
- For example a drone that flies and weather is changing
- Drone needs to take different actions depending on a weather conditions
- Or another example is car driving on a road with randomly appearing obstacles
# 13) Emergent Multi-Agent Systems with reinforcement learning
- Multiple agents live in the same environment, affect each other and learn how to work better
- For example agents might try to collect food which randomly appears on a map. They can move, pick up a food and share it with others.
- Agents are learning with reinforcement learning
- I can use for that Ray Rlib, DeepSpeed, MLflow