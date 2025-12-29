Tags: [[__Machine_Learning]]

# Introduction
In order to detect anomalies ([[Anomaly Detection models|link]]) , we train an autoencoder ([[Autoencoders|link]]) on a data without anomalies.

After training a model, when we see that it makes a significantly bigger error then usually when reconstructing a data sample, it is likely an anomaly. 

That's because model has learnt efficiently to reconstruct data samples which are not anomalies, so when its effectiveness in reconstruction suddenly drops, it might be caused by the fact that this sample is significantly different than the others.

#MachineLearning 