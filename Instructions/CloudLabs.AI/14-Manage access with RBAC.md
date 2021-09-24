# 14 - Manage access with RBAC

In this walkthrough, we will assign roles and view activity logs. 

# Task 1: View and assign roles

In this task, we will assign the Virtual machine contributor role. 

1. Click on the Azure Portal icon on the VM desktop and login with the Azure credentials from the Lab Environment output page.

2. From the **All services** blade, search for and select **Resource groups**

3. Then view the existing resource group. 

    | Setting | Value |
    | -- | -- |
    | Resource group | **myRGRBAC-[DeploymentId]** |
    | | |
    
    **Note**: Deployment ID can be obtained from the Lab Environment output page.

4. Click on the existing resource group

5. You will be directed to the overview page of the resource group

6. Click on the **Access control (IAM)** blade, and then switch to the **Roles** tab. Scroll through the large number of roles definitions that are available. Use the Informational icons to get an idea of each role's permissions. Notice there is also information on the number of users and groups that are assigned to each role.

    ![Screenshot of IAM roles blade. Owner, contributor, and reader roles are shown.](../images/1501.png)

7. Switch to the **Role assignments** tab of the **myRGRBAC-[DeploymentId] - Access control (IAM)** blade, click **+ Add** and then click **Add role assignment**. Assign the Virtual Machine Contributor role to your user account, then click **Save**. 

    | Setting | Value |
    | -- | -- |
    | Role | **Virtual machine contributor** |
    | Assign access to | **user, group, or service principal** |
    | Select | your user account |
    | | |

    **Note:** The Virtual machine contributor role lets you manage virtual machines, but not access their operating system or manage the virtual network and storage account they are connected to. User name can be obtained from the Lab Environment output page

    ![Screenshot of the Add role assignment page filled out with the necessary information.](../images/1502.png)

8. **Refresh** the Role assignments page and ensure you are now listed as a Virtual machine contributor. 

    **Note**: This assignment does not actually grant you any additional provileges, since your account has already the Owner role, which includes all privilges associated with the Contributor role.

# Task 2: Monitor role assignments and remove a role

In this task, we will view the activity log to verify the role assignment, and then remove the role. 

1. On the myRGRBAC-[DeploymentId] resource group blade, click **Activity log**.

2. Click **Add filter**, select **Operation**, and then **Create role assignment**.

    ![Screenshot of the Activity log page with configured filter.](../images/1503.png)

3. Verify the Activity log shows your role assignment.(With your ODL Id). 

    **Note**: Can you figure out how to remove your role assignment?

Congratulations! You have assigned roles and viewed activity logs. 



