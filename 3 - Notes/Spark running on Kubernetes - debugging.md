Tags: [[__Data_Engineering]], [[__Distributed_computing]], [[_Kubernetes]], [[_Spark]]

# CoreDNS
- Check CoreDNS logs
- Check firewall rules using iptables
- Check the CoreDNS configmap, especially the section after ‘forward’ keyword
## Pods
- Spark Operator is running its own Pods called ‘spark-operator-xxxx’. Check their status and logs.
## Services
- Spark Operator is running its own Services called ‘spark-operator-xxxx’. Check their status and logs.
## Service Accounts
- Spark Operator’s Pods are using Service Accounts which need to have proper permissions. We can check what are those Accounts by running:
	- Kubectl get pod \<pod-name> -n \<namespace> -o yaml
## Webhooks
- This is applicable only when we are using webhooks in spark operator. We don’t need to use it. It is problematic to use. If we want to use webhook to add additional specification not supported by the SparkApplicaiton, we can use for that podTemplateFile instead.
- Check if webhook Pod have certificates files mounted. This information is in the YAML specification of the webhook Pod. We can check it by running:
	- kubectl get pod -n \<namespace> \<webhook-pod-name> -o yaml
