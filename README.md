# Spring_boot
Docker Image Name : shashivish123/exploration

Pre-requisite : MiniKube Cluster 
Step 1: Start Your Kubernetes cluster if not running . In below example ,we will be using Minikube cluster for development purpose.
Step 2: Now since our cluster is running fine , we will start by create a namespace where we will deploy our Kubernetes Pods and Services.
>kubectl create namespace casdemo
Next step is to create manifest file which will be used for creating pods and services.
>kubectl create deployment casdemo --image=shashivish123/casexploration:latest --dry-run -o=yaml > deployment.yaml
>kubectl create service clusterip casdemo --tcp=8080:8080 --dry-run -o=yaml > service.yaml
Step 4 : Deployment file points to spring boot application image and it pull that image once Pod is being created.
>kubectl create -f deployment.yaml  -n casdemo
>kubectl create -f service.yaml  -n casdemo
Step 5: Let's make sure that everything is up and running state.
>kubectl get all -n casdemo
Step 6 : Now we will enable port forwarding for accessing Spring boot application.
>kubectl port-forward service/casdemo  8080:8080 -n casdemo
Step 7 : Let's check if we are able to access application using curl command or alternatively you can also check in browser.
>curl http://localhost:8080/actuator/health
