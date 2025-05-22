## Create and configure the deployment environment:
- #### Setup an EC2 instance:
  - Create an EC2 instance using AWS Management Console -> EC2 -> Launch Instance. I launched kubernetes-bootcamp-server [i-074ca054688a7d39a](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#InstanceDetails:instanceId=i-074ca054688a7d39a).
  - Create a security group which allows SSH, HTTP and HTTPS traffic. I created [sg-0248a255eda00ccbc - launch-wizard-3](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#SecurityGroup:securityGroupId=sg-0248a255eda00ccbc).
  - Create an IAM user with AdministratorAccess access and associate an Secret Access key using Security credentials tab for performing various CLI operations. Download .csv file button to get the access key and secret key. I created the accas key for IAM user eruser311 
  -  Connnect to the EC2 instance created above and configure the access keys through **aws configure** using the .csv file downloaded above. Sample output:
     <p>  
     [ec2-user@ip-172-31-93-237 ~]$ aws configure
     AWS Access Key ID [****************TQEH]: 
     AWS Secret Access Key [****************mSVI]: 
     Default region name [us-east-1]: 
     Default output format [None]: 
     [ec2-user@ip-172-31-93-237 ~]$
     </p> 
- #### Install Kubernetes:
  -    
