Next.js App - Dockerized and Deployed on Kubernetes

Project Overview:

 --> Containerized a Next.js app, automated build and push to GitHub Container Registry (GHCR) using GitHub Actions, and deployed it to Kubernetes (Minikube).

Setup Instructions:
...................

SERVER REQUIREMENTS: 2 CPUs or more, 2GB of free memory, 20GB of free disk space

Install Minikube:

--> Clone this repo -> https://github.com/NaveenKumar-0/installlation-scripts.git 
      CMD - git clone https://github.com/NaveenKumar-0/installlation-scripts.git 
      CMD - cd installation-scripts
      CMD -  sh ubuntu-minikube.sh

NOTE:  ( you can use your own minikube installation script )
 _`````````````````````````````````````````````````````````````

--> Check the minikube status: 
      CMD - minikube status

--> Start Minikube (if not running): 
      CMD - minikube start

--> Verify cluster:
      CMD - kubectl cluster-info ( should get cluster info like below )
      
      Kubernetes control plane is running at https://192.168.49.2:8443
      CoreDNS is running at https://192.168.49.2:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

NEXT: Deploy Application

--> Clone the repo:
      CMD - git clone https://github.com/NaveenKumar-0/DevOps-Internship-Assessment.git
      CMD - cd DevOps-Internship-Assessment

--> Running manifest files ( deployement.yaml and service.yaml )
      CMD - kubectl apply -f k8s/


--> Check pods and services:
      CMD - kubectl get pods
      CMD - kubectl get svc

--> Get Minikube IP:
      CMD - minikube ip

--> Get NodePort of service:
      CMD - kubectl get svc

NEXT:

--> CMD - minikube service nextjs-service ( Should get output like below )

┌───────────┬────────────────┬─────────────┬───────────────────────────┐
│ NAMESPACE │      NAME      │ TARGET PORT │            URL            │
├───────────┼────────────────┼─────────────┼───────────────────────────┤
│ default   │ nextjs-service │ 3000        │ http://192.168.49.2:31111 │
└───────────┴────────────────┴─────────────┴───────────────────────────┘
* Opening service default/nextjs-service in default browser...
  http://192.168.49.2:31111

--> Open in browser:
http://<minikube-ip>:<node-port>
Example: http://192.168.49.2:31111

--> CMD - curl http://192.168.49.2:31111  ----> WILL GET HTML OUTPUT.

NOTE: NodePort service is only accessible from the EC2 instance. 
To access it externally (your local browser):

1. Use SSH port forwarding:
   ssh -i your-key.pem -L 31111:<minikube-ip>:31111 ec2-user@<EC2-public-IP>
   Then open http://localhost:31111
