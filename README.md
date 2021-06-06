# Application-Deployment-using-Kubernetes
Simple Mongo DB and Mongo Express Setup using Kubernetes

# Overview of Kubernetes Componentes

- We create a **MongoDB** Pod in which to talk to the pod we will need an internal service which will not allow any external requests.
- We create **Mongo Express Pod** which requires DB URL and login credentials from MongoDB.
- To pass these configurations we will create a **config map** which stores DB URL and **Secret File** which stores the credentials. 
- The Config Map and Secret File will be referenced in **mongo.yaml** file as Environment Variables. 
- At last we need an **external service** which allows us to talk to Mongo Express Pod. The type will be a **Loadbalancer**.

## The Request Flow:

Request comes from Browser ----> Mongo Express External Service ----> Mongo Express ----> Mongo DB Internal Service ----> Mongo DB

##  How to Deploy the Project

First of all you could edit the [Secret Yaml File](http://github.com/gunishjain/Application-Deployment-using-Kubernetes/blob/main/mongo-secret.yaml "Secret Yaml File") and add your own username and password. ***Remember to convert it into Base64 type. ***.  In my case the username is admin and password is gunish(converted to base64)

Step 1:

    kubectl apply -f mongo-secret.yaml
    kubectl get secret

Step 2: 

    kubectl apply -f mongo-configmap.yaml
    kubectl apply -f mongo-express.yaml

Step 3:

    minikube service mongo-express-service 

This command should open browser window running mongo-express ! Otherwise you could see the console to find the ip address of the running service. 
