# Test Project

# Code Walkthrough

For the Dockization of a simple Python–Flask web Application, I have created 3 separate containers based on the requirement mentioned by Red Acre team.
# (Task 1)
1.for the Backend

Backend (Python app) is added with one Dockerfile and docker-compose.yml to build the docker image. For this run, the command “docker build -t my_python_app:0.1  .”

2.For Proxy and load balance.
 
Nginx is a web server that can also be used as a reverse proxy, and load balancer. So, for the proxy server “docker-compose-nginx.yml” file is added to expose the frontend using nginx along with the default configuration file.

3.For Backend-React (sys-stats)
     
Backend (React app) is added with one Dockerfile and docker-compose.yml to build the docker image. For this run, the command “docker build -t my_react_app:0.1  .”
4.Docker-compose main file is created (docker-compose-main.yml)  to aggregate the output of each container. Run the command “docker-compose up - -build” 
 
5.To check whether your application running properly in Docker containers, Run these commands
   for Python-flask app
 “docker run - -name backend-app -p  5000:5000 python_app:0.1”
   for React-app 
 “docker run - -name frontend-app -p  3000:3000 react_app:0.1”

# (Task 3)

6.Kubernetes is an open-source container orchestration system for automating software deployment, scaling, and management. But Minikube is a lightweight Kubernetes implementation that creates a VM on your local machine.
So, to automate operational tasks of docker containers on the local machine 
We need to install minikube. so that this tool lets you run Kubernetes locally. 
=> To start minikube, you need to run the command “start minikube”
=> To check the minikube dashboard run the command “minikube dashboard”
=> We need to load the docker images to minikube. Run there commands 

 “minikube image load  python_app:0.1”
 “ minikube image load  react_app:0.1”

7.Deployment 
 It’s basically a set of pods, in which we need to do container orchestration for this application. two containers into separate pods. I have written separate yml scripts. 

 kubectl commands are used:
 To run the react js app run the command 
“kubectl create -f react_dep.yml” 
“kubectl create -f python_dep.yml”
After that expose the node port using these commands
“Kubectl expose deployment react-deployment  --type=NodePort  --port=3000 –name react-svc -o yml > react_sv.yml”

“Kubectl expose deployment react-deployment  --type=NodePort  --port=3000 –name react-svc -o yml > python_svc.yml”

8.To Run Ingress 
“Kubectl create -f ingress.yml”

# (Task 2)
9.Deploy on Cloud 

we have a docker image for both the backend and frontend app and that is pushed to AWS ECR (Amazon Elastic Container Registry) and then now we need to deploy these containers in the Amazon Elastic Kubernetes services (EKS) with ansible.

Create an AWS EKS Cluster based on the requirement of nodes and also Autoscaling is configured manually for EKS. The container image tag in ECR is copied and added to the deployment.yaml file in the containers image section. All other files in eks like
aws-auth.yaml, ingress.yaml, and service.yaml is the support for cluster authentication and the ingress file exposes HTTP routes from outside the cluster to services within the cluster.


10.k9s a terminal-based UI is installed on the ec2-user to interact with the Kubernetes cluster. kubectl commands are used to deploy the application 

Run these command 
 “kubectl apply -f eks/deployment.yml”. 
 “kubectl apply -f eks/service.yml”.
