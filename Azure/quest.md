### Azure (10 Questions)

1. **What is Azure Kubernetes Service (AKS), and how do you deploy it?**
   - **Answer**: AKS is a managed Kubernetes service. Deploy with:
     ```bash
     az aks create --resource-group myRG --name myAKSCluster --node-count 2
     az aks get-credentials --resource-group myRG --name myAKSCluster
     ```
     Apply manifests with `kubectl apply`.
   - **DevOps Context**: Simplifies Kubernetes management.

2. **How do you set up a CI/CD pipeline in Azure DevOps?**
   - **Answer**: Create a pipeline with build, test, and deploy stages. Example:
     ```yaml
     trigger:
       branches:
         include: [ main ]
     pool:
       vmImage: 'ubuntu-latest'
     steps:
     - task: Docker@2
       inputs:
         command: 'buildAndPush'
         repository: '$(acrName).azurecr.io/myapp'
         tags: '$(Build.BuildId)'
     - task: Kubernetes@1
       inputs:
         connectionType: 'Azure Resource Manager'
         azureSubscription: 'mySubscription'
         azureResourceGroup: 'myRG'
         kubernetesCluster: 'myAKSCluster'
         command: 'apply'
         arguments: '-f k8s/deployment.yaml'
     ```
   - **DevOps Context**: Automates deployments to AKS.

3. **How do you secure an AKS cluster?**
   - **Answer**: Enable Azure AD integration, RBAC, and Network Policies. Example:
     ```bash
     az aks update --resource-group myRG --name myAKSCluster --enable-aad --enable-azure-rbac
     ```
     Use private clusters and Azure Defender.
   - **DevOps Context**: Ensures production security.

4. **What is Azure Container Registry (ACR), and how do you use it?**
   - **Answer**: ACR stores Docker images. Push images with:
     ```bash
     az acr login --name myacr
     docker tag my-app myacr.azurecr.io/my-app:1.0
     docker push myacr.azurecr.io/my-app:1.0
     ```
     Integrate with AKS for deployments.
   - **DevOps Context**: Centralizes image storage.

5. **How do you monitor Azure applications?**
   - **Answer**: Use Azure Monitor, Application Insights, and Log Analytics. Example:
     ```bash
     az monitor log-analytics workspace create --resource-group myRG --workspace-name myWorkspace
     ```
     Set alerts for metrics like CPU usage.
   - **DevOps Context**: Ensures observability.

6. **How do you manage Azure resources with Terraform?**
   - **Answer**: Define resources in Terraform and apply. Example:
     ```hcl
     provider "azurerm" {
       features {}
     }
     resource "azurerm_resource_group" "example" {
       name     = "myRG"
       location = "East US"
     }
     resource "azurerm_kubernetes_cluster" "example" {
       name                = "myAKSCluster"
       location            = azurerm_resource_group.example.location
       resource_group_name = azurerm_resource_group.example.name
       dns_prefix          = "myaks"
       default_node_pool {
         name       = "default"
         node_count = 2
         vm_size    = "Standard_D2_v2"
       }
       identity {
         type = "SystemAssigned"
       }
     }
     ```
     Run `terraform apply`.
   - **DevOps Context**: Enables IaC.

7. **What is Azure Key Vault, and how do you use it?**
   - **Answer**: Key Vault stores secrets securely. Example:
     ```bash
     az keyvault secret set --vault-name myVault --name mySecret --value mypassword
     ```
     Access in apps via SDK or environment variables.
   - **DevOps Context**: Secures credentials in pipelines.

8. **How do you configure networking in Azure for AKS?**
   - **Answer**: Use VNets and Network Security Groups (NSGs). Example:
     ```bash
     az network vnet create --resource-group myRG --name myVNet --address-prefix 10.0.0.0/16
     az aks create --resource-group myRG --name myAKSCluster --vnet-subnet-id /subscriptions/.../subnets/mySubnet
     ```
     Apply NSGs to restrict traffic.
   - **DevOps Context**: Enhances cluster security.

9. **How do you implement blue-green deployments in AKS?**
   - **Answer**: Deploy two environments (blue, green) and switch traffic via Service or Ingress. Example:
     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: my-app-svc
     spec:
       selector:
         app: my-app
         version: green  # Switch to blue for rollout
       ports:
       - port: 80
         targetPort: 8080
     ```
     Update selector with `kubectl apply`.
   - **DevOps Context**: Ensures zero-downtime deployments.

10. **How do you handle disaster recovery in Azure?**
    - **Answer**: Use Azure Site Recovery for VMs and geo-replicated backups. For AKS, replicate clusters across regions. Example:
      ```bash
      az backup vault create --resource-group myRG --name myVault
      ```
      Configure multi-region AKS with `az aks create`.
    - **DevOps Context**: Ensures business continuity.
