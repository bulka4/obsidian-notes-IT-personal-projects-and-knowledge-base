Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Webhook is a tool used for validation or modification of other resources during their creation or update.

They are configured using the MutatingWebhookConfiguration and ValidatingWebhookConfiguration resources.

The Webhook server usually runs inside of its own Pod.

Always when we create a resource in Kubernetes, Kubernetes API server checks if there are any configurations for that resource (MutatingWebhookConfiguration and ValidatingWebhookConfiguration).

If Webhook configurations are found for a resource, then Kubernetes API server communicates with Webhook using HTTPS through the Webhook’s service.
# TLS certificates
Webhook uses TLS certificates for secure HTTPS communication between Kubernetes API server and Webhook server. It is saved as files on the Webhook server and as the caBundle field in the MutatingWebhookConfiguration or ValidatingWebhookConfiguration.

