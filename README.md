<h1 align="center">AWS Kubernetes Capstone Project</h1><br>
Demonstrate the knowledge by successfully completing the following use case scenarios. Clone this repository using command **git clone https://github.com/prashant-aggarwal/aws-engagement-kubernetes-capstone.git and follow the instructions provided below:

1. #### Create and configure the deployment environment:
   - Deploy an environment to use tools such as Docker, Kubernetes, EKSCTL, and any tools required to test your application.
   - Refer to these [instructions](https://github.com/prashant-aggarwal/aws-engagement-kubernetes-capstone/blob/main/1_environment_setup/README.md).
2. #### Containerize the application and store it in a repository:
   - Create Docker images for the application used for the project.
   - Configure an image repository to store and retrieve images in either Dockerhub or ECR.
   - Test the container registry in order to deploy, store, and retrieve images.
   - Store multiple versions of the same image in the image repository.
   - Refer to these [instructions](https://github.com/prashant-aggarwal/aws-engagement-kubernetes-capstone/blob/main/2_containerize_application/README.md).
3. #### Deploy an EKS cluster:
   - Using eksctl, deploy an Amazon EKS cluster using a pre-defined template. Modify the template to include appropriate region, instance types, replicas etc.
   - Refer to these [instructions](https://github.com/prashant-aggarwal/aws-engagement-kubernetes-capstone/blob/main/3_deploy_eks_clutser/README.md).
4. #### Deploy a 3-tier web-based application including the backend database:
   - Deploy the application in a declarative way in an Amazon EKS cluster.
   - The application should be able to scale automatically, use services as necessary, include a backend database, and the configuration should be repeatable.
   - Either use your own or any third party application.
   - Refer to these [instructions](https://github.com/prashant-aggarwal/aws-engagement-kubernetes-capstone/blob/main/4_deploy_web_application/README.md).
5. #### Update your application with a blue/green deployment:
   - Configure the application to be updated via blue/green deployment.
   - Refer to these [instructions](https://github.com/prashant-aggarwal/aws-engagement-kubernetes-capstone/blob/main/5_perform_rolling_updates/README.md).
