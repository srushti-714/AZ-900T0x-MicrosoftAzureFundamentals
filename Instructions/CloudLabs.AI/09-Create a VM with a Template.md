# 09 - Create a VM with a Template

In this walkthrough, we will deploy a virtual machine with a QuickStart template and examine monitoring capabilities.

# Task 1: Explore the gallery and locate a template

In this task, we will browse the Azure QuickStart gallery and deploy a template that creates a virtual machine. 

1. Double click on the Microsoft Edge icon in the VM desktop to open browser

2. In a new tab, access the [Azure Quickstart Templates gallery](https://azure.microsoft.com/resources/templates?azure-portal=true). In the gallery you will find a number of popular and recently updated templates. These templates automate deployment of Azure resources, including installation of popular software packages.

3. Browse through the many different types of templates that are available. 

    **Note**: Are there are any templates that are of interest to you?

4. Search for or directly access the [Deploy a Virtual Machine ](https://azure.microsoft.com/resources/templates/101-vm-simple-windows?azure-portal=true) template.

    **Note**: The **Deploy to Azure** button enables you to deploy the template via the Azure portal. During such deployment, you will be prompted only for small set of configuration parameters. 

5. Click the **Deploy to Azure** button. Your browser session will be automatically redirected to the [Azure portal](http://portal.azure.com/).

6. If prompted, sign in to the Azure with the Azure credentials from the Lab Environment output page.

7. Click **Edit template**. The Resource Manager template format uses the JSON format. Review the parameters and variables.  Then locate the parameter for virtual machine name. Change the name to **myVMTemplate**. **Save** your changes. You are returned to the **Custom deployment** blade in the Azure portal.

    ![Screenshot of the template with the VM name change highlilghted.](../images/0901.png)

8. On the **Custom deployment** blade configure the parameters required by the template (replace ***xxxx*** in the DNS label prefix with DeploymentID). Leave the defaults for everything else. 

    | Setting| Value|
    |----|----|
    | Subscription | **Choose your subscription**|
    | Resource group | **myRGTemplate-[DeploymentID]** (use existing) |
    | Location | **(US) East US** |
    | Admin username | **azureuser** |
    | Admin password | **Pa$$w0rd1234** |
    | DNS label prefix | **myvmtemplate*xxxx*** |
    | Windows OS version | **2019-Datacenter** |
    | | |
    
    **Note**: Deployment ID can be obtained from the Lab Environment output page. There is no cost associated with this template.

9. Click **Review + Create**.

10. Monitor your deployment. 

# Task 2: Verify and monitor your virtual machine deployment

In this task, we will verify the virtual machine deployed correctly. 

1. From the **All services** blade, search for and select **Virtual machines**.

2. Ensure your new virtual machine was created. 

    ![Screenshot of the virtual machines page. The new VM is shown and running.](../images/0902.png)

3. Select your virtual machine and on the **Overview** pane scroll down to view monitoring data.

    **Note**: The monitoring timeframe can be adjusted from one hour to 30 days.

4. Review different charts that are provided including **CPU (average)**, **Network (total)**, and **Disk bytes (total)**. 

    ![Screenshot of the virtual machine monitoring charts.](../images/0903.png)

5. Click on any chart. Note that you can **Add metric** and change the chart type.

6. Return to the **Overview** blade.

7. Click on the **Activity log** (left pane). Activity logs record such events as creation or modification of resources. 

8. Click **Add filter**, and experiment with searching for different event types and operations. 

    ![Screenshot of the Add filters page with Event type selected.](../images/0904.png)


