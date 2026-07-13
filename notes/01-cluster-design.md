## Version of the EKS:

The latest version presently available to use is 1.36. As a standard practice I will be using N-1 which is 1.35 for our EKS cluster project.

## Monthly Cost Predictions:

I will be running this project as a lab hence the instance will be t3.medium. We will use gp3 as EBS storage volume. So, considering 0.1 USD per hour charges of the control plane, the monthly cost may reach about USD 100. Calculations shown below, if run on us-east-1 region:

| Item | Monthly Cost (USD) | Notes |
| --- | ---: | --- |
| EKS Control Plane | $73.00 | Standard support tier ($0.10/hr). |
| Compute (1x t3.medium) | ~$30.37 | On-Demand pricing ($0.0416/hr). |
| Storage (20 GB gp3) | $1.60 | $0.08 per GB/month (20 × 0.08). |
| Total (Approximate) | ~$105.77 | Excluding data transfer/logs. |

## Removed the SSH Block because:

We rarely need to login to the worker node.
It provides better security(No credentials disclosed.)

## EKSCTL surprise:

I was actually thinking that the version that we should be using should be the latest one, but I was surprised to know that it is N-1, because the latest version might contain bugs.

## Version 1.35 Deadline(N-1 at the time of this note being written.)

As per AWS records the version End of Support Date is **27th March 2027.**

## What if SSH session is must required:

In that case we can use AWS SSM Session Manager to open a session.



