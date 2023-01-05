# Day 1 - Lab (Optional)

## Deploy lab infrastructure for Azure Stack HCI

>
> **Use Cloud Shell Bash for the deployment**

Make sure you have configured **main.parameters.json** with the following settings described on the following guide

    deployBastion = false
    registerCluster = false
    deployAKSHCI = false
    deployResourceBridge = false

> **main.parameters.json** located under /azure_arc/azure_jumpstart_hcibox/bicep
    >
    > cd /azure_arc/azure_jumpstart_hcibox/bicep


[Deploy Azure Arc Jumpstart HCIBOX](https://azurearcjumpstart.io/azure_jumpstart_hcibox)

> *Deployment takes about 2-3 hours to finalize*

## Register Windows Admin Center

[Register Windows Admin Center](https://learn.microsoft.com/en-us/azure-stack/hci/manage/register-windows-admin-center)

## Azure Stack HCI deployment (optional)

> Note that HCIBOX comes with Azure Stack HCI cluster already deployed. If you would like to experience Azure Stack HCI cluster creation run the following commands to remove cluster.

```powershell

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

[Azure Stack HCI deployment](https://learn.microsoft.com/en-us/azure-stack/hci/deploy/operating-system)
[Create Azure Stack HCI cluster](https://learn.microsoft.com/en-us/azure-stack/hci/deploy/create-cluster)
[Set up a cluster witness](https://learn.microsoft.com/en-us/azure-stack/hci/manage/witness)
