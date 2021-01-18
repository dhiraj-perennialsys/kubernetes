                                           Kubernetes
What is kubernetes?
 Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.
Kubernetes architecture
Node:- Kubernetes runs your workload by placing containers into Pods to run on Nodes. A node may be a virtual or physical machine, depending on the cluster. Each node contains the services necessary to run Pods, managed by the control plane. Typically you have several nodes in a cluster; in a learning or resource-limited environment, you might have just one. The components on a node include the kubelet, a container runtime, and the kube-proxy.

Master process:-
                                           1)API server

                                           2)Scheduler

                                           3)Controller manager

                                           4)etcd
1)API Server :- kube-apiserver

The Kubernetes API server validates and configures data for the api objects which include pods, services, replicationcontrollers, and others. The API Server services REST operations and provides the frontend to the cluster's shared state through which all other components interact. it is cluster gateway.which get initial request for any updtae & query. acts as a gatekeeper for authentication. validate request

2)Scheduler

The Kubernetes scheduler is a control plane process which assigns Pods to Nodes. The scheduler determines which Nodes are valid placements for each Pod in the scheduling queue according to constraints and available resources. The scheduler then ranks each valid Node and binds the Pod to a suitable Node. Multiple different schedulers may be used within a cluster; kube-scheduler is the reference implementation.

3)Controller manager

The Kubernetes controller manager is a daemon that embeds the core control loops shipped with Kubernetes. In applications of robotics and automation, a control loop is a non-terminating loop that regulates the state of the system. In Kubernetes, a controller is a control loop that watches the shared state of the cluster through the apiserver and makes changes attempting to move the current state towards the desired state.

4)etcd etcd is a consistent and highly-available key value store used as Kubernetes' backing store for all cluster data. If your Kubernetes cluster uses etcd as its backing store, make sure you have a back up plan for those data.

Minikube

Like kind, minikube is a tool that lets you run Kubernetes locally. minikube runs a single-node Kubernetes cluster on your personal computer (including Windows, macOS and Linux PCs) so that you can try out Kubernetes, or for daily development work.

How to install curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo install minikube-linux-amd64 /usr/local/bin/minikube Start your cluster #minikube start

Interact with your cluster

#kubectl get po -A

#minikube kubectl -- get po -A

#minikube dashboard Deploy applications

#kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4 #kubectl expose deployment hello-minikube --type=NodePort --port=8080

#kubectl get services hello-minikube

#minikube service hello-minikube

#kubectl port-forward service/hello-minikube 7080:8080

Manage cluster Pause Kubernetes without impacting deployed applications: #minikube pause

Halt the cluster: #minikube stop

Increase the default memory limit (requires a restart): #minikube config set memory 16384

Browse the catalog of easily installed Kubernetes services: #minikube addons list Create a second cluster running an older Kubernetes release: #minikube start -p aged --kubernetes-version=v1.16.1 Delete all of the minikube clusters: #minikube delete --all

Build a Docker image from existing Python source code and push it to Docker Hub.

cd Docker docker build -t dhiraj599/web .

docker push dhiraj/web

Launch the app with Docker Compose docker-compose up -d

Test the app curl localhost:5000

Deploy the app to Kubernetes

cd ../Kubernetes kubectl create -f db-pod.yml kubectl create -f db-svc.yml kubectl create -f web-pod.yml kubectl create -f web-svc.yml kubectl create -f web-rc.yml

Check that the Pods and Services are created

kubectl get pods kubectl get svc

Get the NodePort for the web Service. Make a note of the port. kubectl describe svc web

Test the app by accessing the NodePort of one of the nodes. kubectl get nodes curl

