---
title: Untitled
draft: false
tags:
date:
description:
---
# configmaps and secrets

> As per K8s docs - A ConfigMap is an API object used to store non-confidential data in key-value pairs.

### why is configmap needed?

- In most applications we always need to store some sort of data for the application to run for example, if the application uses the database, it might need a database connection path and a port number!
- storing these data inside the application code is non an efficient solution as if any of these change in the future, we might need to manually change them in every container inside the pod.
- Usually it is preferred to store these kinds of information in an env file which can then be accessed by the file system. However k8s offers a better solution to tackle this problem by allowing a resource like configmap.
- A configmap is a resource that can be used to store such non-confidential data in a k8s cluster inside etcd and can be mounted to pods, and can be used by applications directly!

![[Pasted image 20260328191910.png]]

### creating and using a configmap

#### 1. as env variables

- create a configmap resource in the cluster!

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: test-cm
data:
  DB_PORT: "3008"
```

```shell
kubectl apply -f configMap.yml
```

- add the reference to the configmap in the deployment!

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
	app: hello-world
spec:
  replicas: 1
  selector:
	  matchLabels:
	    app: hello-world
  template:
	metadata:
	 labels:
	   app: hello-world
	spec:
	  containers:
	  - name: hello-world
        imagePullPolicy: IfNotPresent
        image: aniketpathak028/flask-app:latest
	    envFrom:
        - configMapRef:
            name: test-cm
```

- once the deployment is applied you can log into any of the pods and check if the env variable is present in the pod or not!

```shell
kubectl apply -f deployment.yaml

kubectl exec -it <pod-name> -- /bin/bash

printenv | grep DB
DB_PORT=3008
```

- but the issue with this method is that if you change the port, the pods won't know it, as the env variables do not get changed when the configmap is reapplied! 
- We must destroy and re-create the pods inorder to change it!

To overcome this we should use method 2
#### 2. as volume mounts

- instead of using an env variable we could create a volume mount in the pod and have it updated everytime we update the value in the configMap!

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        imagePullPolicy: IfNotPresent
        image: aniketpathak028/flask-app:latest
        ports:
        - containerPort: 80
        envFrom:
        - configMapRef:
           name: test-cm
        volumeMounts:
         - name: foo
           mountPath: /opt
      volumes:
       - name: foo
         configMap:
          name: test-cm
```

- now a volume is mounted to every deployment, which extracts the configmap info into a path `/etc/foo`
- confirm this by logging into the pods and checking for this file

```shell
kubectl exec -t <pod-name> -- /bin/bash
cat /opt/DB_PORT
3008
```

now if you change the value in configMap, the value would be updated in the pod too!
### why is secret needed?

- The major difference between configmap and secrets is that, secrets usually contain confidential data which is stored in etcd but it is always encrypted by k8s before it is stored!
- the issue in storing confidential files as configmap is, if the cluster gets hacked, these credentials could be exposed.
- Therefore k8s always recommends to assign an RBAC to these secrets and only allow privileges to necessary people!





## Links:

202603280927
