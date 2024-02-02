# Lab 04 - Create a virtual network

## Lab overview

In this walkthrough, we will create a virtual network, deploy two virtual machines onto that virtual network and then configure them to allow one virtual machine to ping the other within that virtual network.

## Lab objectives

In this lab, you will complete the following tasks:

+ Task 1: Create a virtual network
+ Task 2: Create two virtual machines
+ Task 3: Test the connection

## Estimated timing: 20 minutes

## Architecture diagram

![](../images/az900lab04.PNG) 

### Task 1: Create a virtual network

In this task, we will create a virtual network. 

1. On Azure Portal page, in **Search resources, services and docs (G+/)** box at the top of the portal, enter **Virtual networks**, and then select **Virtual networks** under services.

1. On **Create virtual network** blade, click **+ Create**. 

1. On the **Create virtual network** blade, fill in the following (leave the defaults for everything else):

      | Setting | Value | 
      | ---     | ---   |
      | Name    | **vnet1** |
      | Subscription | **Choose your subscription**  |
      | Resource group |  **myRGVNet-<inject key="DeploymentID" enableCopy="false"/>** |
      | Location | **(US) East US** |

      ![Screenshot of the "Basic" step of Create virtual network blade with the default fields.](../images/0301a.png)

1. On the **Create virtual network** blade,click **Next** twice to go to the IP Addresses tab and delete precreated IP address and click on **Add IPV4 address** to create a new address space.

    | Setting | Value | 
    | --- | --- |
    | Address space |**10.1.0.0/16**|
 
 1. Click on **+ Add Subnet** and ensure if the following address is reflecting (Delete if any subnet exists already with the name default) if you have made any changed then click on **Add**.
  
    | Setting | Value | 
    | --- | --- |
    | Subnet Name |**default**|
    | Subnet Address range | **10.1.0.0/24**|
  
    ![Screenshot of the "IP Addresses" step of Create virtual network blade with the default fields.](../images/vnetnow.png)

1. Click the **Review + create** button. Ensure the validation passes.

1. Click the **Create** button to deploy the virtual network. 
    
### Task 2: Create two virtual machines

In this task, we will create two virtual machines in the virtual network. 

1. From the **Search resources, Services, and docs(G+/)** blade, search for **Virtual machines** and then click **+ Create** and choose **Azure virtual machine**.

1. On the **Basics** tab, fill in the following information (leave the defaults for everything else):

   | Setting | Value | 
   | --- | --- |
   | Subscription | **Use default supplied**  |
   | Resource group |  **myRGVNet-<inject key="DeploymentID" enableCopy="false"/>** |
   | Virtual machine name | **vm1**|
   | Region | **(US) East US** |
   | Image | **Windows Server 2019 Datacenter -Gen2** |
   | Username| **azureuser** |
   | Password| **Pa$$w0rd1234** |
   | Public inbound ports| Select **Allow selected ports**  |
   | Selected inbound ports| **RDP (3389)** |

1. Click **Next** to switch to the **Disks** tab and in the **OS Disk type** select **Standard HDD** from the dropdown and leave everything else as default and click **Next**. 

   ![Screenshot of the virtual machine properties with the Connect button highlighted.](../images/hdd.png)


1. In **Networking** tab, make sure the virtual machine is placed in the vnet1 virtual network. Review the default settings, but do not make any other changes. 

   | Setting | Value | 
   | --- | --- |
   | Virtual network | **vnet1** |

1. Click **Review + create**. After the Validation passes, click **Create**. Deployment times can vary but it can generally take between three to six minutes to deploy.

1. Monitor your deployment, but continue on to the next step. 

1. Create a second virtual machine by repeating steps **1 to 5** above from the task 2. Make sure you use a different virtual machine name as given below, and also the virtual machine is within the same virtual network, and is using a new public IP address: 

    | Setting | Value |
    | --- | --- |
    | Resource group | **myRGVNet-<inject key="DeploymentID" enableCopy="false"/>** |
    | Virtual machine name |  **vm2** |
    | Virtual network | **vnet1** |
    | Public IP | (new) **vm2-ip** |

1. Wait for both virtual machines to deploy. 

### Task 3: Test the connection 

In this task, we will try to test whether the virtual machines can communicate (ping) each other. 

1. From the **All resources** blade, search for **vm1**, open its **Overview** blade, and make sure its **Status** is **Running**. You may need to **Refresh** the page.

1. On the virtual machine **Overview** blade, click the **Connect** button and choose the **Connect** from the dropdown.

    ![Screenshot of the virtual machine properties with the Connect button highlighted.](../images/conrdp.png)

    >**Note**: The following directions tell you how to connect to your VM from a Windows computer. On a Mac, you need an RDP client such as this Remote Desktop Client from the Mac App Store and on a Linux computer you can use an open source RDP client.

1. Within the **Connect** page, click on **Download RDP File**.

   ![Screenshot of the virtual machine properties with the Connect button highlighted. ](../images/downrdp.png)

1. Once the file is downloaded,you will be directed with a warning, click on **Keep**.

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
   
   >**Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
    > - Navigate to the Lab Validation page from the upper right corner of the lab guide section.
    > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
    > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
    > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

### Review
In this lab, you have completed:
- Create a virtual network
- Create two virtual machines
- Test the connection
 
## You have successfully completed this lab.
