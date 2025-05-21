### Helm Charts (10 Questions)

1. **What is a Helm chart, and why is it used?**
   - **Answer**: A Helm chart is a package of Kubernetes manifests (e.g., Deployments, Services) with templating for parameterization. It simplifies application deployment and management. Example: `helm create my-chart` generates a chart structure.
   - **DevOps Context**: Streamlines deployments in CI/CD pipelines.

2. **How do you create a custom Helm chart?**
   - **Answer**: Use `helm create` to scaffold a chart, customize `values.yaml` and `templates/`. Example:
     ```bash
     helm create my-app
     # Edit values.yaml
     ```
     ```yaml
     # values.yaml
     replicaCount: 2
     image:
       repository: nginx
       tag: "1.21"
     ```
     Deploy with `helm install my-app ./my-app`.
   - **DevOps Context**: Enables reusable configurations.

3. **How do you override values in a Helm chart?**
   - **Answer**: Use `--set` or a custom `values.yaml`. Example:
     ```bash
     helm install my-app ./my-app --set replicaCount=3
     ```
     Or:
     ```yaml
     # custom-values.yaml
     replicaCount: 3
     ```
     ```bash
     helm install my-app ./my-app -f custom-values.yaml
     ```
   - **DevOps Context**: Supports environment-specific deployments.

4. **What are Helm dependencies, and how do you manage them?**
   - **Answer**: Dependencies are subcharts included in a chart’s `charts/` directory or defined in `Chart.yaml`. Example:
     ```yaml
     # Chart.yaml
     dependencies:
     - name: redis
       version: "17.0.0"
       repository: "https://charts.bitnami.com/bitnami"
     ```
     Update with `helm dependency update`.
   - **DevOps Context**: Simplifies complex app deployments.

5. **How do you upgrade a Helm release?**
   - **Answer**: Use `helm upgrade` to apply changes. Example:
     ```bash
     helm upgrade my-app ./my-app --set image.tag=2.0
     ```
     Use `--atomic` for rollback on failure. Monitor with `helm history my-app`.
   - **DevOps Context**: Ensures smooth updates in CI/CD.

6. **How do you rollback a failed Helm release?**
   - **Answer**: Use `helm rollback` to revert to a previous revision. Example:
     ```bash
     helm rollback my-app 1
     ```
     Check revisions with `helm history my-app`.
   - **DevOps Context**: Critical for production reliability.

7. **How do you secure sensitive data in Helm charts?**
   - **Answer**: Use Helm Secrets or Kubernetes Secrets. Example:
     ```yaml
     # templates/secret.yaml
     apiVersion: v1
     kind: Secret
     metadata:
       name: {{ .Release.Name }}-secret
     type: Opaque
     data:
       password: {{ .Values.secret.password | b64enc }}
     ```
     ```yaml
     # values.yaml
     secret:
       password: mypassword
     ```
     Encrypt with `helm secrets`.
   - **DevOps Context**: Enhances security in pipelines.

8. **What is a Helm repository, and how do you set one up?**
   - **Answer**: A Helm repository stores charts (e.g., ChartMuseum, Harbor). Set up with:
     ```bash
     helm repo add my-repo https://charts.example.com
     helm repo update
     ```
     Host privately with Harbor and push charts:
     ```bash
     helm package my-app
     helm push my-app-0.1.0.tgz oci://harbor.example.com/my-repo
     ```
   - **DevOps Context**: Centralizes chart distribution.

9. **How do you debug a Helm chart deployment?**
   - **Answer**: Use `helm install --dry-run` to validate templates, check rendered manifests with `helm template`, and inspect Kubernetes events with `kubectl describe`. Example:
     ```bash
     helm install my-app ./my-app --dry-run --debug
     ```
   - **DevOps Context**: Speeds up troubleshooting.

10. **How do you version Helm charts?**
    - **Answer**: Define versions in `Chart.yaml`. Example:
      ```yaml
      # Chart.yaml
      apiVersion: v2
      name: my-app
      version: 0.2.0
      ```
      Increment versions for changes (`0.2.0` to `0.3.0`). Use semantic versioning in CI/CD pipelines.
    - **DevOps Context**: Ensures traceability and reproducibility.
