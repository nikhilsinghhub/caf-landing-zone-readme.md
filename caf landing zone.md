# CAF Platform Starter Terraform Landing Zones
-	Single Subscription Deployment Lab

 - Setup your organization

 - Organize your private repository

# The first step is create a private repository in your current organization. It has to be a git repository.

Clone the platform starter repository

The platform starter project is an empty environment that get you started with your initial configuration files and create a coherent stack.

Locally

# Adjust the name of your organization and repository

# You should observe:
Cloning into 'contoso'...
remote: Enumerating objects: 429, done.
remote: Counting objects: 100% (429/429), done.
remote: Compressing objects: 100% (320/320), done.
remote: Total 429 (delta 110), reused 307 (delta 77), pack-reused 0
Receiving objects: 100% (429/429), 2.93 MiB | 1.52 MiB/s, done.
Resolving deltas: 100% (110/110), done.

Open Visual Studio Code from the contoso folder
Code .
Trust the repository

![trust](https://user-images.githubusercontent.com/72153567/216055301-41709159-d9a9-4bc9-a1bd-9c360ea87215.png)


 
Visual Studio code
Visual Studio code should open your cloned repository and display the following structure.
Add remote development extension
Select the Remote - Containers extension and click Install.

![select remote](https://user-images.githubusercontent.com/72153567/216055763-e106e51f-d0af-40a6-a962-e4fa1c2f1bb1.png)


 
Re-open vscode in the dev container
Click on the green bottom left button From the menu select the option

![reopen in container](https://user-images.githubusercontent.com/72153567/216056179-3d23695d-1425-4643-b767-9705446cd51d.png)



You should now see the following terminal. This terminal is where you will run all terminal commands described in this on-boarding tutorial

![terminal](https://user-images.githubusercontent.com/72153567/216056552-ab0a3569-b3a0-4813-a59a-896f63661367.png)


 
Clone the CAF Terraform landingzones code
Now that you have the configuration folder ready to use, let's clone the logic of landing zones (the Terraform code) that we will use to run the commands.

# NOTE

The CAF Terraform landingzones framework assumes the landingzones Terraform code is cloned in a repository called landingzones.

# CAUTION
Do not use another name as landingzones. It is a convention used to drive consistency.
git clone https://github.com/Azure/caf-terraform-landingzones.git landingzones

# Go to the landingzones folder
➜  caf git:(main) ✗ cd landingzones 

# Note all folders are starting with /tf/caf in the devcontainers. 
➜  landingzones git:(main) ✗ pwd
/tf/caf/landingzones
➜  landingzones git:(main) ✗
Switch to the selected landingzones tag
Latest features on CAF Terraform landingzones repository are released on regular basis. In order to align the deployment instructions, you need to make sure the Terraform code is also using the correct branch or tag.Please check the latest tag from the landingzones repo at https://github.com/Azure/caf-terraform-landingzones/releases .

From the terminal, run the following command to checkout to the latest tag:
As, when we are updating the doc, latest tag available is 2203.1 as shown above.
git checkout 2203.1

# Note: switching to '2203.1'.

You are in 'detached HEAD' state. You can look around, makeexperimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.
NOTE
The detached head is expected as your are getting to a tag (release version) and not into a branch.

# Required privileges
NOTE
To deploy the platform landing zones, you need the following privileges
Azure Active Directory:
•	Global Administrator
Azure subscriptions:
•	1 subscription with owner privileges.
Management groups:
•	"management group contributor" permissions on a branch or root management group.

# There are 4 levels in CAF landing Zone 0,1,2,3



# LEVEL 0
 For level 0 – (Core platform automation) – It mainly used for State Management.

   The different landing zones represented in different state files at level 0 would typically be:
   -	The launchpad (storage accounts, Key Vault, RBAC, etc.) components related to Terraform state management.
   -	The subscription creation delegation capabilities derived from the Enterprise Agreement or Microsoft Customer Agreement.
   -	The credential rotation mechanisms and role-based access control core models.



## Pre-requisites


This scenario requires the following privileges:

| Component          | Privileges           |
|--------------------|----------------------|
| Active Directory   | Global Administrator |
| Azure subscription | Subscription owner   |

## Deployment

Elevate your credentials to the tenant root level to have enough privileges to create the management group hierarchy.
If the plan is not successfull you need to come back to the yaml ignite.yaml, fix the values, re-execute the rover ignite and then rover plan.
Execute a rover logout and rover login in order to make sure your azure sessions has the Azure groups membership updated

## Resources…..

# credentials

1.	azuread_api_permissions - You'll need to add additional permissions in order to use Microsoft Graph notifications. Choose Add a permission, and under Microsoft APIs, select Microsoft Graph, and then select Delegated permissions.

2.	azuread_applications – It Cover Application Identitity , Management , Connectivity , Subscription.

3.	azuread_groups_membership – Group membership is managed by both the group owner and the resource owner, letting either owner add or remove members from the group.

4.	azuread_roles – It cover azure service principals , privileged Role Administrator , Application Administrator , Groups Administrator and also specify identity roles “User Administrator””Application Administrator ””Groups Administrator” and Suscription Creation Roles”Application Administrator”  ”Groups Administrator”.

5.	azuread_service_principals - It Cover Application Identitity , Management , Connectivity , Subscription.

6.	Dynamic_keyvault_secrets – It cover subscription _id , tenant_id for level 0 and lower_stg , lower _rg , subscription_id , tenant_id for level 1 , and lower_stg , lower_rg , subscription_id, tenant_id for level 2.

7. Keyvaults – level 0 – It cover name , resource group key , tags- caf tfstate and Environment.

8. Landingzone – It enables application migration , modernization , and innovation at enterprise – scale in Azure.
backend_type = "azurerm"
  level        = "level0"
  key          = "launchpad"
  
# launchpad
1. azuread_api_permissions - You'll need to add additional permissions in order to use Microsoft Graph notifications. Choose Add a permission, and under Microsoft APIs, select Microsoft Graph, and then select Delegated permissions.

2.azuread_applications – It Cover Application Identitity , Management , Connectivity , Subscription.

3.	azuread_groups_membership – Group membership is managed by both the group owner and the resource owner, letting either owner add or remove members from the group.

4.	azuread_roles – It cover azure service principals , privileged Role Administrator , Application Administrator , Groups Administrator and also specify identity roles “User Administrator””Application Administrator ””Groups Administrator” and Suscription Creation Roles”Application Administrator”  ”Groups Administrator”.

5.	azuread_service_principals - It Cover Application Identitity , Management , Connectivity , Subscription.

6.	Dynamic_keyvault_secrets – It cover subscription _id , tenant_id for level 0 and lower_stg , lower _rg , subscription_id , tenant_id for level 1 , and lower_stg , lower_rg , subscription_id, tenant_id for level 2.

7. global setting – It consist passthrough the default naming convention , Inherit tags

8. keyvault access policies - It covers access policy identity , management and subscription for level 0,1,2.

9. keyvaults - Creation of policies ,caf platform maintainers , caf platform contributors as well as for level 1 and 2.

10.Landingzone – It enables application migration , modernization , and innovation at enterprise – scale in Azure.
backend_type = "azurerm"
  level        = "level0"
  key          = "launchpad"

11. Resource Groups – It specifies for level 0,1,2 with regions
resource_groups = {
  level0 = {
    name   = "caf-level0"
    region = "region1"
  }
  level1 = {
    name   = "caf-level1"
    region = "region1"
  }
  level2 = {
    name   = "caf-level2"
    region = "region1"
  }
}

 12. role mapping – In this resource we define different roles for management group “User Access Administrator” ”Management group contributor ” ”Owner” “Reader”.
     For Subscription – Logged in subscription “Owner” ”reader”

 13. storage accounts – It covers accounts name , resource key , account tier, access key , account replication type .
     Blob properties – versioning , access time 
     Containers state , tags.     





# Level 1

 Landing Zone 1 is the operational layer of the Azure Landing Zones and it contains the Azure subscriptions and services that are used for day-to-day operations.

 1. - Identity -  for core platform such as domain controller virtual machines, Azure Active Directory Domain Services, Azure AD Group mappings etc.

 2. -Management - for core platform capabilities such as log management, Azure Monitor capabilities, etc.

 3. -Subscription -  for core platform (to create the core enterprise-scale subscriptions like Identify, Management, Connectivity etc.)


# Identity

  1.	In Identity it cover azuread group – It consist  caf platform maintainers , caf platform contributors – level 0 , alz , identity ,management , connectivity ,          subscription creation platform , subscription creation landingzone.

  2.	landingzone – It consist of backend type , level , key ,global setting key , tfstate , workspace and level of launchpad.

  3.	Recovery Vaults – is a storage entity in azure that houses data. The data is typically copies of data , or configuration information for virtual machines(VMs), workloads , servers , or workstations.

  4.	Resource Groups – is a container that holds related resources for an Azure solutions , or that you want to manage as a group. It consist mainly management and          alerts for name and region.


# Management

  1.	Automations  - It Work on automate our Infra consist account with name and resource group key.

  2.	Azure log analytics – Extention sends the data to Azure Storage , Azure Monitor Metrics (Windows Only) and Azure Event Hubs. The log Analytics agent collects data      to Azure Monitor Logs.

  3.	Landingzone - It consist of backend type , level , key ,global setting key , tfstate , workspace and level of launchpad.

  4.	Monitor action groups – is resource for Monitor of Microsoft Azure consist of action group name . resource key , arm role alert , email receiver .

  5.	Recovery vaults – A recovery Services vault is a storage entity in azure that houses data.

  6.	Resource groups - is a container that holds related resources for an Azure solutions , or that you want to manage as a group. It consist mainly management and          alerts for name and region.

  7.	 Storage Accounts – It covers accounts name , resource key , account tier, access key , account replication type .



# Subscription

  1.	Landingzone – It consist type of backend , level1 , key of landongzone.




# Level 2 
asvm – Azure Subscription Vending Machine – 

  Including the virtual networking components like classic Virtual Network-based Hub and Spoke, Azure Virtual WAN, Azure Virtual WAN regional hub, site-to-site, point-   to-site and ExpressRoute connectivity objects, or third parties Network Virtual Appliances. Due to their regional nature, it is likely that each of those components   would live inside a different Terraform state file.

  1.	Azuread group – It consist caf ac landingzone maintainers non prod and caf ac landingzone maintainers prod.

  2.	Dynamic keyvault secret – The solution is to dynamically generate the resource ID for a key vault secret by using a linked template.

  3.	Keyvaults – It consist of level name , resource group key , tags, caf tfstate , caf environment , creation policies.

  4.	Landingzone - It consist of backend type , level , key ,global setting key , tfstate , workspace and level of launchpad.

  5.	Resource groups - is a container that holds related resources for an Azure solutions , or that you want to manage as a group. It consist mainly management and          alerts for name and region.

  6.	Role mapping – role mapping is the process whereby principals (users or groups ) are dynamically mapped to security roles at runtime.

  7.	Storage Accounts – This mainly creates a azure storage accounts consist of account kind, account tier , account replication type , blob properties , container          delete retention policy. Containers , tags , for level 3 and 4.    
