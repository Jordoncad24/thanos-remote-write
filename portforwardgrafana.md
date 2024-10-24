To port forward in GitHub Codespaces while setting up Grafana using Minikube, you'll need to follow an additional step for exposing ports properly. Here's how you can incorporate port forwarding into your setup:

### Add a Step for Port Forwarding

When running Minikube in GitHub Codespaces, you won’t be able to access the NodePort services directly from your local machine. Instead, you can use `kubectl port-forward` to forward traffic from your GitHub Codespace to your local machine.

### Adjusted Steps for Port Forwarding:

1. **Start Minikube** (same as before):
    ```sh
    minikube start --driver=docker
    ```

2. **Add Helm Repositories** (same as before):
    ```sh
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo add grafana https://grafana.github.io/helm-charts
    helm repo update
    ```

3. **Install Prometheus** (same as before):
    ```sh
    helm install prometheus prometheus-community/prometheus
    ```

4. **Install Grafana** (same as before):
    ```sh
    helm install grafana grafana/grafana
    ```

5. **Port Forward Grafana to Your Local Machine**:
   Run the following command to forward port 3000 (Grafana’s default port) to your local machine:
   
   ```sh
   kubectl port-forward service/grafana 3000:80
   ```

   This command forwards traffic from the Codespace (port `3000`) to Grafana running in Minikube (port `80` inside the cluster).

6. **Port Forward Prometheus (Optional)**:
   If you also want to access Prometheus via port forwarding, use this command:

   ```sh
   kubectl port-forward service/prometheus-server 9090:9090
   ```

   This forwards port `9090` (Prometheus’s default port) from the Codespace to your local machine.

7. **Access Grafana from Your Local Browser**:
   - Once the port forwarding is set up, open your browser and go to `http://localhost:3000`.
   - Retrieve the Grafana admin password:
     ```sh
     kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
     ```
   - Log in using the username `admin` and the password from the command above.

8. **Configure Prometheus as a Data Source** (same as before):
   - In Grafana, go to **Configuration** > **Data Sources**.
   - Add a **Prometheus** data source and set the URL to `http://localhost:9090` (if you set up port forwarding for Prometheus).
   - Click **Save & Test**.

9. **Import a Pre-built Dashboard** (same as before):
   - Go to **Create** > **Import**.
   - Use dashboard ID `6417` to import a Kubernetes monitoring dashboard.

---

### Conclusion
By adding the `kubectl port-forward` commands, you can successfully access Grafana and Prometheus via your local browser, even when running Minikube inside GitHub Codespaces. This setup will allow you to visualize and monitor Kubernetes metrics seamlessly.