# GCP-Kubernets-Example-dashboard
##### Step 1 

Visit: For the detailed guide on K8s Dashboard guide

``https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/``

##### Step 2 

Apply the following command on your GCP - GKE Cluster for the dashboard deployment
``
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
``

##### Step 3 

``
cat <<EOF | kubectl create -f -
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
EOF
``

##### Step 4 
Create ClusterRoleBinding with the user which we have created in the Step 2
``
cat <<EOF | kubectl create -f -
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
EOF
``

##### Step 5 

Proceed with the following command: Now we need to start the kubectl proxy server

``
kubectl proxy
``
##### Step 6 
Generate secret token for accessing dashaboard
Use the following command to generate secret token because we need this token to access the dashboard

``
kubectl proxy
``

##### Step 7 
Generate secret token for accessing dashaboard
Use the following command to generate secret token because we need this token to access the dashboard

``
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
``

##### Step 8 

Access the dashboard
Since you are working on Google Cloud url will be little different for you.

To get the URL first you need to click on the Web Preview option inside the Google Cloud console
