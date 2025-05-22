#### Update your application with a blue/green deployment
- ## Create two deployments for web application:
  - Continue from the previous step of scaling the application. Change the directory to backend using command **cd ./aws-engagement-kubernetes-capstone/4_deploy_web_application/frontend/**.
  - The web application is currently running on version 1.0. Create a copy of web-deployment.yaml file using the command **cp web-deployment.yaml web-deployment-v2.yaml**.
  - Edit the new web-deployment-v2.yaml file and modify the following attributes:<br>
    "name: events-web" to "name: events-web-v2.0"<br>
    "ver: v1.0" labels to "ver: v2.0"<br>
    Container image URL from v1:0 to v2:0
    replica from 1 to 4
  - Change the value of relica attribute to 4 in both web-deployment.yaml and api-deployment.yaml files.
  - Execute the following commands to apply the changes:<br>
    kubectl apply -f api-deployment.yaml<br>
    kubectl apply -f web-deployment.yaml
  - Execute the command **kubectl get pods** to verify that the pods are getting added to maintain the desired count. Sample output:<br>
    NAME                          READY   STATUS      RESTARTS   AGE<br>
    db-initializer-8cgzk          0/1     Completed   0          98m<br>
    events-api-85bbfdbbc6-8z4ks   1/1     Running     0          66s<br>
    events-api-85bbfdbbc6-jfxmg   1/1     Running     0          69m<br>
    events-api-85bbfdbbc6-xclzh   1/1     Running     0          66s<br>
    events-api-85bbfdbbc6-zd867   1/1     Running     0          66s<br>
    events-web-5f66656cc4-m7f8b   1/1     Running     0          8s<br>
    events-web-5f66656cc4-nmm7l   1/1     Running     0          8s<br>
    events-web-5f66656cc4-pbqvv   1/1     Running     0          8s<br>
    events-web-5f66656cc4-r9hvp   1/1     Running     0          81m<br>
    prashant-mariadb-server-0     1/1     Running     0          3h7m
  - Relaunch the application and verify that it is displaying all the relevant records.
  - Execute the command **kubectl apply -f web-deployment-v2.yaml** to apply the changes for web-deployment-v2.yaml.
  - Execute the command **kubectl get deployments** to verify the deployments. Sample output:<br>
    NAME             READY   UP-TO-DATE   AVAILABLE   AGE<br>
    events-api       4/4     4            4           74m<br>
    events-web       4/4     4            4           85m<br>
    events-web-2.0   1/1     1            1           6s
  - Execute the command **kubectl get pods** to verify that the pods are getting added to maintain the desired count. Sample output:<br>
    NAME                              READY   STATUS      RESTARTS   AGE<br>
    db-initializer-8cgzk              0/1     Completed   0          104m<br>
    events-api-85bbfdbbc6-8z4ks       1/1     Running     0          6m50s<br>
    events-api-85bbfdbbc6-jfxmg       1/1     Running     0          75m<br>
    events-api-85bbfdbbc6-xclzh       1/1     Running     0          6m50s<br>
    events-api-85bbfdbbc6-zd867       1/1     Running     0          6m50s<br>
    events-web-2.0-654dfc7b94-6lqfh   1/1     Running     0          59s<br>
    events-web-2.0-654dfc7b94-7vwx2   1/1     Running     0          59s<br>
    events-web-2.0-654dfc7b94-mlzx8   1/1     Running     0          59s<br>
    events-web-2.0-654dfc7b94-w7wmt   1/1     Running     0          59s<br>
    events-web-5f66656cc4-m7f8b       1/1     Running     0          5m52s<br>
    events-web-5f66656cc4-nmm7l       1/1     Running     0          5m52s<br>
    events-web-5f66656cc4-pbqvv       1/1     Running     0          5m52s<br>
    events-web-5f66656cc4-r9hvp       1/1     Running     0          86m<br>
    prashant-mariadb-server-0         1/1     Running     0          3h13m
- ## The Load Balancer is pointing to application version 1.0, switch it to version 2.0:
  - Update the selector from "ver: v1.0" to "ver: v2.0" in web-service.yaml and apply the changes using the command **kubectl apply -f web-service.yaml**.
  - Execute the command **kubectl get svc** to verify the services.
  - Relaunch the application and verify that it is pointing to the version 2.0 as well as displaying all the relevant records.
- ## The Load Balancer is pointing to application version 2.0, roll it back to version 1.0:
  - Update the selector from "ver: v2.0" to "ver: v1.0" in web-service.yaml and apply the changes using the command **kubectl apply -f web-service.yaml**.
  - Execute the command **kubectl get svc** to verify the services.
  - Relaunch the application and verify that it is pointing to the version 1.0 as well as displaying all the relevant records.
    
  
