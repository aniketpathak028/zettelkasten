---
title: K8s interview questions
draft: false
tags:
  - k8s
  - interview-qns
date: 2026-03-25
description: most frequently asked K8s interview qns
---
# K8s interview Qns

1. What is the difference between docker and kubernetes?
	Ans: Docker is a container platform whereas K8s is a container orchestration platform that offers capabilities like Auto healing, Auto scaling, Clustering, and Enterprise level support like Load Balancing.

2. What are the main components of K8s?
	Ans: 
	- Control plane - api-server (kubectl), CCM (cloud controller manager), controller manager, scheduler, etcd
	- Data plane - kubeproxy, container-runtime, kubelet 

3. What is the main difference between Docker swarm and Kubernetes?
	Ans: K8s is better suited for large organizations as it offers more scalability, n/w capabilities like policies and huge 3rd party support like CNCF etc while Docker swarm is very lightweight easy to use and can be used for simple applications.

4. What is the difference between container and a K8s pod?
	Ans: A container is the smallest unit of docker which can be created using a docker cli and it is an isolated virtual system with minimal requirements that can run an application. While a K8s pod is the smallest unit in K8s that can be created using a YAML manifest and a pod can have 1 or more containers and they can communicate with each other as they are in the same network!  

5. What is a namespace in K8s?
	Ans: In k8s a namespace is a logical isolation of resources, network policies, rbac, and everything. For example there are 2 projects using the same K8s cluster. One project can use ns1 and other project can use ns2 without any overlap and authentication problems.

6. What is the role of kube-proxy?
	Ans: kube-proxy works by maintaining a set of network rules on each node in the cluster, which are updated dynamically as services are added or removed. When a client sends a request to a service, the request is intercepted by kube-proxy on the node where it was recieved. Kube-proxy then looks up the destination endpoint for the service and routes the request accordingly.

7. What are the 3 major services in K8s?
	Ans: There are 3 major services in K8s:
	- ClusterIp mode - service can be accessible only inside k8s cluster
	- NodePort mode - services can be accessible only by people who can access the node ie. nodeip:port
	- LoadBalancer mode - services can be accessed publicly over the internet over a publicly exposed ip address!

8. What is the difference between NodePort and LoadBalancer type service?
	Ans: When a service is created as a Nodeport type, the Kubeproxy updates the IPTables with NodeIP address and port that is chosen in the service configuration to access the pods.

    Where as if you create a Service as type LoadBalancer, the cloud control manager creates a external load balancer IP using the underlying cloud provider logic in the C-CM. Users can access services using the external IP

9. What is the role of Kubelet?
	Ans: Kubelet manages the containers that are scheduled to run on that node. It ensures that the containers are running and healthy, and that the resources they need are available.
	 
	Kubelet communicates with the Kubernetes API server to get information about the containers that should be running on the node, and then starts and stops the containers as needed to maintain the desired state. It also monitors the containers to ensure that they are running correctly, and restarts them if necessary!

## Links:

202603251544
