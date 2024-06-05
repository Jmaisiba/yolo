# Kubernetes Configuration Files Overview
This file will go through the configuration files in the directory and their purpose

## Deployment Configuration Files:
These files define Deployments, which provide declarative updates to Pods and ReplicaSets.

## **Deployment Files Used:**

### **backend-deployment.yaml**
Defines the deployment resources for the backend application

### **client-deployment.yaml**
Configures deployment resources in Kubernetes for the client application
This files also contains limits on resources that the will be in use by the cluster

## Service Configuration Files:
These files define Services, which provide network access to a set of Pods in Kubernetes.

## **Service Files Used**

### **mongo-service.yaml**
This is the Kubernetes Service for MongoDB used to allow other components within the cluster to access MongoDB pods via a stable network endpoint.

### **backend-service.yaml**
Kubernetes Service for the backend application providing a stable network endpoint for other components within the cluster to access the backend.
It decalare connection of type loadbalancer giving it external IP for ingress actions

### **client-service.yaml**
Service configuration file for the client application allowing other components within the cluster to access the client via a stable network endpoint.
It also declares type of connection as loadbalancer givimg it an external address

## StatefulSet Configuration Files:
These files define StatefulSets, which are used to manage stateful applications and maintain 

## **Statefulset Configuration Files Used:**

### **mongo-statefulset.yaml**
Configures a StatefulSet in Kubernetes to manage MongoDB pods. 
StatefulSets are used for deploying and managing stateful applications, ensuring stable, unique network identities, and stable storage.

## PersistentVolume (PV) Configuration Files:
These files define PersistentVolumes, which are storage resources provisioned in the cluster.

## **PersistentVolume Configuration Files Used**

### **yolo-pv.yaml**
This configuration file define the PersistentVolume (PV) in our application.
This is a piece of storage provisioned to exist beyond the lifecycle of a pod for persistence of data.

## PersistentVolumeClaim (PVC) Configuration Files:
These files define PersistentVolumeClaims, which are requests for storage by a user.

## **PersistentVolumeClaim Configuration Files Used**

### **yolo-pvc.yaml**
This configuration file define the PersistentVolumeClaim (PVC) in our application.
A PersistentVolumeClaim (PVC) is a request for storage by a user/service.
PVCs consume PV resources and provide a way to use persistent storage without requiring an understanding of the underlying storage infrastructure.


## ConfigMap Configuration Files:
These files define ConfigMaps, which are used to decouple configuration artifacts from image content.

## **ConfigMap Configuration Files Used**

### **mongo-config.yaml**
Configures ConfigMaps in Kubernetes for mongodb which allow you to decouple configuration artifacts from image content to keep containerized applications portable.

## Secret Configuration Files:
These files define Secrets, which securely store sensitive information like passwords and tokens.

## **Secret Configuration Files Used**

### **mongo-secret.yaml**
Specifies admin credentials for mongodb database access which are securely stored as it is sensitive information used by Pods in the cluster.



