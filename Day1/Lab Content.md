# Day 1 - Lab

Below are the lab items that are going to be covered.

- **Applying Azure Policy to Arc Enabled Servers:**

 In this lab environment we are using [**Jumpstart ArcBox for IT Pros**](https://azurearcjumpstart.io/azure_jumpstart_arcbox/itpro) as vm environment.  
 As previously stated please make sure "Microsoft defender for Cloud" environment settings have been enabled prior to lab described [here](https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-enhanced-security). 

Make sure all of the settings are enabled and defender uses the Log Analytics Workspace that ArcBox has created as shown in the pictures
[Defender Plans settings](/Day1/pics/defender1.jpg) and [Setting & Monitoring](/Day1/pics/defender2.jpg).

Arcbox has already created some of the Policies, we'll omit these and assign our own policy settings that should be used in customer deployments.
Please assign Initiatives/Policies listed below within **Resource Group** scope following the article [Tutorial: Create a policy assignment](https://learn.microsoft.com/en-us/azure/azure-arc/servers/learn/tutorial-assign-policy-portal#create-a-policy-assignment):

        Legacy - Enable Azure Monitor for VMs (This Initiative is required to configure dependency agent as well as Log Analytics agent on the VMs)
        Audit Windows machines that do not have the specified Windows PowerShell modules installed
        Audit Windows VMs with a pending reboot

You can find the list of Policies and Initiatives for Arc Enabled Servers [here](https://learn.microsoft.com/en-us/azure/azure-arc/servers/policy-reference).

- **Update Management v2:**

1. follow the article to assign Update management V2 Policies 

        [Preview]: Configure periodic checking for missing system updates on Azure Arc-enabled servers for Arc-enabled machines
        [Preview]: Machines should be configured to periodically check for missing system updates.

described in

[Enable Periodic assessment for your Arc machines using Policy](https://learn.microsoft.com/en-us/azure/update-center/periodic-assessment-at-scale#enable-periodic-assessment-for-your-arc-machines-using-policy)

and 

[Monitor if Periodic Assessment is enabled for your machines (both Azure and Arc-enabled machines)](https://learn.microsoft.com/en-us/azure/update-center/periodic-assessment-at-scale#monitor-if-periodic-assessment-is-enabled-for-your-machines-both-azure-and-arc-enabled-machines)

2. Create Maintenance Configuration for Linux and Windows machines.
    Follow the article [Create a maintenance configuration](https://learn.microsoft.com/en-us/azure/virtual-machines/maintenance-configurations-portal#create-a-maintenance-configuration) to create maintenance configuration for Linux and Windows machines.  

- **Inventory / change tracking**

- **Remote  Connect SSH** [(Preview) SSH access to Azure Arc-enabled servers - Azure Arc | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-arc/servers/ssh-arc-overview?tabs=azure-cli)

- **Windows Admin Center** [Manage Azure Arc-enabled Servers using Windows Admin Center in Azure preview | Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/manage/windows-admin-center/azure/manage-arc-hybrid-machines)

- **Azure Monitor** [Onboard Azure Arc-enabled servers to VM insights - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-azure-arc-enabled-servers/3-onboard-azure-arc-enabled-servers-to-vm-insights)
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
