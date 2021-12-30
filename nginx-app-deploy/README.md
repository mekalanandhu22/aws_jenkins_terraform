This repo consists of terraform scripts to deploy nginx as a pod in an AWS kubernetes cluster i.e. EKS.

Also Repo has a Jenkinsfile that can be used on any jenkins instance to deploy the nginx app after making changes.

This repo in combination with terraform-eks-cluster-provision can be used to deploy a kubernetes cluster and also an nginx app. If you want to update the nginx version, you will need to update the image value accordingly in the kubernetes.tf file.

Things required to execute these scripts,

1. AWS credentials i.e. ACCESS_KEY and SECRET_KEY and the aws cli has to be configured locally on the machine from which it is being executed. If this is being run in CI tool like jenkins then the ACCESS_KEY and SECRET_KEY have to be added in the credentials section of the jenkins settings.

2. terraform has to be installed locally or on the CI runner machines that will execute the code.

3. kubectl utility has to be installed locally or on the CI runner machine.


To deploy the pod manually in an EKS cluster, give the below commands.

# First create the deployment
kubectl create deployment nginx --image=nginx

# Create the service to expose the pods
kubectl expose deployment nginx --port=80 --target-port=80 --type=LoadBalancer --name=nginx-svc

# check the services to get the loadbalancer name and port details
kubectl get svc

Take a note of loadbalancer value and the port value and give the same in the browser. 

