
# Microsoft

# Asset Monitoring Solution

**Table of Contents** 

- [1 About Asset Monitoring Solution](#1-about-asset-monitoring-solution)
- [2 Architecture](#2-architecture)
   - [2.1 Data Flow Architecture Diagram](#21-data-flow-architecture-diagram)
- [3 Azure Services](#3-azure-services)
   - [3.1 Azure Blob](#31-azure-blob)
   - [3.2 Azure IoT HUB](#32-azure-iot-hub)
   - [3.3 Azure Web App](#33-azure-web-app)
   - [3.4 Azure Web Job](#34-azure-web-job)
   - [3.5 Azure SQL DB](#35-azure-sql-db)
   - [3.6 Azure DocumentDB](#36-azure-documentdb)
   - [3.7 Azure Event hub](#37-azure-event-hub)
- [4 Deployment Costs](#4-deployment-costs)
- [5 Prerequisites for Deploying ARM Template](#5-prerequisites-for-deploying-arm-template)
   - [5.1 Azure B2C Tenant Creation and Configuration](#51-azure-b2c-tenant-creation-and-configuration)
   - [5.2 Power BI Configuration](#52-power-bi-configuration)
   - [5.3 Creating an Azure Service Principal](#53-creating-an-azure-service-principal)
- [6 ARM Template Input Parameters](#6-arm-template-input-parameters)
- [7 Getting Started](#7-getting-started)
    - [7.1 Deploying the ARM Template](#71-deploying-the-arm-template)
- [8 Prerequisites for Gateway-Middleware](#8-prerequisites-for-gateway-middleware)
- [9 Step 1 Run the Zadig file](#9-step-1-run-the-zadig-file)
- [10 Step 2 Setup GatewayMiddleware package](#10-step-2-setup-gatewaymiddleware-package)
- [11 Step 3 Configuring WEBAPP](#11-step-3-configuring-webapp)
- [12 Step 4 Adding the pre-requisites in the web app](#12-step-4-adding-the-pre-requisites-in-the-web-app)
    - [12.1 Adding Gateway](#121-adding-gateway)
    - [12.2 Adding Sensor](#122-adding-sensor)
    - [12.3 Adding Asset to Web App using Mobile Application](#123-adding-asset-to-web-app-using-mobile-application)
    - [12.4 Adding Assets to a Group](#124-adding-assets-to-a-group)
    - [12.5 Cofiguring the PoweBi Desktop App and Publishing](#125-cofiguring-the-powebi-desktop-app-and-publishing)
    - [12.6 Configuring the flow in web app](#126-configuring-the-flow-in-web-app)
- [13 Step 5 Running the gateway middleware](#13-step-5-running-the-gateway-middleware)
    - [13.1 Validating data in iot hub and Node server](#131-validating-data-in-iot-hub-and-node-server)
- [14 Step 6 validating the data in web app](#14-step-6-validating-the-data-in-web-app)
- [15 Step 7 Creating and validating the rule in Web app](#15-step-7-creating-and-validating-the-rule-in-web-app)
- [16 Step 8 Configuring the Indoor map in web app](#16-step-8-configuring-the-indoor-map-in-web-app)
    - [16.1 Adding gateway rule](#161-adding-sensor)
    - [16.2 Positioning the gateway on the layout](#162-positioning-the-gateway-on-the-layout)
    - [16.3 Indoor alert notification](#163-indoor-alert-notification)
    - [16.4 Alerts checking](#164-alerts-checking)
    - [16.5 Asset Status](#165-asset-status)
	

## 1 About Asset Monitoring Solution

Asset Monitoring and Tracking Solution is a complete smart inventory management tool. The solution provides a web dashboard & a mobile application to Monitor, Locate and Report all the remote assets so that they are completely visible 24x7.

## 2 Architecture

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/1.jpg)

## 2.1 Data Flow Architecture Diagram

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/2.jpg)

## 3 Azure Services

### 3.1 Azure Blob

The word ‘Blob’ expands to Binary Large Object. Blobs include images, text files, videos and audios. There are three types of blobs in the service offered by Windows Azure namely block, append and page blobs. 
  **Block blobs** are collection of individual blocks with unique block ID. The block blobs allow the users to upload large amount of data. 
  **Append blobs** are optimized blocks that helps in making the operations efficient. 
  **Page blobs** are compilation of pages. They allow random read and write operations. While creating a blob, if the type is not specified they are set to block type by default. 
All the blobs must be inside a container in your storage.  

### 3.2 Azure IoT Hub

Azure IoT HUB is a fully managed service that enables reliable and secure bidirectional communications between millions of IoT devices and a solution back end.  
	-Provides multiple device-to-cloud and cloud-to-device communication options. These options include one-way messaging, file transfer, and request-reply methods. 
	-Provides built-in declarative message routing to other Azure services. 
	-Provides a query able store for device metadata and synchronized state information. 
	-Enables secure communications and access control using per-device security keys.  
 	-Provides extensive monitoring for device connectivity and device identity management events. 
	-Includes device libraries for the most popular languages and platforms.
	
### 3.3 Azure Web App 

Azure Web Apps enables you to build and host web applications in the programming language of your choice without managing infrastructure. It offers auto-scaling and high availability, supports both Windows and Linux, and enables automated deployments from GitHub, Visual Studio Team Services. 

### 3.4 Azure Web Job 

Azure Web Job is back-end program you can run inside Azure, without Azure Web Job, you can deploy windows console app or windows service app to your server, then setup scheduler via windows scheduler or other third-party windows scheduler tools.  

### 3.5 Azure SQL DB 

Azure SQL Database is a relational database-as-a service using the Microsoft SQL Server Engine. SQL Database is a high-performance, reliable, and secure database you can use to build data-driven applications and websites in the programming language of your choice, without needing to manage infrastructure. 

### 3.6 Azure DocumentDB 
Azure DocumentDB is a general-purpose NoSQL database that is used in a wide range of applications and use cases. It is a good choice for any application that needs low order-of-millisecond response times, and needs to scale rapidly. 
Azure Event hub 

### 3.7 Azure Event Hub
Azure Event Hubs is a highly scalable data streaming platform and event ingestion service, capable of receiving and processing millions of events per second. Event Hubs can process and store events, data, or telemetry produced by distributed software and devices. Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters. 

## 4 Deployment Costs 
Below table describes the deployment costs per month for the solution.

**Region-US West**

**Deployment Costs for Type1**

| **Resource Name**                               | **Size**                                                                                                    | **Resource costing model**    | **Azure Cost/month**                                                                                                                
| -------------                                   | -------------                                                                                               | --------------------          | ------------                                                                                                             
| **App Service Plan(3 web apps + 1 web job)**    | F1 (Free Tier), Shared Cores, 1 GB RAM, 1GB Storage                                                         | PAYG                          | $0.00   
| **SQL Database**                                | B1 (Standard tier), 5DTU, 2GB included storage per DB                                                       | PAYG                          | $4.90  
| **IoT HUB**                                     | F1 (Free Tier), 500 devices, 8000 messages/day                                                              | PAYG                          | $0.00  
| **Log Analytics (Optional)**                    | First 5GB of data storage is free.                                                                          | PAYG                          | $2.30 
| **Application Insights (Optional)**             | Basic, 1GB * $2.30 Region: East US                                                                          | PAYG                          | $2.30   
| **Storage Account**                             | Block Blob Storage, General Purpose V1, LRS,100 GB Capacity                                                 | PAYG                          | $2.40
| **Event Hub**                                   | Basic, throughput units 20,1MB/sec ingress events, 2MB/sec egress events.                                   | PAYG                          | $0.75
| **Cosmos DB**                                   | Standard, throuput 2500 RU/s (Request Units per second) 25 x100 Rus(Throughput)- $146 1 GB storage – $0.25  | PAYG                          | $146.25
| **Stream Analytics**                            | Standard Streaming Unit, 3 unit(s) 3 * $80.30 Region: East US                                               | PAYG                          | $240.9
| **Total Cost**                                  |                                                                                                             |                               | $395.2
| **Total Cost Including Optional Components**    |                                                                                                             |                               | $399.8

**Deployment Costs for Type2**

| **Resource Name**                               | **Size**                                                                                                    | **Resource costing model**    | **Azure Cost/month**                                                                                                               
| -------------                                   | -------------                                                                                               | --------------------          | ------------                                                                                                             
| **App Service Plan(3 web apps + 1 web job)**    | B1 (1 core,1.75 GB RAM, 10GB Storage)                                                                       | PAYG                          | $54.75   
| **SQL Database**                                | B1 (Standard tier), 5DTU, 2GB included storage per DB                                                       | PAYG                          | $4.90  
| **IoT HUB**                                     | S1, Unlimited devices, 1 Unit-$25 400,000 messages/day                                                      | PAYG                          | $25.00  
| **Log Analytics (Optional)**                    | First 5GB of data storage is free.Per GB(Standalone) Region East US                                         | PAYG                          | $2.30 
| **Application Insights (Optional)**             | Basic, 1GB * $2.30 Region: East US                                                                          | PAYG                          | $2.30   
| **Storage Account**                             | Block Blob Storage, General Purpose V1, LRS,100 GB Capacity                                                 | PAYG                          | $2.40
| **Event Hub**                                   | Basic, throughput units 20,1MB/sec ingress events, 2MB/sec egress events.                                   | PAYG                          |  $0.75
| **Cosmos DB**                                   | Standard, throuput 2500 RU/s (Request Units per second) 25 x100 Rus(Throughput)- $146 1 GB storage – $0.25  | PAYG                          | $146.25
| **Stream Analytics**                            | Standard Streaming Unit 3 unit(s) 3 * $80.30 Region: East US                                                | PAYG                          | $240.9
| **Total Cost**                                  |                                                                                                             |                               | $474.95
| **Total Cost Including Optional Components**    |                                                                                                             |                               | $479.55

**Monitoring status**

| **Monitoring Status**       | **Delta Price (Model1-Model2)**

| -----------------           | -----------------------

| **Without Monitoring**      | $80.75
| **With Monitoring**         | $79.75


**Deployment Costs for Type3**

| **Resource Name**                               | **Size**                                                                                                    | **Resource costing model**    | **Azure Cost/month**                                                                                                               
| -------------                                   | -------------                                                                                               | --------------------          | ------------                                                                                                             
| **App Service Plan(3 web apps + 1 web job)**    | B1 (1 core,1.75 GB RAM, 10GB Storage)                                                                       | PAYG                          | $54.75   
| **SQL Database**                                | S0 (Standard tier), 10DTU, 250GB storage                                                                    | PAYG                          | $14.72  
| **IoT HUB**                                     | S1, Unlimited devices, 1 Unit-$25 400,000 messages/day                                                      | PAYG                          | $25.00  
| **Log Analytics (Optional)**                    | First 5GB of data storage is free.Per GB(Standalone) Region                                                 | PAYG                          | $2.30 
| **Application Insights (Optional)**             | Basic, 1GB * $2.30 Region: East US                                                                          | PAYG                          | $2.30   
| **Storage Account**                             | Block Blob Storage, General Purpose V1, LRS Redundancy,100 GB Capacity                                      | PAYG                          | $2.40
| **Event Hub**                                   | Basic, throughput units 20,1MB/sec ingress events, 2MB/sec egress events.                                   | PAYG                          | $0.75
| **Cosmos DB**                                   | Standard, throuput 2500 RU/s (Request Units per second) 25 x100 Rus(Throughput)- $146 1 GB storage – $0.25  | PAYG                          | $146.25
| **Stream Analytics**                            | Standard Streaming Unit, 3 unit(s) 3 * $80.30 Region: East US                                               | PAYG                          | $240.9
| **Total Cost**                                  |                                                                                                             |                               | $484.77
| **Total Cost Including Optional Components**    |                                                                                                             |                               | $489.37

**Monitoring Status**

| **Monitoring Status**    | **Delta Price (Model1-Model3)**     | **Delta Price (Model2-Model2)**

| ------------------       | -----------------------             | ------------------------

| **Without Monitoring**   | $89.57                              | $9.82
| **With Monitoring**      | $89.57                              | $9.82


**Deployment Costs for Type4**

| **Resource Name**                               | **Size**                                                                                                    | **Resource costing model**    | **Azure Cost/month**                                                                                                               
| -------------                                   | -------------                                                                                               | --------------------          | ------------                                                                                                             
| **App Service Plan(6 web apps + 1 web job)**    | S0 * 2 (1 core,1.75 GB RAM, 10GB Storage)                                                                   | PAYG                          | $146.00   
| **SQL Database**                                | S0 (Standard tier), 10DTU, 250GB included storage per DB                                                    | PAYG                          | $29.44  
| **IoT HUB**                                     | S1, Unlimited devices, 1 Unit-$25 400,000 messages/day                                                      | PAYG                          | $25.00  
| **Log Analytics (Optional)**                    | First 5GB * $2.30  Region East US                                                                           | PAYG                          | $2.30 
| **Application Insights (Optional)**             | Basic, 1GB * $2.30 Region: East US                                                                          | PAYG                          | $2.30   
| **Storage Account**                             | Block Blob Storage, General Purpose V1, LRS,100 GB Capacity                                                 | PAYG                          | $2.40
| **Event Hub**                                   | Basic, throughput units 20,1MB/sec ingress events, 2MB/sec egress events.                                   | PAYG                          | $0.75
| **Cosmos DB**                                   | Standard, throuput 2500 RU/s (Request Units per second) 25 x100 Rus(Throughput)- $146 1 GB storage – $0.25  | PAYG                          | $146.25
| **Stream Analytics**                            | Standard Streaming Unit 3 unit(s) 3 * $80.30 Region: East US                                                | PAYG                          | $240.9
| **Traffic Manager**                             | 3 Endpoints 3 * $0.54                                                                                       | PAYG                          | $1.62
| **Total Cost**                                  |                                                                                                             |                               | $592.36
| **Total Cost Including Optional Components**    |                                                                                                             |                               | $596.96

**Monitoring Status**

| **Monitoring Status**           |**Delta Price (Model1-Model4)**      |**Delta Price (Model2-Model4)**      |**Delta Price (Model2-Model4)**

| -----------------               | ---------------------------         | ----------------------              | -----------------------

| **Without Monitoring**          | $197.16                             | $117.41                             | $107.59
| **With Monitoring**             | $197.16                             | $117.41                             | $107.59


## 5 Prerequisites for Deploying ARM Template

  1. The Azure AD B2C Tenant should be created and register your web application. 
  2. Create an account in Power BI 
  3. Create an Azure Service Principal. 

### 5.1 Azure B2C Tenant Creation and Configuration   

Creating Azure AD B2C tenant is a one-time activity, if you have a B2C Tenant already created by your admin then you should be added into that tenant as Global Administrator to register your app to get the B2C tenant id, application id and sign-in/sign-up policies.  

**Follow Below steps to create Azure AD B2C Tenant:**

1. Create a new B2C tenant in Azure Active Directory B2C. You'll be shown a page with the information on Azure Active Directory B2C. Click Create at the bottom to start configuring your new Azure Active Directory B2C tenant.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/3.png)

2. Choose the Organization name, Initial Domain name and Country of Region for your Tenant.

3. Note down your entire Tenant name which is highlighted in the below screenshot, this will be used while deploying the ARM template.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/4.png)

4. Once the B2C Tenant is created, Click Directory and Subscription filter on the top right to see your newly created tenant.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/5.png)

5. Switch to your created tenant by clicking on it. Type Azure in search column and select Azure AD B2C.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/6.png)

6. You can see the created tenant overview like below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/7.png)

7.	Click on sign-up or sign-in policies. Then click on Add to add policy.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/8.png)

8.	Provide the name and enter the details as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/9.png)

9.	Select all the Sign-up attributes as show below.

10.	Note down the policy name that you are creating now, this will be used while deploying the template.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/10.png)

11.	Select all the Application claims as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/11.png)

12.	After filling all the required details, click on Create.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/12.png)

13.	Once the deployment is complete, the below screen will appear with sign-up details.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/13.png)

14. Click on the Applications tab and click Add to create a new application.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/36.png)

15.	Provide a name for the application.

16.	Under the Web APP/Web API tab, click Yes to provide the following two redirect URLs for your application. Add an entry in the Redirect URLs section of the B2C application in the following format.

•	https://<**Website Name**>.azurewebsites.net/redirect.html

Note: **Website Name** should be different from **application name.**

•	http://localhost:65159/redirect.html

17.	During the web app registration with PowerBI, you will use this reply URL.

**Example: https://webappiot.azurewebsites.net/redirect.html**

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/36-1.png)

18. Click Yes under the Native client to include the native client url as shown below.

Eg: com.onmicrosoft.<**tenant name**>.<**application name**>://redirect/path

com.onmicrosoft.**amsiot1**.**webapp**://redirect/path

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/36-2.png)

19.	Before clicking on create, note down the application name, Reply URL’s and Custom Redirect URI.

20. After that, click on Create. This web app is used for authenticating the Asset management user login/ registration.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/37.png)


21. Select the application you created and note down the Application ID.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/38.png)


### 5.2 Power BI Configuration

Go to https://dev.powerbi.com/apps and register the web app.

a. Login to your Power BI account with the Azure Login credentials that have Global admin permissions.

b. Provide a name for your web app (This is different from what we created before).

c. Select App type “server-side Web App”.

d. Enter the Redirected URL and Home URL, same as you gave in Azure AD B2C tenant URL without “/redirect.html” for Home URL.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/40.png)

e. Select check boxes for required API’s (select all check boxes for best practice).

* Read all datasets

* Read and write all data sets

* Read all dashboards

* Read all reports

* Read and Write all reports

* Read all Groups

* Create content

f. Click on Register App.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/41.png)

g. The Client id and secret key will be generated. Note down these keys locally, as you will use these later in the configuration.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/42.png)

2. Go to Azure Active Directory from Your Azure Account and click on the App registrations tab. Select the app you just created in PowerBI.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/43.png)

**NOTE:** To grant permissions to the app you must be a **Global Administrator** in the Tenant.

3. Click on the app, navigate to all settings, and give the Required permissions.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/44.png)

4. Enable the following access under delegated permissions in Windows Azure Active Directory.

* Access the directory as the signed in users

* Read directory data

* Read and write all groups

* Read all user’s basic profiles

* Sign in and read user profile

After that click on **Save**

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/45.png)

5. Enable the following access under delegated permissions in Power BI access.

* View all datasets

* View all dashboards

* View content properties

* View all reports

* Create content

* View user groups

* Read and write all datasets

* Read and write all reports

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/46.png)

6. The user can see the number of permissions which have been added.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/47.png)

7. Click on **Grant Permissions**, then click **Yes**.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/48.png)

### 5.3 Creating an Azure Service Principal

To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.

Note down the following ID's once you create the application in Azure Active Directory. You need to enter these details while deploying the ARM template.

o Subscription ID - **You can get the subscription ID in the Azure**

o Tenant ID

o Client ID

o Client Secret 

1. Go to Azure portal..

2. Select **Azure Active Directory**.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/49.png)

3. Select **App registrations**

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/50.png)

4. Select **New application registration**

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/51.png)

5. Provide a name and URL for the application. Select either **Web app / API** or **Native** for the type of application you want to create. After setting the values, select **Create**.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/52.png)

6. You have created your application.

**Get application ID and authentication key**

When programmatically logging in, you need the ID for your application and an authentication key. To get those values, use the following steps:

1. From App registrations in Azure Active Directory, select your application

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/53.png)

2. Copy the Application ID and store it in a secure place. This application ID also refers as the client id.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/54.png)

3. To generate an authentication key, goto settings select Keys.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/55.png)

4. Provide a description of the key, and a duration for the key. When done, select Save.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/56.png)

5. After saving the key, the value of the key is displayed. Copy this value because you are not able to retrieve the key later. You provide the    key value with the application ID to log in as the application. Store the key value where your application can retrieve it.

**Get tenant ID**

When programmatically logging in, you need to pass the tenant ID with your authentication request.

1. To get the tenant ID, select Properties for your Azure AD tenant.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/57.png)

2. Copy the Directory ID. This value is your tenant ID.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/58.png)

**Assign application to role**

To access resources in your subscription, you must assign the application to a role. Make sure that it has the contributor role in your Azure subscription, which allows you to create and delete resources.

1. Navigate to the level of scope you wish to assign the application to. For example, to assign a role at the subscription scope, select **Subscriptions**. You could instead select a resource group or resource.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/59.png)

2. Select the particular subscription (resource group or resource) to assign the application to.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/60.png)

3. Select Access Control (IAM).

4. Select Add.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/61.png)

5. Select Contributor role to assign to the application.

6. Search for your application, and select it.

7. Select **Save** to finish assigning the role. You see your application in the list of users assigned to a role for that scope.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/62.png)

## 6 ARM Template Input Parameters

| **Parameter Name**                               | **Description**                                                                                            | **Allowed Values**    | **Default Values**                                                                                                               
| -------------                                    | -------------                                                                                              | -----------------     | ------------                                                                                                             
| **Solution Type**                                | 1.solution with monitoring - this will deploy AMS core solution & monitoring components. 2. solution without monitoring - this will deploy core AMS solution | solution with monitoring.                          |    
| **Costing Model**                                | Costing models have predefined resources sizes. Please refer Costing Model tables                          | One, Two, Three, Four |   
| **locationDr**                                   | specify the region for webapps and azure sqlserver desaster recovary it should be different of resource group region     | Any String          |  
| **App Insights Location**                    | specify the region for application insights, if you have selected solution type as without monitoring this is optional       | eastus, northeurope,       southcentralus, southeastasia,  westeurope,  westus2      |westus2 
| **IoThub name**             | Name of the IoT Hub instance to provision    |Min Length: 3                | 
| **Capacity units**          | number of desired iot hub units. restricted to 1 unit for F1. Can be set up to maximum number allowed for subscription.           | minValue: 1           | 1 
| **sqlAdministratorLogin**   | provide the user name for the sql server, please make a note of Username this will be used further                                    | Any string | Sqluser 
| **sqlAdministratorLoginPassword**   | provide the password for the sql server, make a note of the Password this will be used further   | PAYG                          | $146.25
| **Stream Analytics**      | Password must be 12 characters and have 3 of the following 1 lower case character, 1 number, and 1 special character  |
| **Sql database name**     | The name of SQL databa                                                         |                               |
| **Sku Capacity**    | describes plan's instance count                                                      | 1                             | 1
| **Website Name**  | Describes Web Site name which should be unique. Enter Website name which you entered in 5.1 section at 16th point (Eg: https://<Website Name>.azurewebsites.net/redirect.html) |           |
| **Website Name Dr**  | Describes Web Site name which should be unique for recovery app    |                                                 |
| **Node server Name**      | Describes the node server name which should be unique. |                       |
| **Api server Name**       | Describes API Server name which should be unique                               |                                |
| **AD Subscription Id**    | Enter your Azure account subscription Id.                                      |                                |
| **AD Tenant Id**          | Enter your Azure account tenant Id.                                            |                                |
| **B2c Tenant**            | Name of the B2C Tenant which you created in 5.1 section at 3rd point. (Eg: amsiot1.onmicrosoft.com)              |                     |
| **B2c Client Id**         | Enter B2C Client id (Application id) that you got after creating the B2C application in 5.1 section at 21st point.                     |                           |
| **B2c Client Id**         | Enter B2C Client id (Application id) that you got after creating the B2C application in 5.1 section at 21st point.                     |                           |
| **B2c Client Id Dr**      |
| **B2c SignUp SignIn policy Id**               | Enter Sign Up Sign In Policy name which you created 5.1 section at 9th point.                                      |                           | 
| **B2c Native Redirect URL**                   | Enter B2C native Redirect URL which you entered while creating the web application in B2C tenant in 5.1 section at 18th point.            |                     |
| **B2c Native Redirect URL Dr**                   |           |                     |
| **AD Client Id**                              | Enter the Client Id that you got from the Azure Active Directory Application in 5.3.1 section at 2nd point (Get application ID and authentication key).           |                     |
| **Ad Secret Key**                             | Enter the Secret key that you got from the Azure Active Directory Application in 5.3.2 section at 4th point (Get application ID and authentication key).            |                     |
| **Webjob Storage type**                        | Select Storage Type            | Standard_LRS, Standard_ZRS, Standard_GRS, Standard_RAGRS, Premium_LRS         | Standard_LRS 
| **Read Region Location**                       | if you select costing model 4 specify the read region of the cosmos database account the region should be different of the resource group region  |eastasia,     southeastasia, centralus, eastus, eastus2, westus, northcentralus, southcentralus, northeurope, westeurope, japanwest, japaneast, brazilsouth, australiaeast, australiasoutheast, southindia,    centralindia,westindia,  canadacentral, canadaeast, uksouth, ukwest, westcentralus, westus2, koreacentral, koreasouth              |
| **OMS Workspace Region**                      | specify the region for oms workspace, if you have selected solution type as without monitoring this is optional            | eastus, westeurope,        southeastasia, australiasoutheast                    | Eastus 
| **OMS Automation Region**                     | specify the region for oms automation account, if you have selected solution type as without monitoring this is optional            | westeurope,            southeastasia, eastus2, southcentralus, japaneast, southeastasia, southcentralus, northeurope, canadacentral, australiasouthest,  centralindia, japaneast    | eastus2 
| **Data Retention**                               | specify the oms retention period in days, if you have selected solution type as without monitoring this is optional          | Min Value: 7 Max Value: 730   | 7
| **Traffic Rouitng methods**                     | specify the traffic routing method for traffic manager            | Performance, Weighted, Geographic Priority                      | Priority 

## 7 Getting Started

### 7.1 Deploying the ARM Template

1. Click below Git hub repo url.

**https://github.com/sysgain/ams-iot.git**

2. Take the main-template.json raw file from testing1 branch. 

3. Go to Azure portal.

4. Navigate to **Create a resource (+)**, search for Template deployment.

5. Click on **create** and click on **Build your own Template**.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/63.png)

6. Replace the template and click on Save

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/64.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/65.png)

7. Deploy the template by providing the following parameters in custom deployment settings.

•	Location 				          - Select location from the drop down.

•	IoT Hub Name			        - Give user defined name.

•	SKU Name 			            - Select SKU type from the drop down.

•	 Capacity Units 			    – Enter Capacity units of IoT Hub.

•	Web job storage type		  – Select storage account type from the drop down.

•	SQL Administrator Login	  – Enter username for SQL server.

•	SQL Administrator Login Password - Enter Password for SQL server.

•	SQL Database Name		      – Enter database name for SQL server.

•	Web SKU Name 			        – Select SKU type from the drop down.

•	SKU Capacity			        – Enter the SKU capacity.

•	Webapp Name 			        – Enter Website name which you entered in 2.1 section at 16th point (Eg: https://<**Website Name**>.azurewebsites.net/redirect.html)

•	Node Server 			        - Give user defined name.

•	Api Server 			          - Give user defined name.

•	B2C Tenant 			          – Name of the B2C Tenant which you created in 2.1 section at 3rd point. (Eg: amsiot1.onmicrosoft.com)

•	B2C Client id 			      – Enter B2C Client id (Application id) that you got after creating the B2C application in 2.1 section at 21st point.

•	B2C Sign Up Sign In Policy Id 	– Enter Sign Up Sign In Policy name which you created 2.1 section at 8th point.

•	B2C native Redirect URL 	      -  Enter B2C native Redirect URL which you entered while creating the web application in B2C tenant in 2.1 section at 18th point.

•	Ad Subscription Id 		    – Enter your Azure account subscription Id.

•	Ad Tenant Id 			        – Enter your Azure account tenant Id.

•	Ad Client Id 			        – Enter the Client Id that you got from the Azure Active Directory Application in 2.3 section at 2nd point(Get application ID and authentication key).

•	Ad Secret key 			      - Enter the Secret key that you got from the Azure Active Directory Application in 2.3 section at 4th point(Get application ID and authentication key).


![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/66.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/67.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/68.png)

8. Once all the parameters are entered, click the terms and conditions check box and click Purchase.

9. Once the deployment is completed, you can start the workflow

## 8 Prerequisites for Gateway-Middleware

1. Visual studio 2015 with c++ dependency.

2. Install **GitBash.**

https://git-scm.com/download/win

4. Install **BLE scanner** app in your mobile to view the sensor ID.

5. Install **ASTRA** app in your mobile.

 https://projectiot.blob.core.windows.net/ams-iot/AndroidMobileApplication/astra.apk

6. Install CSR 4.0 setup file from the below link to enable **BLE** dongle so that your system will act as a Gate way. 

https://projectiot.blob.core.windows.net/ams-iot/CSR_4.0_Bluetooth_exe/CSR 4.0 setup.zip

7. Download Zadig file from the below link.

https://zadig.akeo.ie/

8. Install PowerBI for Desktop  from the below link.

https://www.microsoft.com/en-in/store/p/power-bi-desktop/9ntxr16hnw1t?rtc=1

## 9 Step 1: Run the Zadig file

1. Connect the BLE dongle to your system and enable the Bluetooth.

2. Open the zadig file as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/72.png)

3. Go to options and check list all devices.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/73.png)

4. Select the CSR device from the drop down as shown below and click Replace Driver then it will start installing the driver.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/74.png)

5. After the successful installation of driver you will get the following page.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/75.png)

6. Again, select the CSR device from the drop down as shown below and click Reinstall Driver then it will start installing the driver.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/76.png)

7. After successful installation you will get the following page.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/77.png)

## 10 Step 2: Setup GatewayMiddleware package

Configure the Gateway from the below document.

https://github.com/sysgain/ams-iot/raw/core_components/documents/Configuring%20the%20GatewayMiddleware%20Package.pdf

## 11 Step 3: Configuring WEBAPP

1. To start the work flow of AMS take the web app URL through portal.azure.com from the deployed resource group.

2. Go to Resource groupàsearch for your resource group name àthen click on it.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/79.png)

3. Now you can able to see all the resources of that resource group.

4. You can differentiate the resources based on their types. For that choose **Group By Type** option as shown in below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/80.png)

5. Now click on the name of the web app that you entered while deploying the template so that you can find the web app URL and copy that URL.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/81.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/82.png)

6. Now paste the copied URL in a browser to open the web application of the AMS.

7. Click Sign In.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/83.png)

8. If you are new, use sign-up to login into the web app.(or)if your account is already existed then provide the credentials to login.

9. The web page will take few minutes to open(refresh the page).

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/84.png)

## 12 Step 4: Adding the pre-requisites in the web app.

1. Go to inventory option in web app.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/85.png)

2. The page shows the number of gateways and sensors. Here it shows total gateway and sensor counts.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/86.png)

### 12.1 Adding Gateway

3. Now click on +Add New to add a new gateway.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/87.png)

4. We need to configure all these fields to add a gateway.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/88.png)

5. Click on update so that we can able to add the new gateway.

6. Once we click on update we can able to see the pop up as unit configured successfully and open the Add gateway page.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/89.png)

7. Enter the gateway Name, Serial No (gateway key ID), Description and then click on submit.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/90.png)

8. You can able to see the pop up of gateway added and the total gateway count.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/91.png)

### 12.2 Adding Sensor

9. Click +Add New to add a new sensor.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/92.png)

10. Now you need to enter all the fields of sensor

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/93.png)

11. You need to enter the fields as follows and click on **submit.**

12. Open **BLE Scanner** in your mobile and turn on the bluetooth.

13. Power on your **Sensor** and start searching for **CC2650 SensorTag** in BLE scanner by refreshing it.

14. Click **Connect** then it will get connected.

15. In **Add Sensor** window, give the Name as you like.

16. Give **Serial No** that shows in the BLE Scanner under **CC2650 SensorTag** without colons and alphabet should be in lower case as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/94.png)

17. Choose your Sensor tag as the Sensor type as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/95.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/96.png)

### 12.3 Adding Asset to Web App using Mobile Application

1. Open the mobile app named as **ASTRA** and enter the **rest server URL**.

2. You can find the rest server URL from the azure portal as follows.

3. Go to deployment àfind the resource group name, there you can find the apiserveràclick on the api server and note the url of the rest server.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/97.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/98.png)

4. Note the rest server URL and paste it in the mobile application and click submit

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/99.png)

5. Now the mobile app page redirected to microsoft login page.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/100.png)

6. Enter the credentials to login into application.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/101.png)

7. Now you can able to view the application page as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/102.png)

8. Click on Dispatch option to add an asset to the web portal.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/103.png)

9. Before adding asset to the webportal generate **qrcode** for your sensor and barcode for asset by using the following url’s.

    **Qrcode** -> https://www.barcodesinc.com/generator/qr 

	  **Barcode** -> https://www.barcodesinc.com/generator/index.php

10. you need to add the sensor by using the **qrcode**. While generating the Qrcode, you need to enter your **Sensor ID** in text box and click **Create QR code**.

11. Then Scan the **QR code** in **ASTRA** app in your mobile.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/104.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/105.png)

12. Click on **next**.

13. Add asset to the web portal by scanning the barcode as follows.

14. Generate **Barcode** by entering any text in the text box and scan the **Barcode** in **ASTRA** app in your mobile

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/106.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/107.png)

15. Click next.

16. Now you need to link the asset with the sensor so that asset can be added to the web portal.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/108.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/109.png)

17. Go to web portal and check whether the asset has been added or not.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/110.png)

### 12.4 Adding Assets to a Group

18. Now we need to add the asset to a group. For that you need to check the asset so that Add Group option will be enable.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/111.png)

19. Click on Add group to add asset to a group.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/112.png)

20. Enter name and description of the group and click submit.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/113.png)

21. You can able to see the group in the inventory option as follows

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/114.png)

### 12.5 Cofiguring the PoweBi Desktop App and Publishing


22. Go to Configurations and add the following information.

23. First, we need to enable the firewall of the sqlserver as follows.

24. Go to the resources and choose the resource as sqlserverà Go to firewalls and virtual networks field in the settings option.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/115.png)

25. Add client IP to enable the firewall.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/116.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/117.png)

26. click save option to save the firewall values.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/118.png)

27. Here you can see the successful updation of adding firewall.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/119.png)

28. To configure the powerbi urls and credentials first we need to configure the powerbi desktop as follows.

29. Download the PowerBI template from the below link.

https://projectiot.blob.core.windows.net/ams-iot/AMSLatestcode/HistoricalReport .pbit

30. Run the downloaded powerbi template and enter all the input parameters.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/120.png)

31. Here the fields require,

    **sql server name**

    **Sql database**

    **Document DB url**

    **Document DB Name**

    **Document DB Collection Name**

32. All these values are taken from the azure portal.

33. Go to azure portal and choose your deployment, there you can find all the resources.

34. Now click on sqldb, so that you can find the sql server name and sql db name as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/121.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/122.png)

35. Note down the above two values.

36. Go to document db and note down the values of Collection name and data base name.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/123.png)

37. Go to keys field in the settings option of document and note down the Document DB url and primary key values.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/124.png)

38. Now enter all tehse values in powerbi desktop.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/125.png)

39. Click on load.

40. After loading it will ask for some additional information like cosmos DB account key there you can enter the primary key value of document DB.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/126.png)

41. Click on connect. A Pop-up occurs for sql authentication as follows. Here you need to choose the authentication type as database.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/127.png)

42. Enter the sql user name and password and click connect.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/128.png)

43. Click on run to load the db tables into the powerbi.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/129.png)

44. Here you can see the data fetching from db to powerbi.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/130.png)

45. Once entire data has been fetched the page can be appeared as follows.

46. Here you can click on publish button to publish the powerbi desktop url. Click **publish.**

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/131.png)

47. Click on **save**.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/132.png)

48. You can save the powerbi desktop into your local machine. For that, choose the file location to save.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/133.png)

49. After saving the content it will ask for the destination.Here, the default is workspace and click select.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/134.png)

50. Then the following url will be appeared.click on the **url** ,there you can find the report id of the powerbi.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/135.png)

51. The page can be appeared as follows and here we need to note down the id in between reports and report section

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/136.png)

### 12.6 Configuring the flow in web app

52. Go to web app and click on **configuration** -> choose **powerbi credentials**

53. Enter the values of **powerbi client id, Secret key, username and password (Azure portal credentials).**

54. Click **submit**.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/137.png)

55. Here you can see the pop up saying configuration added/updated.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/138.png)

56. Now open **powerbi url** and paste the published url id in the place of report id.

Example: https://app.powerbi.com/reportEmbed?reportId=5a69ed50-c11f-4097-b608-3d9cf94eb6b8

57. click **submit**. There you can see the successful adding of URL.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/139.png)

## 13 Step 5: Running the gateway middleware

1. Go to portal àclick on apiserverà copy the apiserver URL.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/140.png)

2. Paste it in the gateway window(Asset Monitoring Configuration page) and add / at the end as shown below.

3. Click submit.

**Note:** If the gateway window(Asset Monitoring Configuration) page is closed, run electron . command in gitbash then you will get the gateway window(Asset Monitoring Configuration page).

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/141.png)

4. The page will be redirect to Microsoft login page.

5. Ignore the message by click on ok

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/142.png)


6. Enter the credentials to login. Use the login credentials what we are using to sign up for web app.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/143.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/145.png)

7. Now close the gateway window and run the electron . in gitbash, so that it will automatically direct to the gateway page with all authentications.

**Note:** the sensor should be in on.

8. Here you can see the data coming from the gateway to iot hub via sensor.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/147.png)

### 13.1 Validating data in iot hub and Node server

9. Go to Azure Portal and click IoT Hub as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/147-1.png)

10. The data in iot can be appeared as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/148.png)

11. You can also see the live data in node server.

12.	Go to your Resource Group and click nodeserver as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/148-1.png)

13. To view you need to enable the diagnostic log settings as follows in node server.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/149.png)

14. Go to log stream and see the data as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/150.png)

## 14 Step 6: validating the data in web app

1. To see the live data in web app go to reports -> select group followed by sensor value.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/151.png)

2. Choose group name.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/152.png)

3. Choose sensor name.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/153.png)

4. Here you can find the data coming from iot hub to web application via node server.

5. All the capabilities of sensor data can be viewd as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/154.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/155.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/156.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/157.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/158.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/159.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/160.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/161.png)

## 15 Step 7: Creating and validating the rule in Web app

1. After viewing the reports create a rule based on some threshold conditions.

2. For that go to rules click +Add New.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/162.png)

3. Select the group value of assets.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/163.png)

4. You can set the values to some threshold level.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/164.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/165.png)

5. Click done.

6. You can see the created rule as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/166.png)

7. You can see the rules that we created by refreshing the webapp page and click on rules.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/167.png)

8. Now go to reports and see the capabilities of sensor after adding the rule.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/168.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/169.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/170.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/171.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/173.png)


## 16 Step 8: Configuring the Indoor map in web app

1. Go to configuration,select indoor map Configuration

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/176.png)

2. Upload your indoor map and click **Add.**

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/177.png)

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/178.png)

3. The map can be appeared as follows. The pop up says that indoor map added.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/179.png)

### 16.1 Adding gateway rule

4. Now you need to select the gateway id in the indoor map location.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/180.png)

### 16.2 Positioning the gateway on the layout

5. Now position the gateway at some location in the map and click **update.**

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/181.png)

6. Here you can see the pop up as gateway mapped successfully.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/182.png)

### 16.3 Indoor alert notification	

7. Now Go to dashboard -> click on the flip icon as shown in the below screen shot.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/183.png)

8. Once you click the flip symbol, you can able to see the gateway,sensor and the range in between them.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/184.png)

9. Now click on the sensor colored as yellow, you can see all the capabilities of sensor.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/185.png)

### 16.4 Alerts checking

10. If any rule get bleached you found the alert as like above screen shot.

11. Go to Alerts,select the group -> Asset -> capability and click **apply**

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/186.png)

### 16.5 Asset Status

12. Finally, you can see the status of the asset by using mobile application.

13. Open mobile app and click on the receive option.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/187.png)

14. Now scan the barcode of the asset as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/106.png)

15. Then the status of asset can be appeared as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/189.png)
