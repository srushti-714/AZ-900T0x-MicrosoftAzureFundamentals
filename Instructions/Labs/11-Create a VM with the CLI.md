# Lab 11 - Create a VM with the CLI

## Lab overview

In this walkthrough, we will configure the Cloud Shell, use Azure CLI to create a virtual machine, and review Azure Advisor recommendations.

## Lab objectives

In this lab, you will complete the following tasks:

+ Task 1: Configure the Cloud Shell
+ Task 2: Use CLI to create a virtual machine
+ Task 3: Execute commmands in the Cloud Shell
+ Task 4: Review Azure Advisor Recommendations

## Estimated timing: 15 minutes

## Architecture diagram

![](../images/az900lab11.png)

### Task 1: Configure the Cloud Shell

In this task, we will configure Cloud Shell. 

1. From the Azure portal, open the **Azure Cloud Shell** by clicking on the icon in the top right of the Azure Portal.

    ![Screenshot of Azure Portal Azure Cloud Shell icon.](../images/AZ-900-1101.png)

1. The first time you open the Cloud Shell, you may be prompted to choose the type of shell you want to use (*Bash* or *PowerShell*). If so, select **Bash**.
   
1. If you are prompted to create storage for your Cloud Shell, ensure your subscription is selected and click on **Show advanced settings**.

1. Please make sure you have selected your resource group **myRGCLI-<inject key="DeploymentID" enableCopy="false" />**.

1. Enter **blob<inject key="DeploymentID" enableCopy="false"/>** for the **Storage account**.

1. Enter **blobfileshare<inject key="DeploymentID" enableCopy="false"/>** for the  **File share** , then click on **Create Storage**.

### Task 2: Use CLI to create a virtual machine

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
    
    **Note**: Replace myRGCLI-[deployId] with  **myRGCLI-<inject key="DeploymentID" enableCopy="false" />**

    ```cli
    az vm create \
    --name myVMCLI \
    --resource-group myRGCLI-[deployId] \
    --image Win2019Datacenter \
    --location EastUS \
    --size Standard_B2s \
    --admin-username azureuser \
    --admin-password Pa$$w0rd1234
    ```    
    **Note**: The command will take 2 to 3 minutes to complete. The command will create a virtual machine and various resources associated with it such as storage, networking and security resources. Do not continue to the next step until the virtual machine deployment is complete. 

1. When the command finishes running, in the browser window, close the Cloud Shell pane.

1. In the Azure portal, search for **Virtual machines** and verify that **myVMCLI** is running.

    ![Screenshot of the virtual machines page with myVMPS in a running state.](../images/l10.4.1.png)

### Task 3: Execute commmands in the Cloud Shell

In this task, we will practice executing CLI commands from the Cloud Shell. 

1. From the Azure portal, open the **Azure Cloud Shell** by clicking on the icon in the top right of the Azure Portal.

1. Ensure **Bash** is selected in the upper-left drop-down menu of the Cloud Shell pane.

1. Retrieve information about the virtual machine you provisioned, including name, resource group, location, and status. Notice the PowerState is **running**.

   **Note**: Replace myRGCLI-[deployId] with  **myRGCLI-<inject key="DeploymentID" enableCopy="false" />**

    ```cli
    az vm show --resource-group myRGCLI-[deployId] --name myVMCLI --show-details --output table 
    ```
1. Stop the virtual machine. Notice the message that billing continues until the virtual machine is deallocated.
   
   **Note**: Replace myRGCLI-[deployId] with  **myRGCLI-<inject key="DeploymentID" enableCopy="false" />**

    ```cli
    az vm stop --resource-group myRGCLI-[deployId] --name myVMCLI
    ```

1. Verify your virtual machine status. The PowerState should now be **stopped**.

   **Note**: Replace myRGCLI-[deployId] with  **myRGCLI-<inject key="DeploymentID" enableCopy="false" />**

    ```cli
    az vm show --resource-group myRGCLI-[deployId] --name myVMCLI --show-details --output table 
    ```

### Task 4: Review Azure Advisor Recommendations

In this task, we will review Azure Advisor recommendations.

   **Note:** If you have completed the previous lab (Create a VM with PowerShell), then you have already performed this task. 

1. From the **Search resources,services and Docs** blade, search for and select **Advisor**.

1. On the **Advisor** blade, select **Overview**. Notice recommendations are grouped by Reliability, Security, Performance, and Cost.

    ![Screenshot of the Advisor Overview page. ](../images/l10.2.png)

    >**Note:** Depending on your resources, your recommendations will be different and you might get the notification "You are following all of our performance recommendations".

1. Select **All recommendations** from the left navigation pane and take time to view each recommendation and suggested actions.

    **Note:** Depending on your resources, your recommendations will be different and you might get the notification "You are following all of our performance recommendations".

    ![Screenshot of the Advisor All recommendations page. ](../images/l10.3.png)

1. Notice that from the **Security** option in the left navigation pane,you can download the recommendations as a CSV or PDF file.

    ![Screenshot of the Advisor All recommendations page. ](../images/l10.1.png)

1. Notice that from the **Alerts** in the left navigation pane, you can create alerts.

    >**Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
    > - Navigate to the Lab Validation page from the upper right corner of the lab guide section.
    > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
    > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
    > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

     
### Review
In this lab, you have completed:
- Configure the Cloud Shell
- Use CLI to create a virtual machine
- Execute commands in the Cloud Shell
- Review Azure Advisor Recommendations

 ## Reference link

- https://learn.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-cli
   
## You have successfully completed this lab.
