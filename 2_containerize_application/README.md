## Containerize the application and store it in a repository:
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
- #### Configure an image repository to store and retrieve images:
- #### Test the container registry in order to deploy, store, and retrieve images.
- #### Store multiple versions of the same image in the image repository.
