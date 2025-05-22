## Create and configure the deployment environment:
- #### Setup an EC2 instance:
  - Create an EC2 instance using AWS Management Console -> EC2 -> Launch Instance. I launched kubernetes-bootcamp-server [i-074ca054688a7d39a](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#InstanceDetails:instanceId=i-074ca054688a7d39a).
  - Create a security group which allows SSH, HTTP and HTTPS traffic. I created [sg-0248a255eda00ccbc - launch-wizard-3](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#SecurityGroup:securityGroupId=sg-0248a255eda00ccbc).
  - Create an IAM user with AdministratorAccess access and associate an Secret Access key using Security credentials tab for performing various CLI operations. Download .csv file button to get the access key and secret key. I created the accas key for IAM user eruser311 
  -  Connnect to the EC2 instance created above and configure the access keys through **aws configure** using the .csv file downloaded above. Sample output:<br><br>
     [ec2-user@ip-172-31-93-237 ~]$ aws configure<br>
     AWS Access Key ID [****************TQEH]:<br>
     AWS Secret Access Key [****************mSVI]:<br> 
     Default region name [us-east-1]:<br>
     Default output format [None]:<br>
     [ec2-user@ip-172-31-93-237 ~]$
- #### Install Kubernetes:
  - Execute the following commands:<br><br>
    curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.31.2/2024-11-15/bin/linux/amd64/kubectl<br>
    chmod +x ./kubectl<br>
    mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH<br>
  - Type **kubectl** then press RETURN for verification of the installation: Sample output:<br><br>
    Usage:<br>
    kubectl [flags] [options]<br><br>
    Use "kubectl <command> --help" for more information about a given command.<br>
    Use "kubectl options" for a list of global command-line options (applies to all commands).
- #### Install eksctl:
  - Set the following variables:<br>
    export ARCH=amd64<br>
    export PLATFORM=$(uname -s)_$ARCH<br>
  - Execute the following commands:<br><br>
    curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"<br>
    tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz<br>
    sudo mv /tmp/eksctl /usr/local/bin<br>
  - Type **eksctl** then press RETURN for verification of the installation: Sample output:<br><br>
    Usage: eksctl [command] [flags]<br><br>
    Commands:<br>
       eksctl anywhere                        EKS anywhere<br>
       eksctl associate                       Associate resources with a cluster<br>
       eksctl completion                      Generates shell completion scripts for bash, zsh or fish<br>
- #### Install Docker:
  - Use command sudo yum install docker.
  - Type **docker** then press RETURN for verification of the installation: Sample output:<br><br>
    Run 'docker COMMAND --help' for more information on a command.<br><br>
    For more help on how to use Docker, head to https://docs.docker.com/go/guides/
- #### Install GIT:
  - Use command sudo yum install git.
  - Type **git** then press RETURN for verification of the installation: Sample output:<br><br>
    'git help -a' and 'git help -g' list available subcommands and some<br>
    concept guides. See 'git help <command>' or 'git help <concept>'<br><br>
    to read about a specific subcommand or concept.<br>
    See 'git help git' for an overview of the system.
- #### Install Node:
  - Execute the following commands:<br><br>
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash<br>
    source ~/.bashrc<br>
    nvm install --lts<br>
  - Type **npm** then press RETURN for verification of the installation: Sample output:<br><br>
    More configuration info: npm help config<br>
    Configuration fields: npm help 7 config<br><br>
    npm@10.9.2 /home/ec2-user/.nvm/versions/node/v22.15.1/lib/node_modules/npm
