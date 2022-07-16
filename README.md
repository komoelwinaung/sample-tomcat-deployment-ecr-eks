# sample-tomcat-deployment-ecr-eks
Deploy Sample Tomcat from ECS to EKS

Idea & Tutorial Credit to 
https://towardsdatascience.com/kubernetes-application-deployment-with-aws-eks-and-ecr-4600e11b2d3c
https://hiberstack.com/deploy-war-file-on-tomcat-docker-container/

Prerequisites and Testing Environment! AWS Account, Cli, EKS, ECS, kubectl, eksctl and Docker Desktop on Windows.

1. Create a new repo in AWS ECR.

2. Create a new docker image using local Docker Desktop and push to ECR.
   2.1 docker build -t sample-tomcat-hello .
   2.2 docker images
   2.3 aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin accID.ecr.ap-southeast-1.amazonaws.com
   2.4 docker tag yourlocalimageid public.ecr.aws/n9xxxv0/reponame:imagename
   2.5 docker push public.ecr.aws/n9q3x4v0/reponame:imagename
   
3. Then, deploy a new pod using your ECR image in AWS EKS
* kubectl apply -f hello.yaml 
* expose your service with ELB - kubectl expose deployment/hello --port 80 --target-port 80 --name hello-service --type LoadBalancer

Finally, browse your ELB url, can see your sample deployment page. That's it. Thanks!
