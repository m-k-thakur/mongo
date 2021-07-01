# mongo
eksctl create cluster -f ekscluster.yml
# Scaling nodegroup
eksctl scale nodegroup --cluster=mktcluster --nodes=3 --name=ng-1 --nodes-min=2 --nodes-max=4 kubectl get nodes

#Install Kubernetes Dashboard.

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml

kubectl -n kubernetes-dashboard edit svc kubernetes-dashboard
# Find the service type and change from ClusterIP to LoadBalancer.
kubectl -n kubernetes-dashboard get svc
**#get Login Credentials to access Kubernetes Dashboard.**
kubectl create serviceaccount dashboard -n default

kubectl create clusterrolebinding dashboard-admin -n default  --clusterrole=cluster-admin  --serviceaccount=default:dashboard

kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode
