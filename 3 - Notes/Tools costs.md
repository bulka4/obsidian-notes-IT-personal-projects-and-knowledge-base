Tags: [[__Cloud]], [[__Data_Engineering]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]]

# Managed Kubernetes vs cloud VMs cost

Cost of each node in managed Kubernetes on Azure is the same as cost of a VM with the same specification.

# Cloud VMs vs on prem server cost

## Cloud VM cost

Standard_D4s_v3 (4 vCPU, 16 GB) Azure VM costs $65 per month when bought for 3 years ahead.

**Total cost per 3 years: ~2.5k$**

## Physical server cost

A similar physical server (4+ cores, 16-32 GB) costs ~ $1k.

Let’s assume it will last for 5 years (sometimes there is a warranty for 5 years).

Maintenance for 5 years costs around $1.3k. That includes:

· Maintenance and parts ~ $600

· Electicity – power + cooling ~ $700

**Total cost per:**

· **5 years ~ $2.3k**

· **3 years ~ $1.4k**

# Databricks cost

We pay for VM + DBUs.

If we use Standard_D4s_v3 then for 1h (pay-as-you-go) it will cost:

· **VM cost per hour:** ~$0.20

· **DBU cost per hour:**

o All purpose compute (when running notebooks) ~ $0.5

o Job compute (when running scheduled jobs) ~ $0.3

· **Total per hour:** $0.5 – 0.7

Days in 3 years = 3 * 365 = 1095 days

**Total cost for 3 years running:**

· **5h daily ~ 1095 * 5 * $0.5 = $2700**

· **10h daily ~ 1095 * 10 * $0.5 = $5400**