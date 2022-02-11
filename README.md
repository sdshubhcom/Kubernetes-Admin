# k8s-admin-training

# Before start this training,you must have the below Pre-Requisites to loud better in the kubernetes Administration

- Linux Admiistration knowledge is must
- Ansible Automation/Administration Knowledge is must
- Google cloud account should be created and activated.
- Hub.docker.com login need to be created
- github.com account need to be created

** each VM should be like below **
  
  | Purpose   | VM Name          | CPU | Memory | Disk  | Operating System |
  | -------   | ---------------- | --- | ------ | ----  | ---------------- |
  | Machine 1 | k8s master       |  2  | 4 GB   | 50 GB | Ubuntu  18.0 LTS |
  | Machine 2 | Worker node1     |  2  | 4 GB   | 50 GB | Ubuntu  18.0 LTS |
  | Machine 3 | Worker node2     |  2  | 4 GB   | 50 GB | Ubuntu  18.0 LTS |



# 1st day session :

1. How Deployments were happening before kubernetes.
2. why we need kubernetes what is the actual need of that.
3. what is kubernets in a nutshell (definition).
4. Architecture of Kubernets.
5. Explanation of each componenets and its workflow.
6. what is pod.
7. installation of Kubernets.

https://github.com/cloudnloud/Kubernetes_Admin_Training/blob/main/class3-k8s-installation/installation.txt

# 2nd day session : 

# Creation of Namspace and pods

# create name space

```
kubectl create ns cloudnloud
```

```
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/namespace/namespace.yaml
```

```
kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/namespace/namespace.yaml
```

# create pods...

```
kubectl create ns twitter
```
```
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/1-singlepod.yml
```

```
kubectl apply -f 1-singlepod.yml
```
```
kubectl get all -n twitter -l app=nginx
```
```
kubectl get all -n twitter -l version=v1
```

```
kubectl exec -it pod/webserver bash -n twitter
```

- now you need to understand that lablels will help you to create exact report and find the particular resources

```
kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/1-singlepod.yml
``` 
  
# Multipod.

```
kubectl create ns facebook

```

```
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/2-multipods.yml
```

```
kubectl get all -n facebook -l app=httpd
```

```
kubectl describe pod/multicontainer-pods -n facebook
```

```
kubectl exec -it pod/multicontainer-pods bash -n facebook
```

```
kubectl exec -it pod/multicontainer-pods bash -n facebook -c web
```

```
kubectl exec -it pod/multicontainer-pods bash -n facebook -c db
```
```
kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/2-multipods.yml
```

# Service: Nodeport. 

```
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class6-service/service/nodeport-facebook.yaml
```

```
kubectl describe pod/webserver -n facebook
```

```
kubectl get all -n facebook -o wide
```

 - now access master,node1,node2 public ip and check from outside browser

<Master Node Public IP>:32001
<Worker Node1 Public IP>:32001
<Worker Node2 Public IP>:32001

```
kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class6-service/service/nodeport-facebook.yaml
```
# ReplicaSet - Single Replicaset

```
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class8-replicaset/replicaset/1-singlereplica.yml
```
```
kubectl get all -n twitter
```
```
kubectl describe replicas -n twitter
```
``` 
kubectl get pod,service,replicaset -n twitter -o wide
```
- labels --> service -- selector , replica -- match ---> should be same

```
kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class8-replicaset/replicaset/1-singlereplica.yml
```
# ReplicaSet - Multi Replicaset

```
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class8-replicaset/replicaset/3-multireplica.yaml
```

```
kubectl get all -n facebook
```
```
kubectl describe replicas -n facebook
```
```
kubectl get pod,service,replicaset -n facebook -o wide
```
- labels --> service -- selector , replica -- match ---> should be same

```
kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class8-replicaset/replicaset/3-multireplica.yaml
```
