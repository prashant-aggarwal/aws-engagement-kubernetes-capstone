#### Deploy an EKS cluster:
- ## Create a cluster:
  - Create a directory 3_deploy_eks_clutser under ~/prashant/aws-engagement-kubernetes-capstone directory.
  - Create cluster.yaml file in ~/prashant/aws-engagement-kubernetes-capstone/3_deploy_eks_clutser directory.
  - Create an EKS cluster using command **eksctl create cluster -f cluster.yaml** which may take some time. Sample output:<br>
    kubectl command should work with "/home/ec2-user/.kube/config", try 'kubectl get nodes'<br>
    EKS cluster "pa-cap-eks-cluster" in "us-east-2" region is ready.
  - Run the following commands to view the various resources deployed inside the EKS cluster<br>
  kubectl cluster-info<br>
  kubectl get services<br> 
  kubectl get nodes<br>
  kubectl get pods  
  - Verify the cluster state in AWS Console [pa-cap-eks-cluster](https://us-east-2.console.aws.amazon.com/eks/clusters/pa-cap-eks-cluster?region=us-east-2). There should be three Nodes of type t3.medium in Ready Status.

