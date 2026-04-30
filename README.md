# monitoring-and-logging-stack

Deploy monitoring stack with host and node fix mount with local storage class

Step 1 Create directory and fix permissions on the worker node
sudo mkdir -p /home/addverb/prometheus-data
sudo chown -R 1000:1000 /home/addverb/prometheus-data

Step 2  Apply PV and PVC
kubectl apply -f prometheus-storage.yaml
prometheus-storage.yaml creates a PV backed by the local hostPath and a PVC with matching name that Prometheus operator expects.
 
Step 3 Verify PV is Bound
kubectl get pv && kubectl get pvc -n monitoring
PV status must show Bound before proceeding.
 
Step 4 Install Prometheus via Helm**
helm upgrade --install prometheus prometheus-community/kube-prometheus-stack -n monitoring --create-namespace -f promethesus.yaml
