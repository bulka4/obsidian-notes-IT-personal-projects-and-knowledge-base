Tags: [[__Machine_Learning_Engineering]], [[_ML_model_serving]]
#MLEngineering #MLModelServing

# Introduction
Traditional load balancing, where we distribute requests equally across all servers serving an app, doesn't work.

That's because for ML models, some requests are small and requires little time to process, while others are much bigger. So we can't assign to one server only the small requests and to another server only the big requests.