## Containerize the application and store it in an image repository:
- #### Run an application as a container in Docker:
  - Create directory eventsapp using **mkdir -p prashant/aws-engagement-kubernetes-capstone/2_containerize_application/eventsapp/** command.
  - Change the directory using **cd eventsapp** command.
  - Pull the Git repository containing test application using the following commands:<br>
    git init<br>
    git pull https://github.com/msutton150/eventsappstart.git<br>
  - Run **ls -la** command to view the directory contents.
  - Change the directory using **cd events-api** command.
  - Execute the following commands to install dependencies and run the service. Leave the service in running state.<br>
    npm install<br>
    node server.js
  - Open another session for the EC2 instance for running web application using the following commands:<br>
    cd ~/eventsapp/events-website/<br>
    npm install<br>
    npm start
  - Update the security group [sg-0248a255eda00ccbc - launch-wizard-3](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#SecurityGroup:securityGroupId=sg-0248a255eda00ccbc) attached to the EC2 instance to allow traffic for ports 8080 and 8082 by creating inbound rules.
  - Copy the public DNS name of the EC2 server, paste in a browser, and append :8080 to the address to test the application for e.g. http://ec2-3-84-204-165.compute-1.amazonaws.com:8080/.
  - Stop the services by pressing CTRL+C in both the sessions.
- #### Create Docker images for the application:
  - Create separate Dockerfile files in both the events-api and events-website folders with relevant instructions.
  - Run the command **docker build . -t events-api:v1.0** in the events-api folder for creation of Docker image for events-api.
  - Run the command **docker build . -t events-website:v1.0** in the events-website folder for creation of Docker image for events-website.
  - Run the command **docker images** to view the Docker images created above. Sample output:<br>
    REPOSITORY                                                    TAG       IMAGE ID       CREATED         SIZE<br>
    events-website                                                v1.0      29dca6e718d5   5 seconds ago   264MB<br>
    events-api                                                    v1.0      05ce7fa7a8d5   2 minutes ago   255MB
  - Run both the applications locally in Docker containers using the following commands:<br>
  docker run -d -p 8082:8082 events-api:v1.0<br>
  docker run -d -p 8080:8080 -e SERVER='http://localhost:8082' --network="host" events-website:v1.0
  - Test the application is working using http://ec2-3-84-204-165.compute-1.amazonaws.com:8080/.
- #### Configure an image repository to store and retrieve images in AWS Elastic Container Registry (ECR):
  - Create private repositories as [events-api](https://us-east-1.console.aws.amazon.com/ecr/repositories/private/021668988309/events-api?region=us-east-1) and [events-website](https://us-east-1.console.aws.amazon.com/ecr/repositories/private/021668988309/events-website?region=us-east-1).
  - Use the following commands to login to ECR and push the images to their respective repositories. Replace events-api with events-website for pushing website image:<br>
  docker login -u AWS -p $(aws ecr get-login-password --region us-east-1) 021668988309.dkr.ecr.us-east-1.amazonaws.com/events-api<br>
  docker build -t events-api .<br>
  docker tag events-api:latest 021668988309.dkr.ecr.us-east-1.amazonaws.com/events-api<br>
  docker push 021668988309.dkr.ecr.us-east-1.amazonaws.com/events-api:latest
- #### Run the containers using image from container registry:
  - Stop the previous containers using **docker rm <container_id>** command. container_id can be identified using **docker ps -a** command.
  - Run both the applications locally in Docker containers using the following commands:<br>
  docker run -d -p 8082:8082 021668988309.dkr.ecr.us-east-1.amazonaws.com/events-api:latest<br>
  docker run -d -p 8080:8080 -e SERVER='http://localhost:8082' --network="host" 021668988309.dkr.ecr.us-east-1.amazonaws.com/events-website:latest
- #### Store multiple versions of the same image in the image repository:
  - Edit the file ~/eventsapp/events-website/views/layouts/default.hbs for changing the text.
  - Build the image and push it to [events-website](https://us-east-1.console.aws.amazon.com/ecr/repositories/private/021668988309/events-website?region=us-east-1) using the following commands:<br>
  docker build -t events-website .<br>
  docker tag events-website:latest 021668988309.dkr.ecr.us-east-1.amazonaws.com/events-website<br>
  docker push 021668988309.dkr.ecr.us-east-1.amazonaws.com/events-website:v2.0
