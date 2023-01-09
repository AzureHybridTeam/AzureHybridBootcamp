# Day 3 - Lab
## Arc Enabled Data Services (takes 2-3 hours)

Before start make sure about below prerequisites:

1.Have a Kubernetes cluster and Have access to your Kubernetes Cluster

2.Install  [client tools](https://learn.microsoft.com/en-us/azure/azure-arc/data/install-client-tools) 

Lab steps:

- [Deploy directly connected data controller from Azure Portal](https://learn.microsoft.com/en-us/training/modules/deploy-configure-explore-azure-arc-enabled-data-services/5-exercise-deploy-azure-arc-data-controller?ns-enrollment-type=learningpath&ns-enrollment-id=learn.get-started-azure-arc-enabled-sql-managed-instance)

- [Deploy an Arc-enabled SQL MI (BC) & Connect](https://learn.microsoft.com/en-us/training/modules/deploy-configure-azure-arc-enabled-sql-managed-instance/4-exercise-deploy-azure-arc-enabled-sql-mi?ns-enrollment-type=learningpath&ns-enrollment-id=learn.get-started-azure-arc-enabled-sql-managed-instance)
- [Restore AdventureWorks2019 Azure Arc-enabled SQL Managed Instance](https://learn.microsoft.com/en-us/training/modules/deploy-configure-azure-arc-enabled-sql-managed-instance/5-exercise-restore-adventureworks2019-azure-arc-enabled-sql-mi)

- [Using Azure Arc-enabled SQL Managed Instance (Exercise 1-2-3)](https://learn.microsoft.com/en-us/training/modules/deploy-configure-azure-arc-enabled-sql-managed-instance/7-exercise-using-azure-arc-enabled-sql-managed-instance)

- [Use Grafana to monitor performance of Azure Arc-enabled SQL Managed Instance](https://learn.microsoft.com/en-us/training/modules/monitor-azure-arc-enabled-sql-managed-instance-security-performance/4-exercise-using-grafana-performance-monitor-azure-arc-enabled-sql-mi?ns-enrollment-type=learningpath&ns-enrollment-id=learn.get-started-azure-arc-enabled-sql-managed-instance)

- [Configure and explore High Availability/Disaster Recovery for Azure Arc-enabled SQL Managed Instance(Exercise 1-3-4-5)](https://learn.microsoft.com/en-us/training/modules/high-availability-disaster-recovery-azure-arc-enabled-sql-managed-instance/4-exercise-configure-and-explore-high-availability-disaster-recovery?ns-enrollment-type=learningpath&ns-enrollment-id=learn.get-started-azure-arc-enabled-sql-managed-instance)

 
## Container Apps on Arc Enabled Kubernetes (takes about 1 hour)

Before start be sure about below recommendations:

1. Do not use corp account for azure portal!
2. For the first lab scenario there is a definition as:

WORKSPACE_NAME="$GROUP_NAME-workspace"

But, it is used as **wORKSPACE_NAME** afterwards. 
Be sure to change **wORKSPACE_NAME** to **WORKSPACE_NAME** with capital **W**!

Lab Steps:

-   Environment configuration [Enable Azure Container Apps on Azure Arc-enabled Kubernetes](https://learn.microsoft.com/en-us/azure/container-apps/azure-arc-enable-cluster)
-   Sample app deployment [Create an Azure Container App on Azure Arc-enabled Kubernetes](https://learn.microsoft.com/en-us/azure/container-apps/azure-arc-create-container-app)
