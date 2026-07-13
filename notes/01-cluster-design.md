## Version of the EKS:

The latest version presently available to use is 1.36. As a standard practice I will be using N-1 which is 1.35 for our EKS cluster project.

## Monthly Cost Predictions:

I will be running this project as a lab hence the instance will be t3.medium. We will use gp3 as EBS storage volume. So, considering 0.1 USD per hour chages of the control plane, the monthly cost may reach about US 100. Calculations shown below: 

Monthly Cost Estimate (US-East-1)ItemMonthly Cost (USD)NotesEKS Control Plane$73.00Standard support tier ($0.10/hr).Compute (1x t3.medium)~$30.37On-Demand pricing ($0.0416/hr).Storage (30 GB gp3)$2.40$0.08 per GB/month ($30 \times 0.08$).Total (Approximate)~$105.77Excluding data transfer/logs.
