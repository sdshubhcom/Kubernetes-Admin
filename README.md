# k8s-admin-training

#1st day session :

1. How Deployments were happening before kubernetes.
2. why we need kubernetes what is the actual need of that.
3. what is kubernets in a nutshell (definition).
4. Architecture of Kubernets.
5. Explanation of each componenets and its workflow.
6. what is pod.
7. installation of Kubernets.
https://github.com/cloudnloud/Kubernetes_Admin_Training/blob/main/class3-k8s-installation/installation.txt

2nd day session : 

1. Creation of Namspace and pods

1. create name space

kubectl create ns <namespace name>

kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/namespace/namespace.yaml

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/namespace/namespace.yaml

2. create pods...

kubectl create ns twitter
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/1-singlepod.yml

kubectl apply -f 1-singlepod.yml
kubectl get all -n twitter -l app=nginx
kubectl get all -n twitter -l version=v1

kubectl exec -it pod/webserver bash -n twitter

now you need to understand that lablels will help you to create exact report and find the particular resources

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/1-singlepod.yml
  
  
1.2 Multipod.

kubectl create ns facebook
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/2-multipods.yml

kubectl get all -n facebook -l app=httpd


kubectl describe pod/multicontainer-pods -n facebook


kubectl exec -it pod/multicontainer-pods bash -n facebook

kubectl exec -it pod/multicontainer-pods bash -n facebook -c web
kubectl exec -it pod/multicontainer-pods bash -n facebook -c db

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/2-multipods.yml

2. Service: loadbalancer and Nodeport. (Ongoing)

Nodeport

kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class6-service/service/nodeport-facebook.yaml

kubectl describe pod/webserver -n facebook

kubectl get all -n facebook -o wide

now access master,node1,node2 public ip and check from outside browser

<Master Node Public IP>:32001
<Worker Node1 Public IP>:32001
<Worker Node2 Public IP>:32001

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class6-service/service/nodeport-facebook.yaml
  
Loadbalancer
  
For this load balancer exercise

Goto Google cloud and create Google Kubernete Cluster Engine

gcloud container clusters get-credentials cluster-1 --zone us-central1-c --project model-axe-311317

kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class6-service/service/loadbalancer-facebook.yaml
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class6-service/service/loadbalancer-twitter.yml

kubectl get all -n twitter -o wide
kubectl get pod,services -n twitter -o wide

35.227.119.203:32001

access like above from all node machine ip addresses.it should work from all client machine ip address.then the proxy cluster is working good.

kubectl get services
kubectl describe services


3. Replicaset (Pending).
  
Replica set

kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class8-replicaset/replicaset/1-singlereplica.yml

kubectl get all -n twitter

kubectl describe replicas -n twitter

kubectl get pod,service,replicaset -n twitter -o wide

labels --> service -- selector , replica -- match ---> should be same

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class8-replicaset/replicaset/1-singlereplica.yml
  
MULTIREPLICA

kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class8-replicaset/replicaset/3-multireplica.yaml

kubectl get all -n facebook
kubectl describe replicas -n facebook

kubectl get pod,service,replicaset -n facebook -o wide

labels --> service -- selector , replica -- match ---> should be same

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class8-replicaset/replicaset/3-multireplica.yaml
