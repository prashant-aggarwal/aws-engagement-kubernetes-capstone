## Containerize the application and store it in a repository:
- #### Run an application as a container in Docker:
  - Create directory eventsapp using **mkdir -p prashant/aws-engagement-kubernetes-capstone/1_environment_setup/eventsapp** command.
  - Change the directory using **cd eventsapp** command.
  - Pull the Git repository containing test application using the following commands:<br>
    git init<br>
    git pull https://github.com/msutton150/eventsappstart.git<br>
  - Run **ls -la** command to view the directory contents.
  - Change the directory using **cd events-api** command.
  - Execute the following commands to install dependencies and run the service. Leave the service in running state.<br>
    npm install<br>
    node server.js
    
- Create Docker images for the application used for the project.
- Configure an image repository to store and retrieve images in either Dockerhub or ECR.
- Test the container registry in order to deploy, store, and retrieve images.
- Store multiple versions of the same image in the image repository.
