### Kubernetes (10 Questions)

1. **What is the architecture of a Kubernetes cluster?**
   - **Answer**: A Kubernetes cluster consists of a control plane (master) and worker nodes. The control plane includes the API server (handles requests), etcd (stores cluster state), scheduler (assigns pods), and controller manager (manages replication). Worker nodes run kubelet (manages pods), kube-proxy (networking), and container runtime (e.g., containerd). Example: Deploy a cluster with `kubeadm init` to set up control plane components.
   - **DevOps Context**: Ensures scalability and fault tolerance in production.

2. **How do you deploy a stateless application in Kubernetes?**
   - **Answer**: Use a Deployment resource with a defined replica count, container image, and Service for load balancing. Example:
     ```yaml
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: my-app
     spec:
       replicas: 3
       selector:
         matchLabels:
           app: my-app
       template:
         metadata:
           labels:
             app: my-app
         spec:
           containers:
           - name: my-app
             image: my-app:1.0
             ports:
             - containerPort: 8080
     ---
     apiVersion: v1
     kind: Service
     metadata:
       name: my-app-svc
     spec:
       selector:
         app: my-app
       ports:
       - port: 80
         targetPort: 8080
       type: ClusterIP
     ```
     Apply with `kubectl apply -f deployment.yaml`. Use CI/CD to automate (e.g., GitHub Actions with `kubectl`).
   - **DevOps Context**: Enables scalable, automated deployments.

3. **How do you troubleshoot a pod stuck in `Pending` state?**
   - **Answer**: Use `kubectl describe pod` to check events (e.g., insufficient CPU, no nodes available). Verify resource requests/limits, node affinity, and taints/tolerations. Example:
     ```bash
     kubectl describe pod my-pod
     kubectl get nodes
     ```
     Fix by adjusting resources or scaling the cluster with `kubectl scale`.
   - **DevOps Context**: Critical for maintaining application uptime.

4. **What is an Ingress resource, and how do you configure it?**
   - **Answer**: Ingress exposes HTTP/HTTPS services via a single external endpoint, routing based on host/path. Example:
     ```yaml
     apiVersion: networking.k8s.io/v1
     kind: Ingress
     metadata:
       name: my-ingress
       annotations:
         nginx.ingress.kubernetes.io/rewrite-target: /
     spec:
       rules:
       - host: app.example.com
         http:
           paths:
           - path: /
             pathType: Prefix
             backend:
               service:
                 name: my-app-svc
                 port:
                   number: 80
     ```
     Deploy an Ingress controller (e.g., NGINX) first. Apply with `kubectl apply -f ingress.yaml`.
   - **DevOps Context**: Simplifies external access in production.

5. **How do you implement RBAC in Kubernetes?**
   - **Answer**: Define Roles/ClusterRoles for permissions and bind them to users/ServiceAccounts via RoleBindings/ClusterRoleBindings. Example:
     ```yaml
     apiVersion: rbac.authorization.k8s.io/v1
     kind: Role
     metadata:
       namespace: dev
       name: pod-reader
     rules:
     - apiGroups: [""]
       resources: ["pods"]
       verbs: ["get", "list"]
     ---
     apiVersion: rbac.authorization.k8s.io/v1
     kind: RoleBinding
     metadata:
       namespace: dev
       name: pod-reader-binding
     subjects:
     - kind: User
       name: dev-user
       apiGroup: rbac.authorization.k8s.io
     roleRef:
       kind: Role
       name: pod-reader
       apiGroup: rbac.authorization.k8s.io
     ```
     Apply with `kubectl apply -f rbac.yaml`. Test with `kubectl auth can-i`.
   - **DevOps Context**: Secures multi-tenant clusters.

6. **What is a Horizontal Pod Autoscaler (HPA), and how do you configure it?**
   - **Answer**: HPA scales pods based on metrics like CPU/memory. Example:
     ```yaml
     apiVersion: autoscaling/v2
     kind: HorizontalPodAutoscaler
     metadata:
       name: my-app-hpa
     spec:
       scaleTargetRef:
         apiVersion: apps/v1
         kind: Deployment
         name: my-app
       minReplicas: 2
       maxReplicas: 10
       metrics:
       - type: Resource
         resource:
           name: cpu
           target:
             type: Utilization
             averageUtilization: 70
     ```
     Apply with `kubectl apply -f hpa.yaml`. Requires Metrics Server.
   - **DevOps Context**: Ensures resource efficiency and scalability.

7. **How do you manage secrets in Kubernetes?**
   - **Answer**: Use Secret resources to store sensitive data (e.g., passwords, API keys). Example:
     ```yaml
     apiVersion: v1
     kind: Secret
     metadata:
       name: my-secret
     type: Opaque
     data:
       password: cGFzc3dvcmQ=  # base64-encoded
     ---
     apiVersion: v1
     kind: Pod
     metadata:
       name: my-pod
     spec:
       containers:
       - name: my-app
         image: my-app:1.0
         env:
         - name: MY_PASSWORD
           valueFrom:
             secretKeyRef:
               name: my-secret
               key: password
     ```
     Create with `kubectl apply -f secret.yaml`. Use Helm Secrets or external vaults (e.g., HashiCorp Vault) for production.
   - **DevOps Context**: Enhances security in CI/CD pipelines.

8. **What are PersistentVolumes (PV) and PersistentVolumeClaims (PVC)?**
   - **Answer**: PVs are cluster-wide storage resources, and PVCs are requests for storage by pods. Example:
     ```yaml
     apiVersion: v1
     kind: PersistentVolume
     metadata:
       name: my-pv
     spec:
       capacity:
         storage: 10Gi
       accessModes:
         - ReadWriteOnce
       hostPath:
         path: /mnt/data
     ---
     apiVersion: v1
     kind: PersistentVolumeClaim
     metadata:
       name: my-pvc
     spec:
       accessModes:
         - ReadWriteOnce
       resources:
         requests:
           storage: 10Gi
     ---
     apiVersion: v1
     kind: Pod
     metadata:
       name: my-pod
     spec:
       containers:
       - name: my-app
         image: nginx
         volumeMounts:
         - mountPath: /data
           name: storage
       volumes:
       - name: storage
         persistentVolumeClaim:
           claimName: my-pvc
     ```
     Apply with `kubectl apply -f storage.yaml`.
   - **DevOps Context**: Critical for stateful applications.

9. **How do you monitor a Kubernetes cluster?**
   - **Answer**: Use Prometheus for metrics, Grafana for visualization, and kube-state-metrics for cluster state. Example:
     ```bash
     helm install prometheus prometheus-community/kube-prometheus-stack
     ```
     Configure alerts for pod crashes or high CPU. Use `kubectl top` for quick checks.
   - **DevOps Context**: Ensures observability in production.

10. **How do you perform a rolling update in Kubernetes?**
    - **Answer**: Configure a Deployment with `RollingUpdate` strategy. Example:
      ```yaml
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: my-app
      spec:
        strategy:
          type: RollingUpdate
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 0
        replicas: 3
        selector:
          matchLabels:
            app: my-app
        template:
          metadata:
            labels:
              app: my-app
          spec:
            containers:
            - name: my-app
              image: my-app:2.0
      ```
      Update with `kubectl apply -f deployment.yaml` and monitor with `kubectl rollout status`.
    - **DevOps Context**: Enables zero-downtime deployments in CI/CD.


    