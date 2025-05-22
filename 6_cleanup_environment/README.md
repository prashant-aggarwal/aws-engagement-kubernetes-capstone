## Perform a cleanup of the resources that have been deployed from the previous steps:
   - Execute the **eksctl delete cluster pa-cap-eks-cluster --region us-east-2** command to cleanup resources:
   - This may take a while to complete. Sample output after completion:<br>
     will delete stack "eksctl-pa-cap-eks-cluster-addon-vpc-cni"<br>
     will delete stack "eksctl-pa-cap-eks-cluster-addon-aws-ebs-csi-driver"<br>
     will delete stack "eksctl-pa-cap-eks-cluster-cluster"<br>
     all cluster resources were deleted
   - Verify that the cluster [pa-cap-eks-cluster](https://us-east-2.console.aws.amazon.com/eks/clusters/pa-cap-eks-cluster?region=us-east-2) is no longer available in the console.
