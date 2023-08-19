# Transactions Monitor (Front-end)
The application is built for an e-banking system, where users can check their transactions information by any given date.


## Run with Docker
_Prerequisite: [Docker](https://www.docker.com/get-started/)_

- Clone the project
- Open **Docker** and then `docker compose up`
- Go to [localhost:3000](http://localhost:3000) and enjoiy :)


## Run with Kubernetes (Pod Autoscaling)
_Prerequisite: [Docker](https://www.docker.com/get-started/), [minikube](https://minikube.sigs.k8s.io/docs/start/)_

- Clone the project
- Open **Docker** and then start the minikube cluster with `minikube start`
- Apply the `transaction-frontend.yaml` and 'ingress.yaml' files by `kubectl apply -f transaction-frontend.yaml -f ingress.yaml`
- Get your minikube ip by entering `minikube ip` and copy the ip address
- `sudo vim /etc/host` and set the host name by adding `[MINIKUBE_IP] transaction.com` 
- Go to [transaction.com](http://transaction.com) and enjoiy :)
