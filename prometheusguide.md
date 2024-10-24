Setting Up Prometheus in Minikube
Prerequisites
Minikube installed and running.
kubectl installed and configured to communicate with your Minikube cluster.
Helm installed for managing Kubernetes applications.
Steps to Set Up Prometheus
1. Start Minikube
First, ensure your Minikube cluster is running:

sh
Copy code
minikube start --driver=docker
2. Add Helm Repositories
Add the Prometheus community Helm chart repository:

sh
Copy code
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
3. Install Prometheus
Install Prometheus using Helm:

sh
Copy code
helm install prometheus prometheus-community/prometheus
This command will deploy Prometheus with default configurations.

4. Expose Prometheus
To access Prometheus from outside the cluster, you can expose it using a NodePort service:

sh
Copy code
kubectl expose service prometheus-server --type=NodePort --target-port=80 --name=prometheus-server-np
You can also access Prometheus directly using the ClusterIP service, but for external access, NodePort is preferred.

5. Get Prometheus NodePort
To find the NodePort assigned to Prometheus, run:

sh
Copy code
kubectl get svc
Look for the prometheus-server-np entry, which will show you the port assigned (e.g., 80:30287/TCP means you can access it via port 30287).

6. Access Prometheus
To access the Prometheus web interface:

First, get the Minikube IP:
sh
Copy code
minikube ip
Then, open your browser and navigate to:
php
Copy code
http://<minikube-ip>:<nodeport>
Replace <nodeport> with the port you found in the previous step (e.g., 30287).

7. Verify Prometheus is Running
You can check the status of the Prometheus pod to ensure it's running:

sh
Copy code
kubectl get pods -n default
You should see a pod with a name like prometheus-server-* in a Running state.

8. (Optional) Configure Persistent Storage
If you want to configure persistent storage for Prometheus (to retain data across restarts), you can customize the Helm installation by using a values.yaml file or by setting parameters directly in the Helm command. This is more advanced and optional, depending on your needs.

Recap
Start Minikube.
Add Helm repositories for Prometheus.
Install Prometheus using Helm.
Expose Prometheus as a NodePort service.
Get the NodePort assigned to the service.
Access Prometheus using Minikube's IP and NodePort.
Verify that Prometheus is running correctly.