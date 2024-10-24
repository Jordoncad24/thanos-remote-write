👍  Starting "minikube" primary control-plane node in "minikube" cluster
🏃  Updating the running qemu2 "minikube" VM ...
❗  Due to DNS issues your cluster may have problems starting and you may not be able to pull images
More details available at: https://minikube.sigs.k8s.io/docs/drivers/qemu/#known-issues
❗  Failing to connect to https://registry.k8s.io/ from both inside the minikube VM and host machine
💡  To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
🐳  Preparing Kubernetes v1.31.0 on Docker 27.2.0 ...
🤦  Unable to restart control-plane node(s), will reset cluster: <no value>
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
❗  Enabling 'default-storageclass' returned an error: running callbacks: [Error making standard the default storage class: Error listing StorageClasses: Get "https://10.0.2.15:8443/apis/storage.k8s.io/v1/storageclasses": dial tcp 10.0.2.15:8443: i/o timeout]
🌟  Enabled addons: storage-provisioner

❌  Exiting due to GUEST_START: failed to start node: wait 6m0s for node: wait for healthy API server: apiserver healthz never reported healthy: context deadline exceeded

╭───────────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                           │
│    😿  If the above advice does not help, please let us know:                             │
│    👉  https://github.com/kubernetes/minikube/issues/new/choose                           │
│                                                                                           │
│    Please run `minikube logs --file=logs.txt` and attach logs.txt to the GitHub issue.    │
│                                                                                           │
╰───────────────────────────────────────────────────────────────────────────────────────────╯

jordoncadore@Jordons-MacBook-Pro Documents % 
jordoncadore@Jordons-MacBook-Pro Documents % minikube status

minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Stopped
kubeconfig: Configured

jordoncadore@Jordons-MacBook-Pro Documents % minikube start 
------------------------

It looks like you're encountering issues with the Minikube API server not starting. Here are some steps you can try to resolve this:

1. **Check DNS Configuration**:
   - Ensure your DNS settings are correctly configured. You can follow the guidance provided [here](https://minikube.sigs.k8s.io/docs/drivers/docker/).

2. **Configure a Proxy**:
   - If you're behind a proxy, configure it as suggested here.

3. **Clear Minikube Configurations**:
   - Sometimes, clearing the Minikube configurations and starting fresh can help:
     ```sh
     minikube delete --all --purge
     minikube start
     ```

4. **Check Kubelet Status**:
   - Verify the status of the kubelet service:
     ```sh
     systemctl status kubelet
     journalctl -xeu kubelet
     ```

5. **Increase Memory Allocation**:
   - Try increasing the memory allocated to Minikube:
     ```sh
     minikube start --memory=4096
     ```

6. **Switch Drivers**:
   - If you're using Docker, try switching to another driver like VirtualBox:
     ```sh
     minikube start --driver=virtualbox
     ```

7. **Update Context**:
   - Sometimes updating the Minikube context can resolve issues:
     ```sh
     minikube update-context
     ```

If these steps don't resolve the issue, you might want to check the detailed logs by running:
```sh
minikube logs --file=logs.txt
```
and then attach the logs to a new issue on the [Minikube GitHub page](https://github.com/kubernetes/minikube/issues/14540).

Let me know if you need further assistance!

Source: Conversation with Copilot, 24/10/2024
(1) minikube status says apiserver:stopped #14540 - GitHub. https://github.com/kubernetes/minikube/issues/14540.
(2) API server is not started !! · Issue #14067 · kubernetes/minikube. https://github.com/kubernetes/minikube/issues/14067.
(3) apiServer not starting · Issue #14863 · kubernetes/minikube. https://github.com/kubernetes/minikube/issues/14863.
(4) undefined. https://askubuntu.com/questions/935569/how-to-completely-uninstall-docker.
(5) undefined. https://linuxhint.com/install-minikube-ubuntu/.
(6) undefined. https://minikube.sigs.k8s.io/docs/drivers/virtualbox/.
(7) undefined. https://minikube.sigs.k8s.io/docs/drivers/docker/.
(8) undefined. https://minikube.sigs.k8s.io/docs/drivers/virtualbox/%29.
(9) undefined. https://192.168.49.2:8443/apis/storage.k8s.io/v1/storageclasses.
(10) undefined. https://github.com/kubernetes/minikube/releases/tag/v1.25.2.
(11) undefined. https://192.168.58.2:8443/apis/storage.k8s.io/v1/storageclasses.

i have brave and vpn related things installed.
