### Prerequisites

1. A K8s cluster with AWS EFS CSI driver installed

2. A ready to use AWS EFS file system


### Steps

To deploy MySQL using Persistent Volume one should follow these steps to do so :

* Create Storage Class
* Create PVC (PersistentVolumeClaim) for MySQL.
* Deploy MySQL (Deployment and Service).
* Add data to MySQL.
* Simulate a node failure, and K8s automatically migrates MySQL to other nodes.

Firstly , if you want to apply all these files under any namespace then create namespace as :

```
kubectl create ns mysql
```


In order to follow above steps , one should create various files as mentioned in step section:


* storage_class.yml
* mysql-pvc.yml
* mysql-deployment.yml
* mysql-service.yaml 

Now Perform all operation in the namespace created as:

**For Storage Class Yaml File**

```
kubectl apply -f storageclass.yaml -n mysql


kubectl get storageclass -n mysql
```

**For PVC Yaml File**

```
kubectl create -f mysqlpvc.yaml -n mysql

kubectl get pvc -n mysql
```

**For Deployment Yaml File**

```
kubectl create -f mysql-deployment.yaml -n mysql

kubectl get pods -n mysql
```

If you want to check the logs of the pod then use :

```
kubectl logs "name_of_pod" -n mysql
```


**For Service Yaml File**

```
kubectl create -f mysql-service.yml -n mysql
```


**To simulate Node Failure use the following command :**

```
kubectl run -it --rm --image=mysql:5.7 --restart=Never mysql-client -- mysql -h mysql -ppassword
```


**To Verify Consistency**

```
Let's shut down all the nodes , and yes we have done.
```

