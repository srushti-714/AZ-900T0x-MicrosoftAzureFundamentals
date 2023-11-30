
## 1.	Create a VM with Azure PowerShell
### Task 1: Configure the Cloud Shell

In this task, we will configure Cloud Shell.

1. From the Azure portal, open the **Azure Cloud Shell** by clicking on the icon in the top right of the Azure Portal.

    ![Screenshot of Azure Portal Azure Cloud Shell icon.](../images/AZ-900-1001.png)

1. If you have previously used the Cloud Shell, proceed to the next task.

1. When prompted to select either **Bash** or **PowerShell**, select **PowerShell**.

1. When prompted, select **Show advanced settings** and then select **Use existing** and choose existing resource group. Then select **Create new** against Storage account as well as File Share and provide a unique value in both of the fields and then click on **Create storage**, and wait for the Azure Cloud Shell to initialize.

### Task 2: Create a virtual machine

In this task, we will use PowerShell to create a resource group and a virtual machine.

1. Ensure **PowerShell** is selected in the upper-left drop-down menu of the Cloud Shell pane.

1. In the PowerShell session, within the Cloud Shell pane, get existing resource group.

    ```
    Get-AZResourceGroup
    ```

1. Verify your resource group.

    ```
    Get-AzResourceGroup | Format-Table
    ```
1. Run the following command to registe the EncryptionAtHost feature using the command.

    ```
    Register-AzProviderFeature -FeatureName "EncryptionAtHost" -ProviderNamespace "Microsoft.Compute"
    ```
1. Create a virtual machine. When prompted provide the username (**azureuser**) and the password (**Pa$$w0rd1234**) that will be configured as the local Administrator account on that virtual machines. Ensure that you include the tick (`) characters at the end of each line except for the last one (there should not be any tick characters if you type entire command on a single line).

   **Note**: Replace StudentTestRG-<inject key="DeploymentID" enableCopy="false"/> in the below command with the Resource Group Name from the output 
   of the previous command

    ```
    New-AzVm `
    -ResourceGroupName 'StudentTestRG-[DeploymentId]' `
    -Name 'myVM' 
    -Location 'Canada Central'`
    -Image 'Win2019Datacenter' `
    -VirtualNetworkName 'myVnet'`
    -SubnetName 'mySubnet'`
    -SecurityGroupName 'myNetworkSecurityGroup' `
    -PublicIpAddressName 'myPublicIpAddress' `
    -OpenPorts 80,3389
    ```
    **Note**: Wait for VM to deploy before closing PowerShell

1. Close the PowerShell session Cloud Shell pane.

1. In the Azure portal, search for **Virtual machines** and verify the **myVM** is running. This may take a few minutes.

    ![Screenshot of the virtual machines page with myVM in a running state.](../images/psvm.png)

1. Access the new virtual machine and review the Overview and Networking settings to verify your information was correctly deployed.

## 2.	Create a VM with the Azure CLI:

### Task 1: Use CLI to create a virtual machine

In this task, we will use Azure CLI to create a resource group and a virtual machine.  

1. Ensure **Bash** is selected in the upper-left drop-down menu of the Cloud Shell pane (and if not, select it).

    ![Screenshot of Azure Portal Azure Cloud Shell with the Bash dropdown highlighted.](../images/image-002.png)

1. In the Bash session, within the Cloud Shell pane, get existing resource group. 

    ```cli
    az group list
    ```

1. Format resource group listing output.

    ```cli
    az group list --output table
    ```

1. Create a new virtual machine. Make sure that each line except for the last one is followed by the backslash (`\`) character. If you type the whole command on the same line, do not use any backslash characters. 

    **Note**: If you are using the command line on a Windows computer, replace the backslash (`\`) character with the caret (`^`) character.
    
    **Note**: Replace StudentTestRG-[deployId] with  **myRGCLI-<inject key="DeploymentID" enableCopy="false" />**

    ```cli
   az vm create \
    --name myVMCLI \
    --resource-group StudentTestRG-[deployId] \
    --image Ubuntu2204 \
    --location Canadacentral \
    --admin-username azureuser \
    --admin-password Pa$$w0rd1234
    ```
     
    **Note**: The command will take 2 to 3 minutes to complete. The command will create a virtual machine and various resources associated with it such as storage, networking and security resources. Do not continue to the next step until the virtual machine deployment is complete. 

1. When the command finishes running, in the browser window, close the Cloud Shell pane.

1. In the Azure portal, search for **Virtual machines** and verify that **myVMCLI** is running.

    ![Screenshot of the virtual machines page with myVMPS in a running state.](../images/clivm.png)

## 3.	Create a SQL database:

### Task 1: Create the database

In this task, we will create a SQL database based on the AdventureWorksLT sample database. 

1. On the Azure portal, from the **Search resources, services, and docs** blade, search for and select **SQL databases**, and then click **+ Create**. 

1. On the **Basics** tab, fill in this information.  

    | Setting | Value | 
    | --- | --- |
    | Subscription | **Choose your subscription** |
    | Resource group | **myRGDb-<inject key="DeploymentID" enableCopy="false"/>** |
    | Database name| **db1** | 
    
1. Next to the **Server** drop down list, click **Create new**. Click **OK** when finished.          

    | Setting | Value | 
    | --- | --- |
    | Server name | **sqlserver<inject key="DeploymentID" enableCopy="false"/>** (must be unique) |
    | Location | **Canada Central** |
    | Authentication method | **Use SQL authentication** | 
    | Server admin login | **sqluser** |
    | Password | **Pa$$w0rd1234** |
   
1. Move to the **Networking** tab and configure the following settings (leave others with their defaults) 

    | Setting | Value | 
    | --- | --- |
    | Connectivity method | **Public endpoint** |    
    | Allow Azure services and resources to access this server | **Yes** |
    | Add current client IP address | **No** |
  
    
   ![Screenshot of the Networking tab of the Create SQL Database blade with settings selected as per the table and the Review + create button highlighted.](../images/0501b.png)

1. Move to the **Additional settings** tab. We will be using the AdventureWorksLT sample database, if pop-up comes, click on **OK**.

    | Setting | Value | 
    | --- | --- |
    | Use existing data | **Sample** |
   

    ![Screenshot of the Additional settings tab of the Create SQL Database blade with settings selected as per the table and the Review + create button highlighted.](../images/0501c.png)

1. Click **Review + create** and then click **Create** to deploy and provision the resource group, server, and database. It can take approx. 2 to 5 minutes to deploy.

1. Go to the resource tab to locate the SQL database you created. You may need to refresh.

## 4.	Create a virtual network: 

### Task 1: Create a virtual network

In this task, we will create a virtual network. 

**Note:** Before beginning the lab, disable both the public and private firewall in your virtual machine by opening the Start menu > Settings > Network and Internet > Locate Windows Firewall

1. On the Azure portal, from the **Search resources, Services, and docs(G+/)** blade, search for and select **Virtual networks**, and then click **+ Create**. 

1. On the **Create virtual network** blade, fill in the following (leave the defaults for everything else):


   | Setting | Value | 
   | ---     | ---   |
   | Name    | **vnet1** |
   | Subscription | **Choose your subscription**  |
   | Resource group |  **StudentTestRG-<inject key="DeploymentID" enableCopy="false"/>** |
   | Location | **Canada Central** |


1. On the **Create virtual network** blade, go to the IP Addresses tab and delete precreated IP address and create the new address space.

    | Setting | Value | 
    | --- | --- |
    | Address space |**10.1.0.0/16**|
    
 1. Click on **+ Add Subnet** and enter the following (Delete if any subnet exists already with the name default) then click on **Add**:
  
    | Setting | Value | 
    | --- | --- |
    | Subnet Name |**default**|
    | Subnet Address range | **10.1.0.0/24**|
  
    
    ![Screenshot of the "IP Addresses" step of Create virtual network blade with the default fields.](../images/0301b.png)

1. Click the **Review + create** button. Ensure the validation passes.

1. Click the **Create** button to deploy the virtual network. 

    **Note**: In your organization, how will you know which virtual networks and IP addressing you will need?

### Task 2: Create two virtual machines

In this task, we will create two virtual machines in the virtual network. 

1. From the **Search resources, Services, and docs(G+/)** blade, search for **Virtual machines** and then click **+ Create** and choose **Azure virtual machine**.

1. On the **Basics** tab, fill in the following information (leave the defaults for everything else):

   | Setting | Value | 
   | --- | --- |
   | Subscription | **Use default supplied**  |
   | Resource group |  **StudentTestRG-<inject key="DeploymentID" enableCopy="false"/>** |
   | Virtual machine name | **vm1**|
   | Region | **Canada Central** |
   | Image | **Windows Server 2019 Datacenter -Gen2** |
   | Size | **Standard_D2s_v3** |
   | Username| **azureuser** |
   | Password| **Pa$$w0rd1234** |
   | Public inbound ports| Select **Allow selected ports**  |
   | Selected inbound ports| **RDP (3389)** |
   |||

1. Select the **Networking** tab. Make sure the virtual machine is placed in the vnet1 virtual network. Review the default settings, but do not make any other changes. 

   | Setting | Value | 
   | --- | --- |
   | Virtual network | **vnet1** |
   |||

1. Click **Review + create**. After the Validation passes, click **Create**. Deployment times can vary but it can generally take between three to six minutes to deploy.

1. Monitor your deployment, but continue on to the next step. 

1. Create a second virtual machine by repeating steps **2 to 4** above. Make sure you use a different virtual machine name, that the virtual machine is within the same virtual network, and is using a new public IP address:

    | Setting | Value |
    | --- | --- |
    | Resource group | **StudentTestRG-<inject key="DeploymentID" enableCopy="false"/>** |
    | Virtual machine name |  **vm2** |
    | Virtual network | **vnet1** |
    | Public IP | (new) **vm2-ip** |
    |||

1. Wait for both virtual machines to deploy. 

### Task 3: Test the connection 

In this task, we will try to test whether the virtual machines can communicate (ping) each other. If not we will install a rule to allow an ICMP connection. Usually ICMP connections are automatically blocked.

1. From the **All resources** blade, search for **vm1**, open its **Overview** blade, and make sure its **Status** is **Running**. You may need to **Refresh** the page.

1. On the **Overview** blade, click the **Connect** button and select RDP.

    **Note**: The following directions tell you how to connect to your VM from a Windows computer. 

1. On the **Connect to virtual machine** blade, keep the default options to connect by IP address over port 3389 and click **Download RDP File**.

1. Open the downloaded RDP file and click **Connect** when prompted. 

1. In the **Windows Security** window, type the username **azureuser** and password **Pa$$w0rd1234** and then click **OK**.

1. You may receive a certificate warning during the sign-in process. Click **Yes** or to create the connection and connect to your deployed VM. You should connect successfully. Close the Windows Server and Dashboard windows that pop up. You should see a Blue Windows background. You are now in your virtual machine.

    **Repeat step 1 to 6 for vm2.**

1. In **both** newly created virtual machines(vm1,vm2), connect via RDP and **disable both the public and private firewall** by opening the Start menu > Settings > Network and Internet > Locate Windows Firewall.

    ![image](../images/vnet01.png)


1. Open up a PowerShell command prompt on the virtual machine(vm1), by clicking the **Start** button, typing **PowerShell**, right clicking **Windows PowerShell** in the right-click menu, and clicking **Run as administrator**

1. Try to ping vm2 (make sure vm2 is running). 
    ```
    ping vm2
    ```
1. You should be successful. You have pinged VM2 from VM1.
    
     ![Screenshot of the pinged VM2 from VM.](../images/AZ900Lab4.png)
   
## 5.	Create an Azure Key Vault, and add a test secret:

### Task 1: Create an Azure Key Vault

1. On the Azure Portal, from the **All services** blade, search for and select **Key vaults**, then select **+ Create**.

1. Configure the key vault. Leave the defaults for everything else.

    | Setting | Value | 
    | --- | --- |
    | Subscription | **Use your subscription** |
    | Resource group | **StudentTestRG-<inject key="DeploymentID" enableCopy="false" />**  |
    | Key vault name | **keyvaulttest<inject key="DeploymentID" enableCopy="false" />** |
    | Location | **Canada Central** |
    | Pricing tier | **Standard** |
    | | |

1. Click **Review + create**, and then click **Create**. 

1. Once the new key vault is provisioned, click **Go to resource**. Or you can locate your new key vault by searching for it. 

1. Click on the key vault **Overview** tab and take note of the **Vault URI**. Applications that use your vault through the REST API will need this URI.

1. Take a moment to browse through some of the other key vault options. Under **Settings** review **Keys**, **Secrets**, **Certificates**, **Access Policies**, **Firewalls and virtual networks**.

   **Note**: Your Azure account is the only one authorized to perform operations on this new vault. You can modify this if you wish in the **Settings** and then the **Access policies** section.

### Task 2: Add a secret to the Key Vault
        
In this task, we will add a password to the key vault. 

1. Under **Objects** click **Secrets**, then click **+ Generate/Import**.

1. Configure the secret. Leave the other values at their defaults. Notice you can set an activation and expiration date. Notice you can also disable the secret.

    | Setting | Value | 
    | --- | --- |
    | Upload options | **Manual** |
    | Name | **ExamplePassword** |
    | Value | **hVFkk96** |
    | | |

1. Click **Create**.

1. Once the secret has been successfully created, click on the **ExamplePassword**, and note it has a status of **Enabled**

1. Click the current version, and note the **Secret Identifier**. This is the URL value that you can now use with applications. It provides a centrally managed and securely stored password.

## 6.	Configure RBAC:

### Task 1: View and assign roles

In this task, we will assign the Virtual machine contributor role. 

1. On the Azure portal, from the **Search resources, services, and docs** blade, search for and select **Resource groups**

1. Then view the existing resource group. 

    | Setting | Value |
    | -- | -- |
    | Resource group | **StudentTestRG-<inject key="DeploymentID" enableCopy="false"/>** |

     
1. Click on the existing resource group

1. You will be directed to the overview page of the resource group

1. Click on the **Access control (IAM)** blade, and then switch to the **Roles** tab. Scroll through the large number of roles definitions that are available. Use the Informational icons to get an idea of each role's permissions. Notice there is also information on the number of users and groups that are assigned to each role.

   ![image](../images/AZ-900-access.png)

1. Follow the following step:

   - Switch to the **Role assignments** tab of the **StudentTestRG-<inject key="DeploymentID" enableCopy="false"/> Access control (IAM)** blade, click **+ Add** and then click **Add role assignment**.
   
   - In  Assignment type keep things as default, then switch to Roles tab, Search for the **Virtual Machine Contributor** role and select.

   - Switch to the "Members" tab and Assign access to: the user, group, or service principal. Then click + Select members and type your azure account name (Username: <inject key="AzureAdUserEmail"></inject>) to the popup search function and hit 'select.' Then hit 'Review + Assign'.

      ![image](../images/AZ-900-module-14-addrole.png)

     **Note:** The Virtual machine contributor role lets you manage virtual machines, but not access their operating system or manage the virtual network and storage account they are connected to. User name can be obtained from the Lab Environment output page


1. **Refresh** the Role assignments page and ensure you are now listed as a Virtual machine contributor. 

    **Note**: This assignment does not grant you any additional privileges, since your account has already the Owner role, which includes all privileges associated with the Contributor role.

### Task 2: Monitor role assignments and remove a role

In this task, we will view the activity log to verify the role assignment, and then remove the role. 

1. On the myRGRBAC-<inject key="DeploymentID" enableCopy="false"/> resource group blade, click **Activity log**.

1. Click **Add filter**, select **Operation**, and then **Create role assignment**.

    ![Screenshot of the Activity log page with configured filter.](../images/1503.png)

1. Verify the Activity log shows your role assignment. (With your User Id). 

## 7.	Implement Azure Functions:

### Task 1: Create a Function app

In this task, we will create a Function app.

1. On the Azure portal, in the **Search resources, services, and docs** text box at the top of the portal, search for and select **Function App** and then, from the **Function App** blade, click **+ Create**.

1. On the **Basic** tab of the **Function App** blade, specify the following settings and leave all others with their default values: 

    | Settings | Value |
    | -- | --|
    | Subscription | the name of your Azure subscription |
    | Resource group | the name of **existing** resource group **StudentTestRG-<inject key="DeploymentID" enableCopy="false"/>**  |
    | Function App name | **function-<inject key="DeploymentID" enableCopy="false"/>** |
    | Publish | **Code** |
    | Runtime stack | **.NET** |
    | Version | **6 (LTS)** |
    | Region | **Canada Central** |
    
    
    ![Screenshot of the Function App page with the new Function app.](../images/AZ-900-functionapp.png)
    
1. Click **Review + Create** and, after successful validation, click **Create** to begin provisioning and deploying your new Azure Function App.

1. Wait for the notification that the resource has been created.

1. Navigate back to the **Function App** blade, click **Refresh** and verify that the newly created function app has the **Running** status. 

    ![Screenshot of the Function App page with the new Function app.](../images/az-204_03-01.png)

# Task 2: Create a HTTP triggered function and test

In this task, we will use the Webhook + API function to display a message when there is an HTTP request. 

1. On the overview blade, in the **Functions (1)** section, click **Create in Azure portal (2)**.

    ![Screenshot of the choose a development environment step in the azure functions for dot net getting started pane inside Azure portal. The display elements for creating a new in-portal function are highlighted. The highlighted elements are expand the function app, add new function, in-portal, and the continue button.](../images/function01.png)

1. On the **Templates** tab of the **Create Function** blade, click **HTTP trigger (1)**. Click **Create (2)**  

    ![Screenshot of the create a function step in the azure functions for dot net getting started pane inside Azure portal. The HTTP trigger card is highlighted to illustrate the display elements used to add a new webhook to an Azure function.](../images/function02.png)

1. On the **HttpTrigger1** blade, in the **Developer** section, click **Code + Test**. 

1. On the **HttpTrigger1 \| Code + Test** blade, review the auto-generated code and note that the code is designed to run an HTTP request and log information. Also, notice the function returns a Hello message with a name. 

    ![Screenshot of the function code. The Hello message is hightlighted.](../images/az-204_03-04.png)

1. Click **Get function URL** from the top section of function editor. 

1. Ensure that the value in the **Key** drop-down list is set to **default** and click **Copy** to copy the function URL. 

    ![Screenshot of the get function URL pane inside the function editor in Azure portal. The display elements get function URL button, set key dropdown, and copy URL button are highlighted to indicate how to obtain and copy the function URL from the function editor.](../images/az-204_03-05.png)

1. Open a new browser tab and paste the copied function URL into your web browser's address bar. When the page is requested the function will run. Notice the returned message stating that the function requires a name in the request body.

    ![Screenshot of the please provide a name message.](../images/az-204_03-06.png)

1. Append **&name=*yourname*** to the end of the URL.

    **Note**: Replace ***yourname*** with your first name. For example, if your name is Cindy, the final URL will resemble the following `https://azfuncxxx.azurewebsites.net/api/HttpTrigger1?code=X9xx9999xXXXXX9x9xxxXX==&name=cindy`

    ![Screenshot of a highlighted function URL and an appended example user name in the address bar of a web browser. The hello message and user name are also highlighted to illustrate the output of the function in the main browser window.](../images/az-204_03-07.png)

## 8.	Configure Azure Policy:

### Task 1: Create a Policy assignment

In this task, we will configure the allowed location policy and assign it to our subscription. 

1. On the Azure portal, from the **Search resources, Services, and docs(G+/)** blade, search for and select **Policy**, under the **Authoring** section click **Definitions**.  Take a moment to review the list of built-in policy definitions. For example, in the **Category** drop-down select only **Compute**. Notice the **Allowed virtual machine size SKUs** definition enables you to specify a set of virtual machine SKUs that your organization can deploy.

1. Return to the **Policy** page, under the **Authoring** section click **Assignments**. An assignment is a policy that has been assigned to take place within a specific scope. For example, a definition could be assigned to the subscription scope. 

1. Click **Assign Policy** at the top of the **Policy - Assignments** page.

1. On the **Assign Policy** page, select the Scope selector by clicking the ellipsis.

    ![Screenshot of the scope selector ellipses.](../images/scope.png)

1. Ensure your subscription is selected. Your subscription name might be different. Notice you can optionally scope the policy to a resource group. Leave the defaults and click **Select**. 

    **Note**: A scope determines what resources or grouping of resources the policy assignment applies to. In our case we could assign this policy to a specific resource group, however, we chose to assign the policy at the subscription level. Be aware that resources can be excluded based on the scope configuration. Exclusions are optional.

    ![Screenshot of the Scope pane with field values filled in and the Select button highlighted. ](../images/scope2.png)

1. Select the **Policy definition** ellipsis button. In the **Search** box type **location** and click on the **Allowed locations** definition, then click **Add**.

    **Note**: This **Allowed Locations** policy definition will specify a location into which all resources must be deployed. If a different location is chosen, deployment will not be allowed. For more information view the [Azure Policy Samples](https://docs.microsoft.com/en-us/azure/governance/policy/samples/index) page.

   ![Screenshot of Available Definitions pane with various fields highlighted and the Audit VMs that do not use managed disks option selected.](../images/location.png)

1.  In the **Assign policy** pane, switch to the **Parameters** tab, click on the arrow at the end of the **Allowed locations** box, and from the subsequent list choose **Japan West**. Leave all other values as they are and click **Review + create**, and then **Create**.

    ![Screenshot of Assign policy pane with various fields filled in along with the location Japan West populated and the assign button highlighted.](../images/allowedloc.png)

1. The **Allowed locations** policy assignment is now listed on the **Policy - Assignments** pane and it is now in place, enforcing the policy at the scope level we specified (subscription level).

### Task 2: Test Allowed location policy

In this task, we will test the Allowed location policy. 

1. In the Azure Portal, from the **Search resources, Services, and docs(G+/)** blade, search for and select **Storage accounts**, and then click **+ Create**.

1. Configure the storage account. Leave the defaults for everything else. 

    | Setting | Value | 
    | --- | --- |
    | Subscription | **Use your subscription** |
    | Resource group | **StudentTestRG-<inject key="DeploymentID" enableCopy="false"/>**  |
    | Storage account name | **storageaccount<inject key="DeploymentID" enableCopy="false"/>** |
    | Location | **(US) East US** |
    | | |

1. Click on **Review** and once validation gets success, click on **Create**.
    
   **Note**: You will receive the error message under the Region setting stating that Policy enforcement and Value does not meet requirements on resource, including the **Allowed locations** policy name.

## You have successfully completed Test.