## Budget Details:

**eks-buget-list** created which alerts at $8 and the upper limit is USD 10. 

## Cloudformation Stack Inventory:
The cluster.yaml created two cloudformation stacks as below:
 **eksctl-portfolio-cluster-cluster**
 **eksctl-portfolio-cluster-nodegroup-standard-nodes**

 ## To bring up the cluster:
  Run **eksctl create cluster -f cluster.yaml**

  Running **time eksctl create cluster -f cluster.yaml** will also give the total time taken during startup. In our case it took around 18 minutes.

## Opening SSM Session:

**To Open SSM Session, we can follow below steps:**

Step 1: Identify the IAM role used by **managedNodeGroups**. Our role named as **NodeInstanceRole-XXXX**
Step 2: Attach the **AmazonSSMManagedInstanceCore** managed policy to that role.  
Step 3: Once the policy is attached, nodes will appear in the **AWS Systems Manager** > **Fleet Manager console** under **"Managed Instances."** From here we can then select a node and click "Start session" to get a shell.  

So during the first run I had to follow above steps to attach the policy AmazonSSMManagedInstanceCore manually, but the second time when I brought up the cluster again, it was already attached to the role. So I didn't have to anything manually here.
 ## OR follow below for a CLI Session.
Step 4: Install SSM CLI from this URL https://s3.amazonaws.com/session-manager-downloads/plugin/latest/windows/SessionManagerPluginSetup.exe.
Step 5: Check instances available to SSM:
  aws ssm describe-instance-information --region us-east-1 --query "InstanceInformationList[].InstanceId"
  Example output in my case:
  
$ aws ssm describe-instance-information --region us-east-1 --query "InstanceInformationList[].InstanceId"
[
    "i-0f17bdafd6de45ece"
]


Step 6: Start a SSM Session:
   aws ssm start-session --target i-XXXXXXXXXXXX --region us-east-1

   Example:


$ aws ssm describe-instance-information --region us-east-1 --query "InstanceInformationList[].InstanceId"
[
    "i-0f17bdafd6de45ece"
]

Starting session with SessionId: admin-39cl68p2v9pgi6og2vijy7ljdy
sh-5.2$ 
sh-5.2$


**Post connecting the nodes, kubesystem PODs show up as below:**

$ kubectl get pods -n kube-system
NAME                              READY   STATUS      RESTARTS   AGE
aws-node-mml9w                    2/2     Running     0          17m
coredns-5959c9b9c4-26sx6          0/1     Completed   0          74m
coredns-5959c9b9c4-4pt6t          1/1     Running     0          17m
coredns-5959c9b9c4-ddqv6          1/1     Running     0          17m
coredns-5959c9b9c4-hlr2b          0/1     Completed   0          74m
kube-proxy-42p52                  1/1     Running     0          17m
metrics-server-7b78764d44-2cmqv   0/1     Completed   0          70m
metrics-server-7b78764d44-7ttrb   1/1     Running     0          17m
metrics-server-7b78764d44-hskxt   1/1     Running     0          17m
metrics-server-7b78764d44-jq7xp   0/1     Completed   0          70m


**Real Surprise**

Once I did kubectl get pods it listed 5-6 pods, and I didn't notice all their names, at this point I was thinking that I will be able to connect to all these nodes, but I was able to connect only a single node using SSM.

## To Delete the Cluster:

Run eksctl delete cluster -f cluster.yaml 

**Tearddown proof:**

2026-07-14 14:36:51 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-nodegroup-standard-nodes"
2026-07-14 14:37:22 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-nodegroup-standard-nodes"
2026-07-14 14:38:09 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-nodegroup-standard-nodes"
2026-07-14 14:39:09 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-nodegroup-standard-nodes"
2026-07-14 14:40:19 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-nodegroup-standard-nodes"
2026-07-14 14:42:03 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-nodegroup-standard-nodes"
2026-07-14 14:43:31 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-nodegroup-standard-nodes"
2026-07-14 14:43:32 [ℹ]  will delete stack "eksctl-portfolio-cluster-cluster"
2026-07-14 14:43:32 [ℹ]  waiting for stack "eksctl-portfolio-cluster-cluster" to get deleted
2026-07-14 14:43:32 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-cluster"
2026-07-14 14:44:03 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-cluster"
2026-07-14 14:44:36 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-cluster"
2026-07-14 14:45:41 [ℹ]  waiting for CloudFormation stack "eksctl-portfolio-cluster-cluster"
2026-07-14 14:45:42 [✔]  all cluster resources were deleted

## Completed vs Running Pods:

**Completed Pods** - Are the ones which have fulfilled there taks and have exited. 
**Running Pods** - These are the pods that are still running some processes thats why they are up for the last 17 minutes only.
