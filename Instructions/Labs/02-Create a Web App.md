# Lab 02 - Create a Web App

## Lab overview

Azure App Service is a fully managed web application hosting platform. This platform as a service (PaaS) offered by Azure. 
Azure App Service is actually a collection of four services, all of which are built to help you host and run web applications. The four services (Web Apps, Mobile Apps, API Apps, and Logic Apps) look different, but in the end they all operate in very similar ways. Web Apps are the most commonly used of the four services, and this is the service that we will be using in this lab.

In this walkthrough, we will create a new web app that runs a Docker container. 

## Lab objectives

In this lab, you will complete the following tasks:

+ Task 1: Create a Web App
+ Task 2: Test the Web App

## Estimated timing: 20 minutes

## Architecture diagram

![](../images/az900lab02.PNG) 

### Task 1: Create a Web App
In this task, you will create an Azure App Service Web App.

1. On Azure Portal page, in Search resources, services and docs (G+/) box at the top of the portal, enter **App Service (1)**, and then select **App Services (2)** under services.

   ![](../images/lab2-image1.png) 

1. On **App Services** blade, click **+ Create (1)** then from dropdown select **+ Web App (2)**.

   ![](../images/lab2-image2.png) 

1. On the **Basics** tab of the **Create Web App** blade, specify the following and click **Next > Database (7)**.
 
    | Setting | Value |
    | -- | -- |
    | Subscription | **Accept default subscription (1)** |
    | Resource Group | **myRGWebApp1-<inject key="DeploymentID" enableCopy="false"/>(2)**  |
    | Name | **myDockerWebApp<inject key="DeploymentID" enableCopy="false"/> (3)** |
    | Publish | **Docker Container (4)** |
    | Operating System | **Linux (5)** |
    | Region | **<inject key="Region" enableCopy="false"/>** **(6)** (ignore any service plan availability warnings) |
    |||

    ![](../images/lab2-image3.png)

   
1. **Database** tab, accept default settings and click on Click **Next > Docker** tab. 

1. On **Docker** tab specify the following to configure the container information. The startup command is optional and not needed in this exercise and click **Review + create (5)**.

    | Setting | Value |
    | -- | -- |
    | Options | **Single container (1)** |
    | Image Source | **Docker Hub (2)** |
    | Access Type | **Public (3)** |
    | Image and tag | **mcr.microsoft.com/azuredocs/aci-helloworld (4)** |
    |||

   ![](../images/lab2-image4.png)


   **Note:** This is same container that was used in the Container Instances walkthrough to display a hello world message.

1. Once validation is passed click **Create**.

### Task 2: Test the Web App

In this task, we will test the web app.

1. Wait for the Web App to deploy. Once deployemnt got success click **Go to resource**.

   ![](../images/lab2-image5.png)

1. On the **Overview** blade, locate  the **Default Domain** entry.

     ![](../images/lab2-image6.png)

1. Copy the URL and paste it into a new browser tab to observe the "Welcome to Azure Container Instances!" page.

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

## Reference link

https://azure.microsoft.com/en-us/products/app-service/?ref=jimmybogard.com

https://learn.microsoft.com/en-us/training/modules/host-a-web-app-with-azure-app-service/

## You have successfully completed this lab.
