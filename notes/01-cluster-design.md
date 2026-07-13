## Version of the EKS:

The latest version presently available to use is 1.36. As a standard practice I will be using N-1 which is 1.35 for our EKS cluster project.

## Monthly Cost Predictions:

I will be running this project as a lab hence the instance will be t3.medium. We will use gp3 as EBS storage volume. So, considering 0.1 USD per hour chages of the control plane, the monthly cost may reach about USD 100. Calculations shown below, if run on us-east-1 region:

| Item | Monthly Cost (USD) | Notes |
| --- | ---: | --- |
| EKS Control Plane | $73.00 | Standard support tier ($0.10/hr). |
| Compute (1x t3.medium) | ~$30.37 | On-Demand pricing ($0.0416/hr). |
| Storage (30 GB gp3) | $2.40 | $0.08 per GB/month (30 × 0.08). |
| Total (Approximate) | ~$105.77 | Excluding data transfer/logs. |

## Removed the SSH Block because:

We rarely need to login to the worker node.
It provides better security(No credentials disclosed.)




