# Day 1 - Lab

Below are the lab items that are going to be covered.

- ***Applying Azure Policy to Arc Enabled Servers:***

     In this lab environment we are using [**Jumpstart ArcBox for IT Pros**](https://azurearcjumpstart.io/azure_jumpstart_arcbox/itpro) as vm environment.  
     As previously stated please make sure "Microsoft defender for Cloud" environment settings have been enabled prior to lab described [here](https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-enhanced-security). 

    Make sure all of the settings are enabled and defender uses the Log Analytics Workspace that ArcBox has created as shown in the screenshots
    [Defender Plans settings](/Day1/pics/defender1.jpg) and [Setting & Monitoring](/Day1/pics/defender2.jpg).

    Arcbox has already created some of the Policies, we'll omit these and assign our own policy settings that should be used in customer deployments.
    Please assign Initiatives/Policies listed below within **Resource Group** scope following the article [Tutorial: Create a policy assignment](https://learn.microsoft.com/en-us/azure/azure-arc/servers/learn/tutorial-assign-policy-portal#create-a-policy-assignment):

        Legacy - Enable Azure Monitor for VMs (This Initiative is required to configure dependency agent as well as Log Analytics agent on the VMs)
        Audit Windows machines that do not have the specified Windows PowerShell modules installed
        Audit Windows VMs with a pending reboot

    For further reference, you can find the list of Policies and Initiatives for Arc Enabled Servers [here](https://learn.microsoft.com/en-us/azure/azure-arc/servers/policy-reference).

- ***Update Management v2:***

    1. follow the article to assign Update management V2 Policies 

            [Preview]: Configure periodic checking for missing system updates on Azure Arc-enabled servers for Arc-enabled machines
            [Preview]: Machines should be configured to periodically check for missing system updates.
            [Preview]: Schedule recurring updates using Update Management Center

        described in

        [Enable Periodic assessment for your Arc machines using Policy](https://learn.microsoft.com/en-us/azure/update-center/periodic-assessment-at-scale#enable-periodic-assessment-for-your-arc-machines-using-policy)

        and 

        [Monitor if Periodic Assessment is enabled for your machines (both Azure and Arc-enabled machines)](https://learn.microsoft.com/en-us/azure/update-center/periodic-assessment-at-scale#monitor-if-periodic-assessment-is-enabled-for-your-machines-both-azure-and-arc-enabled-machines)

        [Create a maintenance configuration](https://learn.microsoft.com/en-us/azure/virtual-machines/maintenance-configurations-portal#create-a-maintenance-configuration) to create maintenance configuration for Linux and Windows machines to be used in Scheduling Policy.

        and

        [Schedule recurring updates for machines using Azure portal and Azure Policy](https://learn.microsoft.com/en-us/azure/update-center/scheduled-patching?tabs=schedule-updates-single-overview%2Cschedule-updates-scale-overview#dynamic-scoping-using-policy)

        **Note:**   Before creating the scheduling policy, copy the ARM ID of the created maintenance configuration in *properties* section.
    
    2. For Manual update check without waiting for policy follow [Check for Updates on scale following article](https://learn.microsoft.com/en-us/azure/update-center/view-updates?tabs=singlevm-overview%2Cat-scale-overview#check-updates-at-scale)
    
    3. For one time installation of updates follow [Install updates one time following Article](https://learn.microsoft.com/en-us/azure/update-center/deploy-updates?tabs=install-single-overview%2Cinstall-scale-overview#install-updates-at-scale)
 

- ***Inventory / Change Tracking***


    1. Please check if Automation account is created in ArcBox RG. If not, please create one. 
    following the article [Create a new Automation account in the Azure portal](https://learn.microsoft.com/en-us/azure/automation/automation-create-standalone-account?tabs=azureportal#create-a-new-automation-account-in-the-azure-portal).

    2. Please check if Change Tracking and Inventory is enabled for the Automation account. If not, please enable folowing the article [Enable Change Tracking and Inventory](https://learn.microsoft.com/en-us/azure/automation/change-tracking/enable-from-automation-account#enable-machines-in-the-workspace)
    
    3. Follow the article [Manage Change Tracking and Inventory](https://learn.microsoft.com/en-us/azure/automation/change-tracking/manage-change-tracking)
    In this article exercie the scenarios below:
        * Configure file tracking on Windows
        * Configure file tracking on Linux
        * Track file contents
        * Enable tracking for file content changes
        * View the contents of a tracked file
        * Track registry keys
        * Search logs for change records

- ***Remote  Connect SSH***

    We are going to make ssh connection to one of the Windows Arc enabled Servers. SSH server services needs to be enabled on the server side. 

    1. Logon to one of the Windows Servers using Hyper-V console on Arc Box vm and enable SSH server following the article

    [Get started with OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell)

    Make sure "OpenSSH SSH Server" and "OpenSSH Authentication Agent" services are started on the Arc enabled server.

    2. Enable SSH on azure connected machine agent and enable connection points following the article
 
    [(Preview) SSH access to Azure Arc-enabled servers - Azure Arc | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-arc/servers/ssh-arc-overview?tabs=azure-cli)

    3. Try remote SSH to Arc Enabled Server using command line  

- ***Azure Key Vault***

    We'll be exercising to deploy a self-signed certificate to Arc enabled Server using Azure KeyVault.

    1. Follow the article to create [Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/general/quick-create-portal#create-a-vault) 

    2. Follow the article to [Set and Retrieve Certificate from Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/certificates/quick-create-portal)
    
    3. Create access policy on Azure Key Vault you have created. You can configure permissions on your vault by going to it in the Azure Portal, clicking Access policies in the navigation pane, and then Add Access Policy.

     In the Secret permissions drop down, tick the boxes for Get and List. Then, next to Select Principal, click None selected to open the AAD object picker. 

    Search for your Arc enabled server by its name, click it, then click Select. Click Add to finish configuring the Arc enabled server's permissions then click Save to commit the change.
    
    4. Modify and run the following lines in the below PowerShell script

```Powershell
$Settings = @{
  secretsManagementSettings = @{
    observedCertificates = @(
      "https://YOURVAULTNAME.vault.azure.net/secrets/YOURCERTIFICATENAME"
      # Add more here in a comma separated list
    )
    certificateStoreLocation = "LocalMachine"
    certificateStoreName = "My"
    pollingIntervalInS = "3600" # every hour
  }
  authenticationSettings = @{
    # Don't change this line, it's required for Arc enabled servers
    msiEndpoint = "http://localhost:40342/metadata/identity"
  }
}

$ResourceGroup = "ARC_SERVER_RG_NAME"
$ArcMachineName = "ARC_SERVER_NAME"
$Location = "ARC_SERVER_LOCATION (e.g. eastus2)"

New-AzConnectedMachineExtension -ResourceGroupName $ResourceGroup -MachineName $ArcMachineName -Name "KeyVaultForWindows" -Location $Location -Publisher "Microsoft.Azure.KeyVault" -ExtensionType "KeyVaultForWindows" -Setting (ConvertTo-Json $Settings)
```

 

- ***Windows Admin Center*** 

    Follow the article to install and connect to Windows Admin Center on Arc Enabled Servers 
    [Manage Azure Arc-enabled Servers using Windows Admin Center in Azure preview | Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/manage/windows-admin-center/azure/manage-arc-hybrid-machines)

- ***Azure Monitor*** [Onboard Azure Arc-enabled servers to VM insights - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-azure-arc-enabled-servers/3-onboard-azure-arc-enabled-servers-to-vm-insights)
- Alert: Agent version alert
  - Alert: Heartbeat Alert
  - Failed connections alert, open ports
- Custom script extension

- Security Baseline Assessment
- Simulate endpoint attack
  - Powershell script in fileless attack
  - Live response tutorial
  - custom detection
- Sentinel enable
