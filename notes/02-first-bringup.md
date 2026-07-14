
## Opening SSH Shell:

**To Open SSH Shell, we can follow below steps:**

Step 1: Identify the IAM role used by **managedNodeGroups**. Our role named as **NodeInstanceRole-XXXX**
Step 2: Attach the **AmazonSSMManagedInstanceCore** managed policy to that role.  
Step 3: Once the policy is attached, nodes will appear in the **AWS Systems Manager** > **Fleet Manager console** under **"Managed Instances."** From here we can then select a node and click "Start session" to get a shell.  

**Real Surprise**

Once I did kubectl get pods it listed 5-6 pods, and I didn't notice all their names, at this point I was thinking that I will be able to SSH to all of them but I found out that only one node can be SSHed -  i-01adda5aa65c8367e (portfolio-cluster-standard-nodes-Node).
