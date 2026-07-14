## Version of the EKS:

The latest version presently available to use is 1.36. As a standard practice I will be using N-1 which is 1.35 for our EKS cluster project.

## Monthly Cost Predictions:

I will be running this project as a lab hence the instance will be t3.medium. We will use gp3 as EBS storage volume. So, considering 0.1 USD per hour charges of the control plane, the monthly cost may reach about USD 100. Calculations shown below, if run on us-east-1 region:

| Item | Monthly Cost (USD) | Notes |
| --- | ---: | --- |
| EKS Control Plane | $73.00 | Standard support tier ($0.10/hr). |
| Compute (1x t3.medium) | ~$30.37 | On-Demand pricing ($0.0416/hr). |
| Storage (20 GB gp3) | $1.60 | $0.08 per GB/month (20 × 0.08). |
| Total (Approximate) | ~$104.97 | Excluding data transfer/logs. |

## Removed the SSH Block because:

We rarely need to login to the worker node.
It provides better security(No credentials disclosed.)

## EKSCTL surprise:

I was actually thinking that the version that we should be using should be the latest one, but I was surprised to know that it is N-1, because the latest version might contain bugs.

## Version 1.35 Deadline(N-1 at the time of this note being written.)

As per AWS records the version End of Support Date is **27th March 2027.**

## What if SSH session is must required:

In that case we can use AWS SSM Session Manager to open a session.

## After the cluster is brought up.

The kube-system namespace contains the "brain" and "nervous system" of the cluster. These pods are not our applications; they are the services that keep Kubernetes running. Understanding Each node in kubesystem, explained below:


**Pod	Role**

**coredns**	Handles DNS resolution within the cluster. Allows pods to find each other by name (e.g., my-app.default.svc.cluster.local).
**kube-proxy**	Runs on every node. Manages networking rules, ensuring that traffic reaches the correct containers.
**vpc-resource-controller**	EKS-specific. Manages the assignment of VPC IP addresses to pods (ENI management).
**aws-node (VPC CNI)**	The plugin that integrates Kubernetes networking with the AWS VPC, giving each pod its own IP address within the VPC.
**metrics-server**	Gathers CPU/Memory performance data for nodes and pods, enabling kubectl top commands.

## Opening SSH Shell:

**To Open SSH Shell, we can follow below steps:**

Step 1: Identify the IAM role used by **managedNodeGroups**. Our role named as **eksctl-portfolio-cluster-cluster-ServiceRole-XXXX**
Step 2: Attach the **AmazonSSMManagedInstanceCore** managed policy to that role.  
Step 3: Once the policy is attached, nodes will appear in the **AWS Systems Manager** > **Fleet Manager console** under **"Managed Instances."** From here we can then select a node and click "Start session" to get a shell.  

**Real Surprise**

Once I did kubectl get pods it listed 5-6 pods, and I didn't notice all their names, at this point I was thinking that I will be able to SSH to all of them but I found out that only one node can be SSHed -  i-01adda5aa65c8367e (portfolio-cluster-standard-nodes-Node).
