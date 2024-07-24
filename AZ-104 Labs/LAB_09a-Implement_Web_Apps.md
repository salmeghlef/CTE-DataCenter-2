---
lab:
    title: '09a - Implement Web Apps'
    module: 'Module 09 - Serverless Computing'
---

# Lab 09a - Implement Web Apps
# Student lab manual

## Lab scenario

You need to evaluate the use of Azure Web apps for hosting Contoso's web sites, hosted currently in the company's on-premises data centers. The web sites are running on Windows servers using PHP runtime stack. You also need to determine how you can implement DevOps practices by leveraging Azure web apps deployment slots.

## Objectives

In this lab, you will:

+ Task 1: Create an Azure web app
+ Task 2: Create a staging deployment slot
+ Task 3: Configure web app deployment settings
+ Task 4: Deploy code to the staging deployment slot
+ Task 5: Swap the staging slots
+ Task 6: Configure and test autoscaling of the Azure web app

## Estimated timing: 30 minutes

## Architecture diagram

![image](../media/lab09a.png)

## Instructions

### Exercise 1

#### Task 1: Create an Azure web app

In this task, you will create an Azure web app.

1. Sign in to the [**Azure portal**](http://portal.azure.com).

1. In the Azure portal, search for and select **App services**, and, on the **App Services** blade, click **+ Create**.

1. On the **Basics** tab of the **Web App** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- | ---|
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | the name of a new resource group **az104-09a-rg1** |
    | Web app name | any globally unique name |
    | Publish | **Code** |
    | Runtime stack | **PHP 7.3** |
    | Operating system | **Windows** |
    | Region | the name of an Azure region where you can provision Azure web apps |
    | App service plan | accept the default configuration |

1. Click **Review + create**. On the **Review + create** tab of the **Create Web App** blade, ensure that the validation passed and click **Create**.

    >**Note**: Wait until the web app is created before you proceed to the next task. This should take about a minute.

1. On the deployment blade, click **Go to resource**.

#### Task 2: Create a staging deployment slot

In this task, you will create a staging deployment slot.

1. On the blade of the newly deployed web app, click the **URL** link to display the default web page in a new browser tab.

1. Close the new browser tab and, back in the Azure portal, in the **Deployment** section of the web app blade, click **Add a Deployment slot**.

    >**Note**: The web app, at this point, has a single deployment slot labeled **PRODUCTION**.

1. Click **+ Add slot**, and add a new slot with the following settings:

    | Setting | Value |
    | --- | ---|
    | Name | **staging** |
    | Clone settings from | **Do not clone settings**|

1. Back on the **Deployment slots** blade of the web app, click the entry representing the newly created staging slot.

    >**Note**: This will open the blade displaying the properties of the staging slot.

1. Review the staging slot blade and note that its URL differs from the one assigned to the production slot.

#### Task 3: Configure web app deployment settings

In this task, you will configure web app deployment settings.

1. On the staging deployment slot blade, in the **Deployment** section, click **Deployment Center** and then select the **Settings** tab.

    >**Note:** Make sure you are on the staging slot blade (rather than the production slot).
    
1. On the **Settings** tab, in the **Source** drop-down list, select **Local Git** and click the **Save** button

1. On the **Deployment Center** blade, copy the **Git Clone Url** entry to Notepad.

    >**Note:** You will need the Git Clone Url value in the next task of this lab.

1. On the **Deployment Center** blade, select the **Local Git/FTPS credentials** tab, in the **User Scope** section, specify the following settings, and click **Save**.

    | Setting | Value |
    | --- | ---|
    | User name | any globally unique name (must not contain `@` character) |
    | Password | any password that satisfies complexity requirements|

    >**Note:** The password must be at least eight characters long, with two of the following three elements: letters, numbers, and non-alphanumeric characters.

    >**Note:** You will need these credentials in the next task of this lab.



In this task, you will swap the staging slot with the production slot

1. Navigate back to the blade displaying the production slot of the web app.

1. In the **Deployment** section, click **Deployment slots** and then, click **Swap** toolbar icon.

1. On the **Swap** blade, review the default settings and click **Swap**.

1. Click **Overview** on the production slot blade of the web app and then click the **URL** link to display the web site home page in a new browser tab.

1. Verify the default web page has been replaced with the **Hello World!** page.



    >**Note**: You also have the option of scaling the web app manually.

1. Leave the default option **Scale based on a metric** selected and click **+ Add a rule**

1. On the **Scale rule** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- |--- |
    | Metric source | **Current resource** |
    | Time aggregation | **Maximum** |
    | Metric namespace | **App Service plans standard metrics** |
    | Metric name | **CPU Percentage** |
    | Operator | **Greater than** |
    | Metric threshold to trigger scale action | **10** |
    | Duration (in minutes) | **1** |
    | Time grain statistic | **Maximum** |
    | Operation | **Increase count by** |
    | Instance count | **1** |
    | Cool down (minutes) | **5** |

    >**Note**: Obviously these values do not represent a realistic configuration, since their purpose is to trigger autoscaling as soon as possible, without extended wait period.

1. Click **Add** and, back on the App Service plan scaling blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- |--- |
    | Instance limits Minimum | **1** |
    | Instance limits Maximum | **2** |
    | Instance limits Default | **1** |

1. Click **Save**.
#### Clean up resources

   >**Note**: Remember to remove any newly created Azure resources that you no longer use. Removing unused resources ensures you will not see unexpected charges.

1. In the Azure portal, open the **PowerShell** session within the **Cloud Shell** pane.

1. List all resource groups created throughout the labs of this module by running the following command:

#### Review

In this lab, you have:

+ Created an Azure web app
+ Created a staging deployment slot
+ Configured web app deployment settings
+ Deployed code to the staging deployment slot
+ Swapped the staging slots
+ Configured and test autoscaling of the Azure web app
