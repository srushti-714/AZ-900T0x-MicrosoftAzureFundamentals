# Lab 02 - Create a Web App

## Lab overview

In this walkthrough, we will create a new web app that runs a Docker container. The container displays a Welcome message.

## Lab objectives

In this lab, you will complete the following tasks:

+ Task 1: Create a Web App
+ Task 2: Test the Web App

## Estimated timing: 20 minutes

## Architecture diagram

![](../images/az900lab02.PNG) 

### Task 1: Create a Web App

Azure App Service is actually a collection of four services, all of which are built to help you host and run web applications. The four services (Web Apps, Mobile Apps, API Apps, and Logic Apps) look different, but in the end they all operate in very similar ways. Web Apps are the most commonly used of the four services, and this is the service that we will be using in this lab.

In this task, you will create an Azure App Service Web App.

1. On the Azure portal, from the **Search resources, Services, and docs(G+/)** blade, search for and select **App Services**.

   ![](../images/lab2-image1.png) 

1. Click **+ Create** then from dropdown select **+ Web App**.

   ![](../images/lab2-image2.png) 

1. On the **Basics** tab of the **Create Web App** blade.

    **Note:**  **DeploymentId** can be obtained from the Lab Environment output page.

    | Setting | Value |
    | -- | -- |
    | Subscription | **Choose your subscription** |
    | Resource Group | **myRGWebApp1-<inject key="DeploymentID" enableCopy="false"/>**  |
    | Name | **myDockerWebApp<inject key="DeploymentID" enableCopy="false"/>** |
    | Publish | **Docker Container** |
    | Operating System | **Linux** |
    | Region | **East US** (ignore any service plan availability warnings) |
    |||

    ![](../images/lab2-image3.png)

   
1. Click **Next > Database** tab, accept default settings and click on Click **Next > Docker** tab. 
1. On **Docker** tab and configure the container information. The startup command is optional and not needed in this exercise.

    **Note:** This is same container that was used in the Container Instances walkthrough to display a hello world message.

    | Setting | Value |
    | -- | -- |
    | Options | **Single container** |
    | Image Source | **Docker Hub** |
    | Access Type | **Public** |
    | Image and tag | **mcr.microsoft.com/azuredocs/aci-helloworld** |
    |||

   ![](../images/lab2-image4.png)
   
1. Click **Review + create**, and then click **Create**.

### Task 2: Test the Web App

In this task, we will test the web app.

1. Wait for the Web App to deploy. Once deployemnt got success click **Go to resource**.

   ![](../images/lab2-image5.png)

1. On the **Overview** blade, locate the **Default Domain** entry.

     ![](../images/lab2-image6.png)

1. Click on the **URL** to open the new browser tab and display the Welcome to Azure Container Instances page.

    ![](../images/lab2-image7.png)

1. Switch back to the **Overview** blade of your web app and select Monitoring tab note that it includes several charts. If you repeat step 4 a few times, you should be able to see corresponding telemetry being displayed in the charts. This includes number of requests and average response time.

      ![](../images/lab2-image8.png)

   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
   > - Click Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation tab.
   > - Hit the Validate button for the corresponding task.
   > - If you receive a success message, you can proceed to the next task. If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

### Review
In this lab, you have completed:
- Create a Web App
- Test the Web App
  
## You have successfully completed this lab.
