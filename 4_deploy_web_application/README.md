## Deploy a 3-tier web application including the backend database
- #### Install database MariaDB on the cluster with the help of Helm charts:
  - Change the directory to backend using command **cd ./aws-engagement-kubernetes-capstone/4_deploy_web_application/sample-application/backend/**.
  - Execute the following commands:<br>
    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3<br>
    chmod 700 get_helm.sh<br>
    ./get_helm.sh
  - Type helm then press RETURN for verification of the installation.    
  - Execute the following command to install the chart:<br>
    helm install prashant-mariadb-server oci://registry-1.docker.io/bitnamicharts/mariadb
  - The information is displayed about how to obtain the database root password.
  - Execute the following commands to check the installation:<br>
    kubectl get pods
    kubectl get statefulsets
    kubectl get service
  - If the Maria DB server pod is not running or appearing in Ready state, then execute the following command to set the default storage class:<br>
    kubectl patch storageclass gp2 -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
  - Execute command **kubectl get sc** to verify that the default storage class is set. Sample output:<br>
    NAME            PROVISIONER             RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE<br>
    gp2 (default)   kubernetes.io/aws-ebs   Delete          WaitForFirstConsumer   false                  4h44m
- #### Install the backend API:
  - Execute the following commands to install a service of type ClusterIP listening on port 8082 and a deployment with replicaset:<br>
    kubectl apply -f api-service.yaml<br>
    kubectl apply -f api-deployment.yaml
  - Execute the command **kubectl get pods** to verify that the backend pods are running. Sample output:<br>
    NAME                          READY   STATUS    RESTARTS   AGE<br>
    events-api-85bbfdbbc6-2rzpx   1/1     Running   0          4s<br>
    events-api-85bbfdbbc6-92zg2   1/1     Running   0          4s<br>
    events-api-85bbfdbbc6-gd9d6   1/1     Running   0          4s<br>
    prashant-mariadb-server-0     1/1     Running   0          67s
- #### Install the website:
  - Change the directory to frontend using command **cd ../frontend/**.
  - Execute the following commands to install a service of type LoadBalancer listening on port 8080 and a deployment with replicaset:<br>
    kubectl apply -f web-service.yaml<br>
    kubectl apply -f web-deployment.yaml
  - Execute the command **kubectl get pods** to verify that the frontend pods are running. Sample output:<br>
    NAME                          READY   STATUS    RESTARTS   AGE<br>
    events-api-85bbfdbbc6-2rzpx   1/1     Running   0          14m<br>
    events-api-85bbfdbbc6-5x4rw   1/1     Running   0          97s<br>
    events-api-85bbfdbbc6-mv4hf   1/1     Running   0          6m58s<br>
    events-web-5f66656cc4-mgngs   1/1     Running   0          24s<br>
    events-web-5f66656cc4-qgcbk   1/1     Running   0          24s<br>
    events-web-5f66656cc4-s8wr7   1/1     Running   0          24s<br>
    events-web-5f66656cc4-xrfrj   1/1     Running   0          24s<br>
    prashant-mariadb-server-0     1/1     Running   0          95s<br>
- #### Verify that the application is running and able to maintain the state:
  - Execute the command **kubectl get svc** to view the various services which are running. Sample output:<br>
    NAME                               TYPE           CLUSTER-IP       EXTERNAL-IP                                                               PORT(S)        AGE<br>
    events-api-svc                     ClusterIP      10.100.12.98     <none>                                                                    8082/TCP       30m<br>
    events-web-svc                     LoadBalancer   10.100.171.69    a97543b4264c64732affe918fe3df302-1411613217.us-east-2.elb.amazonaws.com   80:30624/TCP   4m37s<br>
    kubernetes                         ClusterIP      10.100.0.1       <none>                                                                    443/TCP        5h22m<br>
    prashant-mariadb-server            ClusterIP      10.100.140.121   <none>                                                                    3306/TCP       19m<br>
    prashant-mariadb-server-headless   ClusterIP      None             <none>                                                                    3306/TCP       19m
  - Launch the application by prefixing http:// with the EXTERNAL-IP value of events-web-svc e.g. http://a97543b4264c64732affe918fe3df302-1411613217.us-east-2.elb.amazonaws.com/. It should display two records.
  - Add one or more records using **Add an event** button followed by **submit**.
  - Relaunch the application and verify that it is displaying all the relevant records.
- #### Verify that the application is able to scale automatically and able to maintain the state:
  - Change the value of relica attribute to 1 in both web-deployment.yaml and api-deployment.yaml files.
  - Execute the following commands to apply the changes:<br>
    kubectl apply -f web-service.yaml<br>
    kubectl apply -f web-deployment.yaml
  - Execute the command **kubectl get pods** to verify that the pods are getting terminating to maintain the desired count. Sample output:<br>
    NAME                          READY   STATUS        RESTARTS   AGE<br>
    events-api-85bbfdbbc6-2rzpx   1/1     Terminating   0          38m<br>
    events-api-85bbfdbbc6-5x4rw   1/1     Running       0          25m<br>
    events-api-85bbfdbbc6-mv4hf   1/1     Terminating   0          30m<br>
    events-web-5f66656cc4-xrfrj   1/1     Running       0          24m<br>
    prashant-mariadb-server-0     1/1     Running       0          25m
  - Relaunch the application and verify that it is displaying all the relevant records.
  - Change the value of relica attribute to 3 in both web-deployment.yaml and api-deployment.yaml files.
  - Execute the following commands to apply the changes:<br>
    kubectl apply -f web-service.yaml<br>
    kubectl apply -f web-deployment.yaml
  - Execute the command **kubectl get pods** to verify that the  are getting added to maintain the desired count. Sample output:<br>\
    NAME                          READY   STATUS    RESTARTS   AGE<br>
    events-api-85bbfdbbc6-5x4rw   1/1     Running   0          35m<br>
    events-api-85bbfdbbc6-7grjx   1/1     Running   0          58s<br>
    events-api-85bbfdbbc6-m6g92   1/1     Running   0          58s<br>
    events-web-5f66656cc4-5c5nx   1/1     Running   0          42s<br>
    events-web-5f66656cc4-hdz9r   1/1     Running   0          42s<br>
    events-web-5f66656cc4-xrfrj   1/1     Running   0          34m<br>
    prashant-mariadb-server-0     1/1     Running   0          35m
