# Lab 14 - Manage access with RBAC

### Lab overview

In this walkthrough, we will assign roles and view activity logs.

## Lab objectives

In this lab, you will complete the following tasks:

+ Task 1: View and assign roles
+ Task 2: Monitor role assignments and remove a role

## Estimated timing: 15 minutes

## Architecture diagram

![](../images/az900lab14.png)

### Task 1: View and assign roles

In this task, we will assign the Virtual machine contributor role. 

1. On the Azure portal, from the **Search resources, services, and docs** blade, search for and select **Resource groups**

   ![image](../images/lab14-image1.png)

1. Then view and select the existing resource group **myRGRBAC-<inject key="DeploymentID" enableCopy="false"/>**.

   ![image](../images/lab14-image2.png)
     
1. You will be directed to the overview page of the resource group

1. Click on the **Access control (IAM)** blade, and then switch to the **Roles** tab. Scroll down and notice roles definitions that are available. Use the View link under details to get an idea of each role's permissions. Notice there is also information on the number of users and groups that are assigned to each role.

   ![image](../images/lab14-image3.png)

1. On the **myRGRBAC-<inject key="DeploymentID" enableCopy="false"/> | Access control (IAM)** blade select **+ Add** then from drop-down select **Add Role assignments**. 

   ![image](../images/lab14-image4.png)
   
1. In  **Add Role assignments** blade on the **Role** tab, Search for the **Virtual Machine Contributor** role and select **Virtual Machine Contributor** then click on **Next**

    ![image](../images/lab14-image5.png)
   
1. On **Members** tab ensure **Assign access to**: **the user, group, or service principal** is selected. Then click **+ Select members** popup window will open in search bar enter your azure account name (Username: <inject key="AzureAdUserEmail"></inject>) click **select**. 

    ![image](../images/lab14-image6.png)

1. Click **Review + Assign**.

   ![image](../images/lab14-image7.png)
   
     **Note:** The Virtual machine contributor role lets you manage virtual machines, but not access their operating system or manage the virtual network and storage account they are connected to. User name can be obtained from the Lab Environment output page

1. Back on **myRGRBAC-<inject key="DeploymentID" enableCopy="false"/> | Access control (IAM)** blade, select **Role assignments** tab.

    ![image](../images/lab14-image8.png)

1. **Refresh** the Role assignments page and ensure you are now listed as a Virtual machine contributor.

     ![image](../images/lab14-image9.png)

    **Note**: This assignment does not grant you any additional privileges, since your account has already the Owner role, which includes all privileges associated with the Contributor role.

### Task 2: Monitor role assignments and remove a role

In this task, we will view the activity log to verify the role assignment, and then remove the role. 

1. On the myRGRBAC-<inject key="DeploymentID" enableCopy="false"/> resource group blade, click **Activity log**.

1. On the myRGRBAC-<inject key="DeploymentID" enableCopy="false"/> | Activity log blade, click **Add filter**.

    ![image](../images/lab14-image10.png)

5. From the **Resource (1)** drop-down, select **Operation (2)**, and then from **Selected (3)** drop-down search for **Create role assignment (4)** and select **Create role assignment (microsoft.Authorization/roleAssignments/write) (5)**

    ![image](../images/lab14-image11.png)

    ![image](../images/lab14-image12.png)

1. Verify the Activity log shows your role assignment. (With your User Id). 

     ![image](../images/lab14-image13.png)
   
    **Note**: Can you figure out how to remove your role assignment?

   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
   > - Click Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation tab.
   > - Hit the Validate button for the corresponding task.
   > - If you receive a success message, you can proceed to the next task. If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.
 
### Review
In this lab, you have completed:
- View and assign roles
- Monitor role assignments and remove a role
  
## You have successfully completed this lab.
