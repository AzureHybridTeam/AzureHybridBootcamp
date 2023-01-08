# Recommended trainings for Azure Stack HCI

> [Azure Stack HCI foundations - Learning path](https://learn.microsoft.com/en-us/training/paths/azure-stack-hci-foundations/)
>
> [Plan for and deploy SDN infrastructure on Azure Stack HCI - Learning path](https://learn.microsoft.com/en-us/training/modules/plan-deploy-sdn-infrastructure/) 
> 
> [Azure Stack HCI Workshop Teams](https://teams.microsoft.com/l/team/19%3ae28fa46102514210b4ebbdebd7ee91f6%40thread.skype/conversations?groupId=038d32e9-8df7-4547-a7ad-af80c0818f08&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47
)


# Day 1 - Lab (Optional)

Due to complexity of the lab environment this module provided as an optional. Azure Stack HCI requires hardware to understand all moving parts however the following instructions utilizes nested Azure Stack HCI servers running on top of Azure VM.

## Deploy required infrastructure for Azure Stack HCI

### Lab pre-requisites

>
> Note: **Use Cloud Shell Bash for the deployment**

Make sure you have configured **main.parameters.json** with the following settings described on the following lab guide

> deployBastion: false
>
> registerCluster: false
>
> deployAKSHCI: false
>
> deployResourceBridge: *false

**main.parameters.json** located under /azure_arc/azure_jumpstart_hcibox/bicep
>
> cd /azure_arc/azure_jumpstart_hcibox/bicep

### Lab guide

[Deploy Azure Arc Jumpstart HCIBOX](https://azurearcjumpstart.io/azure_jumpstart_hcibox)

*Note that deployment takes about 2-3 hours to finalize.*
This ARM template prepares the lab infrastructure to help you to experience all the moving parts of the Azure Stack HCI.

## Register Windows Admin Center

> Windows Admin Center (WAC) comes pre-installed on the **admincenter** vm. Register WAC proceeding the lab steps.

### Lab pre-requisites

> *Due to bug on the WAC GA version that was published back in Nov 2022*
>  
> Run the following PowerShell on both Azure Stack HCI nodes to install required PowerShell module for registration.

```powershell 
#Install Az.StackHCI module on both nodes
Get-Module Az.StackHCI -ListAvailableValidate
#Validate module installation 
Get-Module Az.StackHCI -ListAvailable
 
#Install module
Install-Module Az.StackHCI -Force
 
#Validate module installation
Get-Module Az.StackHCI -ListAvailable
```

### Lab guide

[Registering Windows Admin Center](https://learn.microsoft.com/en-us/azure-stack/hci/manage/register-windows-admin-center)

## Azure Stack HCI deployment (optional)

### Lab pre-requisites

> Note that HCIBOX comes with Azure Stack HCI cluster already deployed. If you would like to experience Azure Stack HCI cluster creation run the following commands to remove cluster.

```powershell
Get-VMSwitch -ComputerName (Get-ClusterNode).name | Remove-VMSwitch -Force

Update-StorageProviderCache
Get-StoragePool | Where-Object IsPrimordial -eq $false | Set-StoragePool -IsReadOnly:$false -ErrorAction SilentlyContinue
Get-StoragePool | Where-Object IsPrimordial -eq $false | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$false -ErrorAction SilentlyContinue
Get-StoragePool | Where-Object IsPrimordial -eq $false | Remove-StoragePool -Confirm:$false -ErrorAction SilentlyContinue
Get-PhysicalDisk | Reset-PhysicalDisk -ErrorAction SilentlyContinue
Get-Disk | Where-Object Number -ne $null | Where-Object IsBoot -ne $true | Where-Object IsSystem -ne $true | Where-Object PartitionStyle -ne RAW | Foreach-Object {
            $_ | Set-Disk -isoffline:$false
            $_ | Set-Disk -isreadonly:$false
            $_ | Clear-Disk -RemoveData -RemoveOEM -Confirm:$false
            $_ | Set-Disk -isreadonly:$true
            $_ | Set-Disk -isoffline:$true
        }
Disable-ClusterS2D -Confirm:$false
Remove-Cluster -Force -CleanupAD -Verbose -ErrorAction SilentlyContinue
```
### Lab guide (using Windows Admin Center)

[Azure Stack HCI deployment](https://learn.microsoft.com/en-us/azure-stack/hci/deploy/operating-system)

[Create Azure Stack HCI cluster](https://learn.microsoft.com/en-us/azure-stack/hci/deploy/create-cluster)

### Lab guide (using Powershell)

[Create Azure Stack HCI cluster](https://learn.microsoft.com/en-us/azure-stack/hci/deploy/create-cluster-powershell)

[Deploy host networking with Network ATC](https://learn.microsoft.com/en-us/azure-stack/hci/deploy/network-atc?tabs=22H2)

## Register Azure Stack HCI

### Lab guide (using Windows Admin Center)

[Register Azure Stack HCI cluster with Azure](https://learn.microsoft.com/en-us/azure-stack/hci/deploy/register-with-azure#register-a-cluster-using-windows-admin-center)

### Lab guide (using Powershell)

[Register Azure Stack HCI cluster with Azure](https://learn.microsoft.com/en-us/azure-stack/hci/deploy/register-with-azure#register-a-cluster-using-powershell)


## Manage Azure Arc VMs

### Lab guide

[Set up Azure Arc VM management using WAC](https://learn.microsoft.com/en-us/azure-stack/hci/manage/deploy-arc-resource-bridge-using-wac)

[Set up Azure Arc VM management using PowerShell](https://learn.microsoft.com/en-us/azure-stack/hci/manage/deploy-arc-resource-bridge-using-command-line?tabs=for-static-ip-address-1%2Cfor-static-ip-address-2)

[Create VM images using Azure Marketplace images](https://learn.microsoft.com/en-us/azure-stack/hci/manage/virtual-machine-image-azure-marketplace?tabs=azurecli)

[Create VM images using Azure Storage account](https://learn.microsoft.com/en-us/azure-stack/hci/manage/virtual-machine-image-storage-account?tabs=azurecli)

[Create VM images using in local share](https://learn.microsoft.com/en-us/azure-stack/hci/manage/virtual-machine-image-local-share?tabs=azurecli)

[Create virtual networks](https://learn.microsoft.com/en-us/azure-stack/hci/manage/create-virtual-networks?tabs=windows-admin-center)

[Deploy Azure Azure Arc VMs](https://learn.microsoft.com/en-us/azure-stack/hci/manage/manage-virtual-machines-in-azure-portal)

## Deploy AKS hybrid

### Lab guide

[Deploy and manage AKS hybrid clusters](https://learn.microsoft.com/en-us/azure/aks/hybrid/kubernetes-walkthrough-powershell)

## AKS hybrid management

### Lab guide

[Create and manage multiple node pools](https://learn.microsoft.com/en-us/azure/aks/hybrid/use-node-pools)

[Scale AKS hybrid cluster](https://learn.microsoft.com/en-us/azure/aks/hybrid/scale-cluster)

[Use AKS Hybrid autoscaler](https://learn.microsoft.com/en-us/azure/aks/hybrid/work-with-horizontal-autoscaler)

[Use multiple load balancers in AKS hybrid](https://learn.microsoft.com/en-us/azure/aks/hybrid/multiple-load-balancers)

[Create additional workload cluster without Load balancer](https://learn.microsoft.com/en-us/azure/aks/hybrid/configure-custom-load-balancer)

[Deploy MetalLB as Load balancer](https://learn.microsoft.com/en-us/azure/aks/hybrid/deploy-metallb)

[Using ingress controller](https://learn.microsoft.com/en-us/azure/aks/hybrid/create-ingress-controller)


## AKS hybrid with Azure Arc enabled kubernetes - Onboarding

### Lab guide

[Connect worload cluster to Azure Arc in AKS hybrid](https://learn.microsoft.com/en-us/azure/aks/hybrid/connect-to-arc)

## AKS hybrid with Azure Arc enabled kubernetes

### Lab guide

[Explore Azure Arc-enabled Kubernetes cluster extensions](https://learn.microsoft.com/en-us/azure/azure-arc/kubernetes/extensions)

[Enable Azure Monitor Container Insights](https://learn.microsoft.com/en-us/azure/azure-monitor/containers/container-insights-enable-arc-enabled-clusters?toc=%2Fazure%2Fazure-arc%2Fkubernetes%2Ftoc.json&tabs=create-portal%2Cverify-portal%2Cmigrate-cli)

[Deploy applications using GitOps](https://learn.microsoft.com/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?tabs=azure-cli)

[Implement CI/CD with GitOps](https://learn.microsoft.com/en-us/azure/azure-arc/kubernetes/tutorial-gitops-flux2-ci-cd)

[Enable Azure Policy extension](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/policy-for-kubernetes?toc=%2Fazure%2Fazure-arc%2Fkubernetes%2Ftoc.json&bc=%2Fazure%2Fazure-arc%2Fkubernetes%2Fbreadcrumb%2Ftoc.json#install-azure-policy-extension-for-azure-arc-enabled-kubernetes)

[Access secrets from Azure Key Vault](https://learn.microsoft.com/en-us/azure/azure-arc/kubernetes/tutorial-akv-secrets-provider)

[Enable Microsoft Defender for Containers](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-enable?pivots=defender-for-container-arc&toc=%2Fazure%2Fazure-arc%2Fkubernetes%2Ftoc.json&bc=%2Fazure%2Fazure-arc%2Fkubernetes%2Fbreadcrumb%2Ftoc.json&tabs=aks-deploy-portal%2Ck8s-deploy-asc%2Ck8s-verify-asc%2Ck8s-remove-arc%2Caks-removeprofile-api#protect-arc-enabled-kubernetes-clusters)

## AKS hybrid with Azure Arc enabled kubernetes - Preparing for Data services

### Lab guide

[Enable Azure Arc-enabled data services](https://learn.microsoft.com/en-us/azure/aks/hybrid/deploy-arc-data-services)

[Create and manage custom locations](https://learn.microsoft.com/en-us/azure/azure-arc/kubernetes/custom-locations)

