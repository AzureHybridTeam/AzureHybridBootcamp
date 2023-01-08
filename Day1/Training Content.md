# Day 1 - Content

# Table of Contents

1. [Arc-enabled Server](#ArcEnabledServer)
2. [Azure Stack HCI](#AzureStackHCI)
3. [Arc-enabled VMWare](#ArcEnabledVMWare)
4. [Arc-enabled VMM](#ArcEnabledVMM)

## Arc-enabled Server

- Pre-Requisites
- Onboarding
- Log Analytic Workspace configuration

## Azure Stack HCI

### Features

- Ws2022 Azure Edition  
- 2008 and 2012 ESU
- Stretch clustering
- Network ATC
- Hot-patching
- Single node
- Software Defeined Networking
- AKS Hybrid (Sdn support)
- Azure Arc VM
    - Image management
	      - Azure Marketplace
          - Custom vm images
    - VM deployment
    - on-prem Virtual Network management
- Kernel soft reboot
- Azure Virtual Desktop
- Storage Thin provisioning
- AKS hybrid cluster provisioning from Azure 

### Architecture

### Requirements

- Firewall requirements – Only outbound and mostly 443
- Azure AD
- Domain
- All Hardware components must be in the Azure Stack HCI Catalog
    - [Server requirements](https://learn.microsoft.com/en-us/azure-stack/hci/concepts/system-requirements#server-requirements)
    - [Storage requirements](https://learn.microsoft.com/en-us/azure-stack/hci/concepts/system-requirements#storage-requirements)
    - [Physical Network](https://learn.microsoft.com/en-us/azure-stack/hci/concepts/physical-network-requirements?tabs=22H2%2C20-21H2reqs)
    - [Network adapter](https://learn.microsoft.com/en-us/azure-stack/hci/concepts/host-network-requirements)

- Environment readiness validator - [Assess environment readiness](https://learn.microsoft.com/en-us/azure-stack/hci/manage/use-environment-checker?tabs=connectivity) 

### Deployment Process

-   WAC
-   PowerShell

### Licensing / Billing

- Hybrid benefit (AKS hybrid included)
- Windows Server Licensing
- Free Legacy product security updates (ESU)

### Appendix

- Supplemental package [Azure Stack HCI deployment overview (preview) - Azure Stack HCI | Microsoft Learn](https://learn.microsoft.com/en-us/azure-stack/hci/deploy/deployment-tool-introduction)
- Lab environment for testing (hcibox) [Azure Arc Jumpstart](https://azurearcjumpstart.io/azure_jumpstart_hcibox/)

### Roadmap

## Arc-enabled VMWare

## Arc-enabled VMM

