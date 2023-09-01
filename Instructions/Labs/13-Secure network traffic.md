# Lab 13 - Secure network traffic

## Lab overview

In this walkthrough, we will configure a network security group.

## Lab objectives

In this lab, you will complete the following tasks:

+ Task 1: Create a virtual machine
+ Task 2: Create a network security group
+ Task 3: Configure an inbound security port rule to allow RDP
+ Task 4: Configure an outbound security port rule to deny Internet access
  
## Estimated timing: 45 minutes

## Architecture diagram

![](../images/az900lab13.png)

### Task 1: Create a virtual machine 

In this task, we will create a Windows Server 2019 Datacenter virtual machine. 

1. Click on the Azure Portal icon on the VM desktop.

1. From the **Search resources, services, and docs** blade, search for and select **Virtual machines**, and then click **+ Create** then select Azure Virtual machines.

1. On the **Basics** tab, fill in the following information (leave the defaults for everything else):

    | Settings | Values |
    |  -- | -- |
    | Subscription | **Choose your subscription**|
    | Resource group | **myRGSecure-<inject key="DeploymentID" enableCopy="false"/>** (use existing) |
    | Virtual machine name | **SimpleWinVM** |
    | Location | **(US) East US**|
    | Availability option | **No infrastructure redundancy required** |
    | Image | **Windows Server 2019 Datacenter Gen 2**|
    | Size | **Standard D2s v3**|
    | Administrator account username | **azureuser** |
    | Administrator account password | **Pa$$w0rd1234**|
    | Inbound port rules | **None**|
    | | |

1. Switch to the **Networking** tab, and configure the following setting:

    | Settings | Values |
    | -- | -- |
    | NIC network security group | **None**|
    | | |

1. Switch to the **Monitoring** tab, select the following setting:

    | Settings | Values |
    | -- | -- |
    | Boot diagnostics | **Disable**|
    | | |

1. Leave the remaining defaults and then click the **Review + create** button at the bottom of the page.

1. Once Validation is passed click the **Create** button. It can take about five minutes to deploy the virtual machine.

1. Monitor the deployment. It may take a few minutes for the resource group and virtual machine to be created. 

1. From the deployment blade or from the Notification area, click **Go to resource**. 

1. On the **SimpleWinVM** virtual machine blade, click **Networking**, review the **Inbound port rules** tab, and note that there is no network security group associated with the network interface of the virtual machine or the subnet to which the network interface is attached.

    **Note**: Identify the name of the network interface. You will need it in the next task.

### Task 2: Create a network security group

In this task, we will create a network security group and associate it with the network interface.

1. From the **Search resources, services, and docs** blade, search for and select **Network security groups** and then click **+ create**

1. On the **Basics** tab of the **Create network security group** blade, replace DeploymentId which is in environment details, specify the following settings.

    | Setting | Value |
    | -- | -- |
    | Subscription | **Choose your subscription** |
    | Resource group | **myRGSecure<inject key="DeploymentID" enableCopy="false"/>** |
    | Name | **myNSGSecure** |
    | Region | **(US) East US**  |
    | | |

1. Click **Review + create** and then after the validation click **Create**.

1. After the NSG is created, click **Go to resource**.

1. Under **Settings** click **Network interfaces** and then **Associate**.

1. Select the **network interface** you identified in the previous task, and then Click **Ok**. 

### Task 3: Configure an inbound security port rule to allow RDP

In this task, we will allow RDP traffic to the virtual machine by configuring an inbound security port rule. 

1. In the Azure portal, navigate to the blade of the **SimpleWinVM** virtual machine. 

1. On the **Overview** pane, click **Connect > RDP > Download the RDP file > Run that file**.

1. Attempt to connect to the virtual machine using RDP. By default the network security group does not allow RDP. Close the error window. 

    ![Screenshot of the error message that the virtual machine connection has failed.](../images/1201.png)

1. On the virtual machine blade, scroll down to the **Settings** section, click on **Networking**, and notice the inbound rules for the **myNSGSecure (attached to network interface: simplewinvm<inject key="Deployment-id" enableCopy="false"/>)** network security group deny all inbound traffic except traffic within the virtual network and load balancer probes.

1. On the **Inbound port rules** tab, click **Add inbound port rule** . Click **Add** when you are done. 

    | Setting | Value |
    | -- | -- |
    | Source | **Any**|
    | Source port ranges | **\*** |
    | Destination | **Any** |
    | Destination port ranges | **3389** |
    | Protocol | **TCP** |
    | Action | **Allow** |
    | Priority | **300** |
    | Name | **AllowRDP** |
    | | |

1. Wait for the rule to be provisioned and then try again to RDP into the virtual machine. This time you should be successful. Remember the user is **azureuser** and the password is **Pa$$w0rd1234**.

### Task 4: Configure an outbound security port rule to deny Internet access

In this task, we will create a NSG outbound port rule that will deny Internet access and then test to ensure the rule is working.

1. Continue in your virtual machine RDP session. If pop-up comes then select **yes**.

1. After the machine starts, open an **Internet Explorer** browser, then click on **Ok**. 

1. Verify that you can access **https://www.bing.com** , click **OK** if pop-up comes, and then close Internet Explorer. You will need to work through the IE enhanced security pop-ups. 

    **Note**: We will now configure a rule to deny outbound internet access. 

1. In the Azure portal, navigate back to the blade of the **SimpleWinVM** virtual machine. 

1. Under **Settings**, click **Networking**, and then **Outbound port rules**.

1. Notice there is a rule, **AllowInternetOutbound**. This a default rule and cannot be removed. 

1. Click **Add outbound port rule** to the right of the **myNSGSecure  (attached to network interface: simplewinvm<inject key="DeploymentID" enableCopy="false"/>)** network security group and configure a new outbound security rule with a higher priority that will deny internet traffic. Click **Add** when you are finished. 

    | Setting | Value |
    | -- | -- |
    | Source | **Any**|
    | Source port ranges | **\*** |
    | Destination | **Service Tag** |
    | Destination service tag | **Internet** |
    | Destination port ranges | **\*** |
    | Protocol | **TCP** |
    | Action | **Deny** |
    | Priority | **4000** |
    | Name | **DenyInternet** |
    | | |

1. Return to your RDP session. 

1. Browse to **https://www.microsoft.com**. The page should not display. You may need to work through additional IE enhanced security pop-ups.  

   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
   > - Click Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation tab.
   > - Hit the Validate button for the corresponding task.
   > - If you receive a success message, you can proceed to the next task. If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

### Review
In this lab, you have completed:
- Create a virtual machine
- Create a network security group
- Configure an inbound security port rule to allow RDP
- Configure an outbound security port rule to deny Internet access
  
## You have successfully completed this lab.
