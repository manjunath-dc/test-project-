# Process used to connect Kubernetes cluster on AWS EKS with kubectl and k9s

# Step 1:  Install kubectl on your local host machine. Or, if you have a dedicated Amazon Elastic Compute Cloud (Amazon EC2) instance with a kubectl package installed, use SSH to connect to the instance.

# step 2: On the same host machine where kubectl is installed, configure the AWS CLI with the designated_user credentials:  aws configure

# step 3:  In the AWS CLI, run the following command: aws sts get-caller-identity
           The output should return the IAM user details for designated_user.
example:
       {
    "UserId": "XXXXXXXXXXXXXXXXXXXXX",
    "Account": "XXXXXXXXXXXX",
    "Arn": "arn:aws:iam::XXXXXXXXXXXX:user/designated_user"
}

# step 4: List the pods that are running in the cluster of the default namespace: kubectl get pods --namespace default

# step 5: if the output shows the following: "Unauthorized error" Configure the AWS access key ID and the AWS secret access key of cluster_creator.
          created a cluster using the AWS Management Console, then identify the IAM role or user that created the cluster. In the host machine where kubectl is installed, 
          configure the cluster_creator IAM user or role in the AWS CLI: aws configure

# step 6: Verify that cluster_creator has access to the cluster: kubectl get pods

# step 7: To give designated_user access to the cluster, add the mapUsers section to your aws-auth.yaml file. aws-auth.yaml is add in the eks folder 

# step 8: Apply the new ConfigMap to the RBAC configuration of the cluster: kubectl apply -f aws-auth.yaml

# step 9: if you need to configure again Change the AWS CLI configuration again to use the credentials of designated_user.

# step 10: To interact with kubernetes cluster: use kubectl tools 
            1. kubectl get service 
            2. To get list of pods : kubectl get pods 
# step 11: K9s is a terminal based UI to interact with your Kubernetes clusters. very useful and I recommend.
            Via Scoop for Windows : scoop install k9s
