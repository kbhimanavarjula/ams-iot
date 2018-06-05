
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
    	    
       - [5.1.1 Create an Application in Azure B2C Tenant for Deployment Cost Type 1 or 2 or 3](#511-create-an-application-in-azure-b2c-tenant-for-deployment-cost-type-1-or-2)
	    
	   - [5.1.2 Create an Application in Azure B2C Tenant for Deployment Cost Type 4](#512-create-an-application-in-azure-b2C-tenant-for-deployment-cost-type-3-or-4)

    - [5.2 Power BI Configuration](#52-power-bi-configuration)
    - [5.3 Creating an Azure Service Principal](#53-creating-an-azure-service-principal)
	   
	   - [5.3.1 Get application ID and authentication key](#531-get-application-id-and-authentication-key)
	   
	   - [5.3.2 Get tenant ID](#532-get-tenant-id)
	  
	   - [5.3.3 Assign application to role](#533-assign-application-to-role)
	  
- [6 ARM Template Input Parameters](#6-arm-template-input-parameters)
- [7 Getting Started](#7-getting-started)
   - [7.1 Deploying the ARM Template](#71-deploying-the-arm-template)
- [8 Prerequisites for Gateway-Middleware](#8-prerequisites-for-gateway-middleware)
   - [8.1 Step 1 Run the Zadig file](#81-step-1-run-the-zadig-file)
   - [8.2 Step 2 Setup GatewayMiddleware package](#82-step-2-setup-gatewaymiddleware-package)
   - [8.3 Step 3 Configuring WEBAPP](#83-step-3-configuring-webapp)
   - [8.4 Step 4 Adding the pre-requisites in the web app](#84-step-4-adding-the-pre-requisites-in-the-web-app)

       - [8.4.1 Adding Gateway](#841-adding-gateway)

       - [8.4.2 Adding Sensor](#842-adding-sensor)

       - [8.4.3 Adding Asset to Web App using Mobile Application](#843-adding-asset-to-web-app-using-mobile-application)

       - [8.4.4 Adding Assets to a Group](#844-adding-assets-to-a-group)

       - [8.4.5 Cofiguring the PoweBi Desktop App and Publishing](#845-cofiguring-the-powebi-desktop-app-and-publishing)

       - [8.4.6 Configuring the flow in web app](#846-configuring-the-flow-in-web-app)

   - [8.5 Step 5 Running the gateway middleware](#85-step-5-running-the-gateway-middleware)

       - [8.5.1 Validating data in iot hub and Node server](#851-validating-data-in-iot-hub-and-node-server)

   - [8.6 Step 6 validating the data in web app](#86-step-6-validating-the-data-in-web-app)
   - [8.7 Step 7 Creating and validating the rule in Web app](#87-step-7-creating-and-validating-the-rule-in-web-app)
   - [8.8 Step 8 Configuring the Indoor map in web app](#88-step-8-configuring-the-indoor-map-in-web-app)

       - [8.8.1 Adding gateway rule](#881-adding-sensor)

       - [8.8.2 Positioning the gateway on the layout](#882-positioning-the-gateway-on-the-layout)

       - [8.8.3 Indoor alert notification](#883-indoor-alert-notification)

       - [8.8.4 Alerts checking](#884-alerts-checking)

       - [8.8.5 Asset Status](#885-asset-status)

- [9 Monitoring Componenets](#9-monitoring-components)
    - [9.1 OMS Log Analytics](#91-oms-log-analytics)
    - [9.2 Application Insights](#92-application-insights)
- [10 Hardening Components](#10-hardening-components)
    - [10.1 Geo Replication](#101-geo-replication)
          
        - [10.1.1 Setting up Geo Replication for Cosmos DB](#1011-setting-up-geo-replication-for-cosmos-db)
         
	    - [10.1.2 Setting up Geo Replication for SQL DB](#1012-setting-up-geo-replication-for-sql-db)
    - [10.2 Traffic Manager](#102-traffic-manager)
	
## 1 About Asset Monitoring Solution

Asset Monitoring and Tracking Solution is a complete smart inventory management tool. The solution provides a web dashboard & a mobile application to Monitor, Locate and Report all the remote assets so that they are completely visible 24x7.

## 2 Architecture

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/1.jpg)

**With Monitoring Architecture Diagram**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/AMS%20monitoring185.jpg)

**With Hardening Architecture Diagram**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/AMS%20Hardening24-05-18.jpg)

## 2.1 Data Flow Architecture Diagram

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/2.jpg)

## 3 Azure Services

The below described azure services are used for AMS core solution.

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

Azure Web Job is back-end program you can run inside Azure, without Azure Web Job, you can deploy windows console app or windows service app to your server, then setup scheduler via windows scheduler or other third-party windows scheduler tools. 41
### 3.5 Azure SQL DB 

Azure SQL Database is a relational database-as-a service using the Microsoft SQL Server Engine. SQL Database is a high-performance, reliable, and secure database you can use to build data-driven applications and websites in the programming language of your choice, without needing to manage infrastructure. 

### 3.6 Azure DocumentDB 
Azure DocumentDB is a general-purpose NoSQL database that is used in a wide range of applications and use cases. It is a good choice for any application that needs low order-of-millisecond response times, and needs to scale rapidly. 
Azure Event hub 

### 3.7 Azure Event Hub
Azure Event Hubs is a highly scalable data streaming platform and event ingestion service, capable of receiving and processing millions of events per second. Event Hubs can process and store events, data, or telemetry produced by distributed software and devices. Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters. 

## 4 Deployment Costs 

Below table describes the deployment costs per month for the solution.

**Deployment Costs for Type1 (Core Solution)**

**Region-US East**

| **Resource Name**                               | **Size**                                                                                                    | **Resource costing model**    | **Azure Cost/month**                                                                                                                
| -------------                                   | -------------                                                                                               | --------------------          | ------------                                                                                                             
| **App Service Plan**    | B1 (1 Cores(s), 1.75 GB RAM, 10 GB Storage, US$0.075)                                                          | PAYG                          | $54.75  
| **SQL Database**                                | B1 (Basic tier), 5DTUs, 2GB included storage per DB, US$ 0.0067/hour                   | PAYG                          | $4.90  
| **IoT HUB**                                     | S1(Standard), Unlimited devices, 400,000 msgs/day, US$ 25.00/month. 400,000 messages/day.         | PAYG                          | $25.00   
| **Event Hub**                                   | Standard, throughput units 2. Ingress 1 million events.                                | PAYG                          | $43.83 
| **Cosmos DB**                                   | Standard, storage: 1 GB * US$ 0.250 per GB/month, Rus reserved: 4x100 RU/sec * US$ 0.008 per hour    | PAYG                | $23.61
| **Stream Analytics**                            | Standard Streaming Unit 1 unit(s) 1 * US$ 80.30                                         | PAYG                          | $80.30
| **Storage Account**                        | Capacity 1GB=US$ 0.02, Redundancy=LRS               | PAYG                             | $0.o2
|                                |                                                                                             | **Estimated Monthly Cost**                 | **US$ 232.41** 

**Deployment Costs for Type2 (Core Solution with Monitoring)**

| **Resource Name**                               | **Size**                                                                                                    | **Resource costing model**    | **Azure Cost/month**                                                                                                               
| -------------                                   | -------------                                                                                               | --------------------          | ------------                                                                                                             
| **App Service Plan**                            | B1 (1 Cores(s), 1.75 GB RAM, 10 GB Storage, US$0.075)                                     | PAYG                          | $54.75   
| **SQL Database**                                | B1 (Basic tier), 5DTUs, 2GB included storage per DB, US$ 0.0067/hour                      | PAYG                          | $4.90  
| **IoT HUB**                                     | S1(Standard), Unlimited devices, 400,000 msgs/day, US$ 25.00/month. 400,000 messages/day.         | PAYG                          | $25.00 
| **Event Hub**                                   | Standard, throughput units 2. Ingress 1 million events  .                               | PAYG                          |  $43.83  
| **Cosmos DB**                                   | Standard, storage: 1 GB * US$ 0.250 per GB/month, Rus reserved: 4x100 RU/sec * US$ 0.008 per hour   | PAYG                          | $23.61
| **Stream Analytics**                            | Standard Streaming Unit, 1 Units * US$ 80.30                                                 | PAYG                          | $80.30
| **Storage Account**                       | Capacity 1GB=US$ 0.02, Redundancy=LRS                | PAYG                    | $0.02
| **OMS(Log Analytics)**       | Logs ingested 6VMs * 1 Average logs ingested per VM(in GB) , 5 GB of data is included for free. An average Azure VM ingests 1 GB to 3 GB of data per month. Region: East US)          | PAYG                   | $2.30 
| **Application Insights**             | Basic, 6 GB * US$ 2.30 (5GB of data is included for free per month. Region: East US.                      | PAYG                          | $2.30   
|                                  |                                                    | **Estimated monthly cost**                              | **US$ 237.01** 
                                                      
**Deployment Costs for Type3 (Core Solution with Hardening)**

| **Resource Name**                               | **Size**                                                                                                    | **Resource costing model**    | **Azure Cost/month**                                                                                                               
| -------------                                   | -------------                                                                                               | --------------------          | ------------                                                                                                             
| **App Service Plan**    | S1:2 Cores(s), 3.5 GB RAM, 50GB Storage, US$ 0.200, 1 Instance                                                                      | PAYG                          | $146.00    
| **SQL Database**                                | B1 (Basic tier), 5DTUs, 2GB included storage per DB, US$ 0.0067/hour                                        | PAYG                          | $4.90   
| **IoT HUB**                                     | S1(Standard), Unlimited devices, 400,000 msgs/day, US$ 25.00/month. 400,000 messages/day.    | PAYG                          | $25.00   
| **Event Hub**                                   | Standard, throughput units 2. Ingress 1 million events.                                 | PAYG                          | $43.83
| **Cosmos DB**                                   | Standard, storage: 4 GB * US$ 0.250 per GB/month, Rus reserved: 8x100 RU/sec * US$ 0.008 per hous   | PAYG                    | $47.72 
| **Stream Analytics**                            | Standard Streaming Unit, 1 Units * US$ 80.30                                                | PAYG                          | $80.30
| **Storage Account**                 | Capacity 1GB=US$ 0.02, Redundancy=LRS                       | PAYG                      | $0.02
| **Azure App Service Certificate**             | S1 Standard, 69.99 * 3 USD/YEAR                   | BYOL                      | $209.97
| **Hardining(Geo-Replication+traffic manager)**       | TM:  3 * 2 External EndPoints US$ 0.54, Region: East US                               | PAYG                              | $3.24  
|     |                                                        | **Estimated monthly cost**                              | **US$ 560.98** 

**Deployment Costs for Type4 (Core Solution with Monitoring and Hardening)**

| **Resource Name**                               | **Size**                                                                                                    | **Resource costing model**    | **Azure Cost/month**                                                                                                                     
| -------------                                   | -------------                                                                                               | --------------------          | ------------                                                                                                             
| **App Service Plan**    | S1:2 Cores(s), 3.5 GB RAM, 50GB Storage, US$ 0.200, 1 Instance                                                                    | PAYG                          | $146.00       
| **SQL Database**                                | B1 (Basic tier), 5DTUs, 2GB included storage per DB, US$ 0.0067/hour                                      | PAYG                          | $4.90     
| **IoT HUB**                                     | S1(Standard), Unlimited devices, 400,000 msgs/day, US$ 25.00/month. 400,000 messages/day.                 | PAYG                          | $25.00  
| **Event Hub**                                   | Standard, throughput units 2,1MB/sec ingress events, 2MB/sec egress events.                                 | PAYG                          | $43.83    
| **Event Hub**                                   | Standard, throughput units 2,1MB/sec ingress events, 2MB/sec egress events.                                 | PAYG                          | $43.83 
| **Cosmos DB**                                   | Standard, storage: 4 GB * US$ 0.250 per GB/month, Rus reserved: 8x100 RU/sec * US$ 0.008 per hour   | PAYG                          | $47.72 
| **Stream Analytics**                            | Standard Streaming Unit, 1 Units * US$ 80.30                                                 | PAYG                          | $80.30
| **Hardining(Geo-Replication+traffic manager)**         | TM:  3 * 2 External EndPoints US$ 0.54, Region: East US                              | PAYG                          | $3.24 
| **Storage Account**                      | Capacity 1GB=US$ 0.02, Redundancy=LRS            | PAYG                               | $0.02
| **Azure App Service Certificate**        | S1 Standard, 69.99 * 3 USD/YEAR          | PAYG                         | $209.97
| **Application Insights (Optional)**             | Basic, 6 GB * US$ 2.30 (5GB of data is included for free per month. Region: East US.                            | PAYG                          | $2.30 
| **OMS(Log Analytics)**    | Logs ingested 6VMs * 1 Average logs ingested per VM (in GB) , 5 GB of data is included for free. An average Azure VM ingests 1 GB to 3 GB of data per month. Region: East US)            | PAYG                          | $2.30    
|                                  |                                     | **Estimated Cost**                                                  | **US$ 565.58**                           

## 5 Prerequisites for Deploying ARM Template

  1. The Azure AD B2C Tenant should be created and register your web application. 
  2. Create an account in Power BI 
  3. Create an Azure Service Principal. 

### 5.1 Azure B2C Tenant Creation and Configuration   

Creating Azure AD B2C tenant is a one-time activity, if you have a B2C Tenant already created by your admin then you should be added into that tenant as Global Administrator to register your app to get the B2C tenant id, application id and sign-in/sign-up policies.  

**Follow Below steps to create Azure AD B2C Tenant:**

1. To create a new B2C tenant in **Azure Active Directory B2C**. Login to **Azure portal** -> Click **+** to Create a resource to open the New page.

2. In the New page **search box** enter **Azure Active Directory B2C** the result is displayed in the **Everything page**.

3. Click **Azure Active Directory B2C** to open a create **Azure Active Directory B2C page**.

4. Click **Create** button at the bottom to start configuring your new **Azure Active Directory B2C tenant**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/3.png)

5.	Select **Create** a new **Azure AD B2C Tenant**.

6.	Enter the **Organization name**, **Initial Domain name** in their respective fields and select the **Country of Region** for your Tenant from the dropdown list.

7.	Note down your entire **Tenant name** which is highlighted in the below figure, this will be used while deploying the **ARM template**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/4.png)

8.	Once the B2C Tenant is created, Click **Directory and Subscription filter** on the top right to see your newly created tenant.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/5.png)

9.	Switch to your created tenant by clicking on it. Type **Azure** in search box and select **Azure AD B2C**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/6.png)

10.	You can see the **created tenant** overview as shown in the following figure.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/7.png)

11.	Click **sign-up or sign-in policies** under **POLICIES** section. Then click **+Add** to add policy.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/8.png)

12.	Provide the **name** and enter the details as shown in the following figure.

13.	**Note** down the **policy name** that you are creating, as it is used while deploying the template.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/9.png)

14.	Select all the **Sign-up attributes** as show in the following figure.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/10.png)

15.	Select all the **Application claims** as shown in the following figure.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/11.png)

16.	After providing all the required details, click **Create** button.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/12.png)

17.	Once the deployment is complete, the sign-up details are displayed as shown in the following figure.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/13.png)

**Note**:

* If you want to **Deployment Cost Type 1 or 2 or 3**, follow the section 5.1.1. to create the Web Application. 

* If you want to **deploy Deployment Cost Type 4**, follow section **5.1.2.** to create the **Web Application**.

#### 5.1.1 Create an Application in Azure B2C Tenant for Deployment Cost Type 1 or 2 or 3 
 
1. Open **azure portal** -> **switch to created azure AD** -> Click the **Applications tab** and click **+Add** to create a new application. 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/36.png)

2. Provide a name for the application in the **name** field.

3. Under the **Web APP/Web API** tab, click **Yes** to provide the following two **Reply URLs** for your application. Add an entry in the **Reply URLs** section of the B2C application in the following format.

    * https://<**Website Name**>.azurewebsites.net/redirect.html

    **Note: Website Name** should be different from **application name.**

    * **http://localhost:65159/redirect.html**

4. During the web app registration with PowerBI, you will use this reply URL.

   **Example: https://webappiot.azurewebsites.net/redirect.html**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/36-1.png)

5. Click **Yes** under the **Native client** to include the native client url as shown below.

**Example**: com.onmicrosoft.<**tenant name**>.<**application name**>://redirect/path

com.onmicrosoft.**amsiot1**.**webapp**://redirect/path

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/36-2.png)

6. Before clicking on create, note down the **Website name, Reply URL’s and Custom Redirect URI**.

7. After that, click on **Create**. This web app is used for authenticating the Asset management user l**ogin/ registration**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/37.png)

8. Select the application you created and note down the **Application ID**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/38.png)

#### 5.1.2 Create an Application in Azure B2C Tenant for Deployment Cost Type 4 

**5.1.2.1 Key vault and webapp certificate creation**

If you want to deploy **core and hardening** and **core and hardening with monitoring** follow below steps:

**5.1.2.1. Keyvault creation**

1. Go to **Azure portal**.

2. Navigate to **(+)** to Create a resource, search for **keyvault**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/k1.png)

3. Click **create**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/k2.png)

4. When you click on create you can see the below fields.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/k3.png)

5. Enter the all required fields and click on **create**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/k4.png)

6. Now you can see the created keyvault in your resource group.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/k5.png)

**5.1.2.2 Certificate creation for traffic manager**

1. The Web App can be accessed with Traffic Manager URL but since the Traffic Manager has **http** protocol we have to redirect it to **https**. In order to redirect the http of Traffic Manager URL to https Configure an SSL Certificate for your Azure App Service.

2. **Click** on **+Add** (icon) in the Resource Group.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/image%20(1).png)

3. **Search** for **App Service Certificate** and **select** it to create a certificate.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z1.png)

4. **Enter** a friendly **Name** for your **SSL certificate** and enter the **Traffic manager name** in the **Domain Host Name**. Use the existing Resource Group, Accept the Legal Terms and **click** on Create.

**Note:** Make sure to enter **correct** host name (custom domain) that you want to protect with this certificate. **DO NOT** append the Host name with **WWW**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z2.png)

5. Once the SSL Certificate purchase is complete.The certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate. **Click** **Certificate Configuration** inside the Certificate Properties page.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z3.png)

6. **Click** on **Step 1** Store to store this certificate in Azure Key Vault.From the Key Vault Status page, **click Key Vault Repository** to choose an existing Key Vault to store this certificate **OR** **Create New Key Vault** to create new Key Vault inside same subscription and resource group.

7. Once you have selected the Key Vault Repository to store this certificate in, the Store option should show success.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z4.png)

8. From the same **Certificate Configuration** page you used in **Step 5**, click Step 2: Verify. There are **four** types of domain verification supported by App Service Certificates: **App Service, Domain, Mail, and Manual Verification**. Choose **App Service**. **Click** on **Verify** button to complete this step.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z5.png)

9. After clicking Verify, use the **Refresh** button until the Verify option should show success.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z6.png)

10. Created certificates for **restserver** and **nodeserver** you will follow the above steps mentioned **webapp** for creating complete certification process.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z7.png)
![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z8.png)

 
**Retrieving the web apps certificate secret name and thumbprint from keyvault**

If you want to deploy the core and hardening and core and hardening with monitoring you should have the created three webapps certificate key vault secret names and certificate thumbprints.

1. go to the created keyvault resource group click on created keyvault resource  click on secrets if you see like below you are unauthorizes to view these contents add the user in the access polices by following the below steps.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s1.png)

**Add new user to key vault**

1. click **access policies** -> click **+add new**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s2.png)

2. select **user id** like below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s3.png)

3. select the **prinicipal, key permissions, secret permissions and certificate permissions** like below click **ok**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s4.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s5.png)

4. After **click** **save** you can see user is added like below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s6.png)

5. **Click secrets** then you can able to see the secrets.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s7.png)

6. **Click** on each **secret name** then you can get the key vault secret name of each certificate.

7. **Note down** the **secret keys**, you have to use In deployment.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s8.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s9.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s10.png)

8.	Go to the created certificate name there you can see the thumbprints.

9. **Note down** the **certificates**, you have to use in deployment.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s11.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s12.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/s13.png)

1. Go to your newly created B2C Tenant.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z9.png)

2. Click **Applications** and click **Add** on the left side to create a new application for traffic manager.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/z10.png)

3. Provide a name for the **application**. 

4. Under the **Web APP/Web API** tab, click **Yes** to provide the following two redirect URLs for your application. Add an entry in the Redirect URLs section of the B2C application in the following format. 

* https://<**Website Name**>.trafficmanager.net/redirect.html 
	
**Note: Website Name** should be different from **application name**. 

* http://localhost:65159/redirect.html  

5. During the web app registration with PowerBI, you will use this reply URL. 

**Example: https://webappiot.trafficmanager.net/redirect.html** 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/z11.png)

6. Click **Yes** under the **Native client** to include the native client URL as shown below.

Eg: com.onmicrosoft.<**tenant name**>.<**application name**>://redirect/path 
	
   com.onmicrosoft.**amsiot1. trafficmanagerapp:**//redirect/path
   
![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z12.png)
   
7. Before clicking on Create, note down the **website name, Reply URL’s and Custom Redirect URL**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z13.png)

8. After that, click **Create**.

9. Select the application you created and note down the **Application ID**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/z14.png)

10. Again, click the **Applications** tab and click **Add** to create another application for web application.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/z15.png)

11. Provide a name for the **application**.

12. Under the **Web APP/Web API** tab, click **Yes** to provide the two Reply URLs for your application. 

13.Enter the same **Reply URL’s** that you have entered in previous web application. **The Reply URLs should be same for both application**. 

14. During the web app registration with PowerBI, you will use this reply URL. 

**Example**: https://webapplication.trafficmanager.net/redirect.html 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/z16.png)

15. Click **Yes** under the **Native client** to include the native client URL as shown below.

Eg: com.onmicrosoft.<**tenant name**>.<**application name**>://redirect/path  
	
   com.onmicrosoft.**amsiot1.webapplication**://redirect/path 
   
![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z17.png)
   
16. Before clicking on Create, note down the **website name, Reply URL’s and Custom Redirect URL**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/z18.png)

17. After that, click **Create**. This web app is used for authenticating the Asset management user login/ registration.

18. Select the application you created and note down the **Application ID**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/Z19.png)

### 5.2 Power BI Configuration

1. Go to https://dev.powerbi.com/apps and register the web app.

a. Login to your Power BI account with the Azure Login credentials that have Global admin permissions.

b. Provide a **name** for your web app (This is different from what we created before).

c. Select App type “**server-side Web App**”.

d. Enter the Redirected URL and Home URL, same as you gave in Azure AD B2C tenant **Reply URL** without “/**redirect.html**” for Home URL. 

e. If you want to deploy Deployment Cost Type 4, give **traffic manager Reply URL** without “**/redirect.html**” for Home URL. 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/40.png)

f. Select check boxes for required API’s (select all check boxes for best practice).

* Read all datasets

* Read and write all data sets

* Read all dashboards

* Read all reports

* Read and Write all reports

* Read all Groups

* Create content

g. Click on **Register App**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/41.png)

h. The **Client id and secret key** will be generated. Note down these keys locally, as you will use these later in the configuration.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/42.png)

2. Go back to azure portal and navigate to **your Azure account** from **Azure B2C tenant** as shown below. 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/pb.png)

3. Go to **Azure Active Directory** from Your Azure Account and click on the **App registrations** tab. Select the app you just created in **PowerBI**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/43.png)

**NOTE:** To grant permissions to the app you must be a **Global Administrator** in the Tenant.

4. Click on the app, navigate to all settings, and give the **Required permissions**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/44.png)

5. Enable the following access under delegated permissions in Windows Azure Active Directory.

* Access the directory as the signed in users

* Read directory data

* Read and write all groups

* Read all user’s basic profiles

* Sign in and read user profile

6. After that click on **Save**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/45.png)

7. Enable the following access under delegated permissions in Power BI access.

* View all datasets

* View all dashboards

* View content properties

* View all reports

* Create content

* View user groups

* Read and write all datasets

* Read and write all reports

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/46.png)

8. The user can see the number of permissions which have been added.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/47.png)

9. Click on **Grant Permissions**, then click **Yes**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/48.png)

### 5.3 Creating an Azure Service Principal

To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.

Note down the following ID's once you create the application in Azure Active Directory. You need to enter these details while deploying the ARM template.

o Subscription ID - **You can get the subscription ID in the Azure**

o Tenant ID

o Client ID

o Client Secret 

1. Go to **Azure portal**.

2. Select **Azure Active Directory**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/49.png)

3. Select **App registrations**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/50.png)

4. Select **New application registration**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/51.png)

5. Provide a name and URL for the application. Select either **Web app / API** or **Native** for the type of application you want to create. After setting the values, select **Create**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/52.png)

6. You have created your application.

#### 5.3.1 Get application ID and authentication key

When programmatically logging in, you need the ID for your application and an authentication key. To get those values, use the following steps:

1. From **App registrations** in Azure Active Directory, select your **application**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/53.png)

2. Copy the **Application ID** and store it in a secure place. This **application ID** also refers as the **client id**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/54.png)

3. To generate an authentication key, goto **settings** select Keys.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/55.png)

4. Provide a description of the key, and a duration for the key. When done, select **Save**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/56.png)

5. After saving the key, the value of the key is displayed. Copy this value because you are not able to retrieve the key later. You provide the    key value with the application ID to log in as the application. Store the key value where your application can retrieve it.

#### 5.3.2 Get tenant ID

When programmatically logging in, you need to pass the tenant ID with your authentication request.

1. To get the **tenant ID**, select **Properties** for your Azure AD tenant.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/57.png)

2. Copy the **Directory ID**. This value is your **tenant ID**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/58.png)

#### 5.3.3 Assign application to role

To access resources in your subscription, you must assign the application to a role. Make sure that it has the contributor role in your Azure subscription, which allows you to create and delete resources.

1. Navigate to the level of scope you wish to assign the application to. For example, to assign a role at the subscription scope, select **Subscriptions**. You could instead select a resource group or resource.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/59.png)

2. Select the particular subscription (resource group or resource) to assign the application to.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/60.png)

3. Select **Access Control (IAM)**.

4. Select **Add**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/61.png)

5. Select **Contributor** role from dropdown list to assign to the application.

6. Search for your application by entering the name of the application in the Name field and select it from the searched results. 

7. Select **Save** to finish assigning the role. You see your application in the list of users assigned to a role for that scope.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/62.png)

## 6 ARM Template Input Parameters

| **Parameter Name**                               | **Description**                                                                                            | **Allowed Values**    | **Default Values**                                                                                                               
| -------------                                    | -------------                                                                                              | -----------------     | ------------ 
| **Location**           | specify the region for where the complete solution will deploy      | northeurope, southcentralus, southeastasia, westeurope, westus2, eastus, eastus2, australiasouthet,
 centralus, canadacentral                | westus2
| **Solution Type**                                | 1.core solution will launch the ams core components. 2. core solution with monitoring will launch the core components with monitoring. 3.core and hardening will launch the high availability solution. 4.core and hardening with monitoring will launch the high availabity solution with monitoring. | core solution, core solution with monitoring, core and hardening, core and hardening with monitoring   |    
| **locationDr**                                   | if you select core and hardening or core and hardening with monitoring specify the desaster recovery region for webapps and azure sqlserver,cosmos Db desaster recovary it should be different of resource group region     | eastasia, centralus, northcentralus, brazilsouth, australiaeast, southindia, westindia, canadaeast, ukwest, koreacentral    | centralus
| **sqlAdministratorLogin**   | The admin user of the SQL Server                              | Any string          | Sqluser
| **sqlAdministratorLoginPassword**   | The password of the admin user of the SQL Server   |                         | 
| **Website Name**  | Describes Web Site name which should be unique. Enter Website name which you entered in 5.1 section at 16th point (Eg:https://<WebsiteName>.azurewebsites.net/redirect.html) |           |
| **Website Name Dr**  | Describes Web Site name which should be unique for recovery app    |                                                 |
| **AD Subscription Id**    | Subscription ID of your Azure AD tenant.                                      |                                |
| **AD Tenant Id**          | Tenant ID of Azure AD.                                            |                                |
| **AD Client Id**                              | Client ID of Azure AD application.           |                     |
| **Ad Secret Key**                             | Secret Key of Azure AD application            |                     |
| **B2c Tenant**            | Describes B2C Tenant Name Directory              |                     |
| **B2c Client Id**         | Describes the client Id registered with B2C Directory.                     |                           |
| **B2c SignUp SignIn policy Id**               | Describes the B2C Sign Up-Sign In policy.                                      |                           | 
| **B2c Native Redirect URL**                   | Describes the B2C redirect URL for the Native Client.            |                     |
| **B2c Native Redirect URL Dr**                   | If you select costing model 4 specify b2cNativeRedirectURL describes the B2C redirect URL for the Native Client of disaster recovery web application       |    |
| **webSiteTrafficManagerName**             | Describes Web Site trafficmaanger name it should be same as the customdomain name prefix of certifacate of website if ypu select core solution or core solution with monitoring in solution type this value is optional  |                      |
| **apiServerTrafficManagerName**       | Describes apiserver trafficmaanger name it should be same as the customdomain name prefix of certifacate of apiserver if ypu select core solution or core solution with monitoring in solution type this value is optional            |                              |
| **nodeServerTrafficManagerName**            | Describes nodeserver trafficmaanger name it should be same as the customdomain name prefix of certifacate of apiserver if ypu select core solution or core solution
with monitoring in solution type this value is optional             |                |
| **keyVaultName**        | Existing Key Vault name with an access policy to allow Microsoft.Web RP to read Key Vault secrets          |                     | 
| **keyVaultwebAppSecretName**    | Describes the keyvault secret name of webapp certificate if you select core solution or core solution with monitoring in solution type this value is optional     |            |
| **keyVaultApiServerSecretName**    | Describes the keyvault secret name of webapp certificate if you select core solution or core solution with monitoring in solution type this value is optional  |             |
| **keyVaultNodeServerSecretName**   | Describes the keyvault secret name of webapp certificate if you select core solution or core solution with monitoring in solution type this value is optional   |   |
| **webAppCertificatethumbPrint**    | Describes the webapp certificate thumbprint if you select core solution or core solution with monitoring in solution type this value is optional   |         |
| **apiServerCertificatethumbPrint** | Describes the apiserver certificate thumbprint if you select core solution or core solution with monitoring in solution type this value is optional          |       |
| **nodeServerCertificatethumbPrint**     | Describes the nodeserver certificate thumbprint if you select core solution or core solution with monitoring in solution type this value is optional    |            |
                    
## 7 Getting Started

### 7.1 Deploying the ARM Template

1. Click below Git hub repo url.

**https://github.com/sysgain/ams-iot.git**

2. Select main-template from AmsWithExistingCertificates branch.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/tt.PNG)

3. Select Raw from the top right corner.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/t1.png)

4. Copy the raw template and paste in your azure portal for template deployment.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/t2.png)

**To deploy a template for Azure Resource Manager, follow the below steps**. 

1. Go to Azure portal.

2. Navigate to **Create a resource (+)**, search for Template deployment.

3. Click on **create** and click on **Build your own Template**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/t3.png)

4. The Edit template page is displayed as shown in the following figure. 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/t4.png)

5. Replace/paste the template and click on Save

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/t5.png)

6. The Custom deployment page is displayed as shown in the following figure.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q1.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q2.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q3.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q5.png)

**Parameters for core Solution with monitoring**

7. Deploy the template by providing the parameters in custom deployment settings as shown in the following figure. 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q6.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q7.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q8.png)

**Parameters for core Hardening and core hardening with monitoring**

**Note**: Deploy the template in the same Resource group in which you have created Key vault and Certificate

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q9.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q10.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q11.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q12.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/q13.png)


8. Once all the parameters are entered, click the terms and conditions check box and click Purchase.

9. After the successful deployment of the ARM template, the following resources are created in a Resource Group.

	* 2 App Service plan 
	* 6 App Services 
	* Storage account 
	* IoT HUB 
	* IoT Device provisioning service 
	* 2 SQL server 
	* 2 SQL database 
	* 2 Cosmos DB 
	* Event Hub 
	* Stream Analytics 
	* Application Insights 
	* OMS Workspace 
	* Traffic Manager 
	
10. Once the solution is deployed successfully navigate to the resource group, select the created resource group to view the list of resources that are created in the Resource Group as shown in the following figure. 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/t12.png)

Once the deployment was completed make sure that **SSL Configuration** should be **ON**. If it was **off** turn it to **ON**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/t13.png)

## 8 Prerequisites for Gateway-Middleware

1. Visual studio 2015 with c++ dependency.

2. Install **GitBash.**

https://git-scm.com/download/win

3. Install **BLE scanner** app in your mobile to view the sensor ID.

4. Install **ASTRA** app in your mobile.

 https://projectiot.blob.core.windows.net/ams-iot/AndroidMobileApplication/astra.apk

5. Install CSR 4.0 setup file from the below link to enable **BLE** dongle so that your system will act as a Gate way. 

https://projectiot.blob.core.windows.net/ams-iot/CSR_4.0_Bluetooth_exe/CSR 4.0 setup.zip

6. Download Zadig file from the below link.

https://zadig.akeo.ie/

7. Install PowerBI for Desktop  from the below link.

https://www.microsoft.com/en-in/store/p/power-bi-desktop/9ntxr16hnw1t?rtc=1

## 8.1 Step 1: Run the Zadig file

1. Connect the BLE dongle to your system and enable the Bluetooth.

2. Open the zadig file as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/72.png)

3. Go to options and check list all devices.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/73.png)

4. Select the CSR device from the drop down as shown below and click Replace Driver then it will start installing the driver.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/74.png)

5. After the successful installation of driver you will get the following page.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/75.png)

6. Again, select the CSR device from the drop down as shown below and click Reinstall Driver then it will start installing the driver.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/76.png)

7. After successful installation you will get the following page.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/77.png)

## 8.2 Step 2: Setup GatewayMiddleware package

Configure the Gateway from the below document.

**https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/documents/Configuring-the-GatewayMiddleware-Package-29-05-18.pdf**

## 8.3 Step 3: Configuring WEBAPP

1. To start the work flow of AMS take the **web app** or **Traffic manger URL** through portal.azure.com from the deployed resource group. 

2. Go to **Resource group** [Symbol]search for your **resource group name** [Symbol]then click on it. 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/n1.PNG)

3. Now you can able to see all the resources of that resource group.

4. You can differentiate the resources based on their types. For that choose **Group By Type** option as shown in below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/n2.PNG)

5. Now click on **Deployments** and select **Microsoft.Template**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/n3.PNG)

6. Now go to **Outputs** and copy the **web app URL**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/n4.PNG)

7. Now **paste** the copied URL in a browser to open the web application of the AMS.

8. Click **Sign In**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/83.png)

9. If you are new, use **sign-up** to login into the web app.(or)if your account is already existed then provide the credentials to **login**.

10. The web page will take few minutes to open(refresh the page).

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/84.png)

## 8.4 Step 4: Adding the pre-requisites in the web app.

1. Go to **inventory** option in web app.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/85.png)

2. The page shows the number of **gateways** and **sensors**. Here it shows total gateway and sensor counts.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/86.png)

### 8.4.1 Adding Gateway

3. Now click on **+Add New** to add a new gateway.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/87.png)

4. We need to configure all these fields to add a gateway.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/88.png)

5. Click on **update** so that we can able to add the new gateway.

6. Once we click on update we can able to see the pop up as unit configured successfully and open the **Add gateway page**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/89.png)

7. Enter the **gateway Name, Serial No (gateway key ID), Description** and then click on **submit**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/90.png)

8. You can able to see the pop up of **gateway added** and the total gateway count.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/91.png)

### 8.4.2 Adding Sensor

9. Click **+Add New** to add a new sensor.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/92.png)

10. Now you need to enter all the fields of sensor

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/93.png)

11. You need to enter the fields as follows and click on **submit.**

12. Open **BLE Scanner** in your mobile and **turn on** the **bluetooth**.

13. **Power on** your **Sensor** and start searching for **CC2650 SensorTag** in BLE scanner by refreshing it.

14. Click **Connect** then it will get connected.

15. In **Add Sensor** window, give the Name as you like.

16. Give **Serial No** that shows in the BLE Scanner under **CC2650 SensorTag** without colons and alphabet should be in lower case as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/94.png)

17. Choose your **Sensor tag** as the **Sensor type** as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/95.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/96.png)

### 8.4.3 Adding Asset to Web App using Mobile Application

1. Open the mobile app named as **ASTRA** and enter the **rest server URL**.

2. You can find the **rest server URL** from the azure portal as follows.

3. Go to **deployment** -> find the **Resource group name** -> **Deployments** -> **Microsoft.Template** -> **Outputs**.

4. Copy the **APISERVER URL**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/n5.PNG)

5. Note the **Api Server URL** and paste it in the mobile application without / at end and click **submit**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/99.png)

6. Now the mobile app page redirected to **microsoft login page**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/100.png)

7. Enter the credentials to **login** into application.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/101.png)

8. Now you can able to view the application page as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/102.png)

9. Click on **Dispatch** option to add an asset to the web portal.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/103.png)

10. Before adding asset to the webportal **generate qrcode** for your **sensor** and **barcode** for asset by using the following url’s.

    **Qrcode** -> https://www.barcodesinc.com/generator/qr 

    **Barcode** -> https://www.barcodesinc.com/generator/index.php

11. you need to add the **sensor** by using the **qrcode**. While generating the **Qrcode**, you need to enter your **Sensor ID** in text box and click **Create QR code**.

12. Then Scan the **QR code** in **ASTRA** app in your mobile.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/104.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/105.png)

13. Click on **next**.

14. Add asset to the web portal by scanning the barcode as follows.

15. Generate **Barcode** by entering any text in the text box and scan the **Barcode** in **ASTRA** app in your mobile

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/barcode.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/107.png)

16. Click **next**.

17. Now you need to **link** the asset with the sensor so that asset can be added to the web portal.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/108.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/109.png)

18. Go to web portal and check whether the asset has been added or not.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/110.png)

### 8.4.4 Adding Assets to a Group

19. Now we need to **add** the asset to a **group**. For that you need to check the asset so that **Add Group** option will be enable.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/111.png)

20. Click on **Add group** to add asset to a group.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/112.png)

21. Enter **name** and **description** of the group and click **submit**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/113.png)

22. You can able to see the **group** in the inventory option as follows

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/114.png)

### 8.4.5 Cofiguring the PoweBi Desktop App and Publishing

23. Go to **Configurations** and add the following information.

24. First, we need to enable the firewall of the sqlserver as follows.

25. Go to the resources and choose the resource as sqlserverà Go to firewalls and virtual networks field in the settings option.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/115.png)

26. Add **client IP** to enable the firewall.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/116.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/117.png)

27. click **save** option to save the firewall values.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/118.png)

28. Here you can see the successful updation of adding firewall.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/119.png)

29. To configure the **powerbi urls** and **credentials** first we need to configure the powerbi desktop as follows.

30. **Download the PowerBI template** from the below link.

https://projectiot.blob.core.windows.net/ams-iot/AMSLatestcode/HistoricalReport .pbit

31. **Run** the downloaded powerbi template and enter all the **input parameters**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/120.png)

32. Here the fields require,

    **sql server name**

    **Sql database**

    **Document DB url**

    **Document DB Name**

    **Document DB Collection Name**

33. All these values are taken from the azure portal.

34. Go to azure portal and choose your deployment, there you can find all the resources.

35. Now go to **Resource Group** -> **Deployments** -> **Microsoft.Template** -> **Outputs**.

36. **Copy** the **sql db name** and **Sql Server name**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/n6.PNG)

37. **Note** down the above two values.

38. Go to **deployment -> find the Resource group name -> Deployments -> Microsoft.Template -> Outputs**.

39. **Copy** and **Note down** the values of **document db, Collection** name and **data base name**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/n7.PNG)

40. Go to **keys** field in the settings option of document and note down the **Document DB url** and **primary key values**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/124.png)

41. Now enter all tehse values in powerbi desktop.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/125.png)

42. Click on **load**.

43. After loading it will ask for some additional information like cosmos DB account key there you can enter the primary key value of document DB.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/126.png)

44. Click on **connect**. A Pop-up occurs for sql authentication as follows. Here you need to choose the authentication type as **database**.
5![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/127.png)

45. Enter the **sql user name** and **password** and click **connect**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/128.png)

46. Click on **run** to load the db tables into the powerbi.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/129.png)

47. Here you can see the data fetching from db to powerbi.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/130.png)

48. Once entire data has been fetched the page can be appeared as follows.

49. Here you can click on **publish** button to publish the powerbi desktop url. Click **publish.**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/131.png)

50. Click on **save**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/132.png)

51. You can save the powerbi desktop into your local machine. For that, choose the file location to save.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/133.png)

52. After saving the content it will ask for the **destination**.Here, the default is workspace and click select.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/134.png)

53. Then the following **url** will be appeared.click on the **url** ,there you can find the report id of the powerbi.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/135.png)

54. The page can be appeared as follows and here we need to note down the id in between **reports** and **report section**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/136.png)

### 8.4.6 Configuring the flow in web app

55. Go to web app and click on **configuration** -> choose **powerbi credentials**

56. Enter the values of **powerbi client id, Secret key, username and password (Azure portal credentials).**

57. Click **submit**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/137.png)

58.	A message configuration added/updated is displayed on the bottom right corner as shown in the following figure.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/138.png)

59. Now open **powerbi url** and paste the published url id in the place of report id which you have noted down in **step 54** above..

**Example**: https://app.powerbi.com/reportEmbed?reportId=5a69ed50-c11f-4097-b608-3d9cf94eb6b8

60. click **submit**. A message **URL Updated** is displayed on the bottom right corner as shown in the following figure..

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/139.png)

## 8.5 Step 5: Running the gateway middleware

1. Go to **azure Portal** -> find the **Resource group name** -> **Deployments** -> **Microsoft.Template** -> **Outputs**.

2. **Copy** the **API Server URL**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/n8.PNG)

3. Paste it in the **Gateway window (Asset Monitoring Configuration page)**.

4. Click **submit**.

**Note:** If the Gateway window (Asset Monitoring Configuration page) is closed, run electron . command in gitbash then you will get the Gateway window (Asset Monitoring Configuration page).

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/142.png)

5. The page will be redirect to **Microsoft login page**.

6. Ignore the message by click on **ok**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/142.png)

7. Enter the **credentials** to login. Use the login credentials what we are using to sign up for web app.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/143.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/145.png)

8. Now close the gateway window and **run** the **electron .** in **gitbash**, so that it will automatically direct to the gateway page with all authentications.

**Note:** the **sensor** should be in **on**.

9. Here you can see the data coming from the gateway to **iot hub** via sensor.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/147.png)

### 8.5.1 Validating data in iot hub and Node server

10. Go to Azure Portal and click **IoT Hub** as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/147-1.png)

11. The data in **iot** can be appeared as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/148.png)

12. You can also see the **live data** in node server.

13.	Go to your **Resource Group** and click **nodeserver** as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/148-1.png)

14. To view you need to enable the **diagnostic log** settings as follows in **node server**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/149.png)

15. Go to **log stream** and see the **data** as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/150.png)

## 8.6 Step 6: validating the data in web app

1. To see the live data in web app go to **reports** -> select group followed by sensor value.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/151.png)

2. Choose **group name**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/152.png)

3. Choose **sensor name**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/153.png)

4. Here you can find the data coming from **iot hub** to **web application** via node server.

5. All the **capabilities** of sensor data can be viewd as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/154.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/155.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/156.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/157.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/158.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/159.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/160.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/161.png)

## 8.7 Step 7: Creating and validating the rule in Web app

1. After viewing the reports create a **rule** based on some threshold conditions.

2. For that go to rules click **+Add New**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/162.png)

3. Select the **group value** of assets.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/163.png)

4. You can set the values to some **threshold level**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/R1.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/r2.png)

5. While creating the rule, if you select **Vibration** or **Invert** then it will create **Stream analytics Job** for each. 

**Note:** Each Stream Analytics Job costs $80.30 

6. Click **done**.

7. You can see the created **rule** as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/166.png)

8. You can see the rules that we created by refreshing the webapp page and click on **rules**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/167.png)

9. Now go to **reports** and see the **capabilities** of sensor after adding the rule.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/168.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/169.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/170.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/171.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/173.png)


## 8.8 Step 8: Configuring the Indoor map in web app

1. Go to **configuration**,select **indoor map Configuration**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/176.png)

2. **Upload** your indoor map and click **Add.**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/177.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/178.png)

3. The map can be appeared as follows. The pop up says that **indoor map added**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/179.png)

### 8.8.1 Adding gateway rule

4. Now you need to select the **gateway id** in the indoor map location.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/180.png)

### 8.8.2 Positioning the gateway on the layout

5. Now **position** the gateway at some location in the map and click **update.**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/181.png)

6. Here you can see the pop up as **gateway mapped successfully**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/182.png)

### 8.8.3 Indoor alert notification	

7. Now Go to **dashboard** -> click on the **flip icon** as shown in the below screen shot.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/183.png)

8. Once you click the flip symbol, you can able to see the **gateway,sensor** and the **range** in between them.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/184.png)

9. Now click on the sensor colored as **yellow**, you can see all the capabilities of sensor.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/185.png)

### 8.8.4 Alerts checking

10. If any rule get **bleached** you found the alert as like above screen shot.

11. Go to **Alerts**,select the **group -> Asset -> capability** and click **apply**

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/186.png)

### 8.8.5 Asset Status

12. Finally, you can see the **status** of the asset by using **mobile application**.

13. Open **mobile app** and click on the **receive option**.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/187.png)

14. Now **scan** the **barcode** of the asset as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/barcode.png)

15. Then the **status** of asset can be appeared as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/189.png)

## 9 Monitoring Components 

### 9.1 OMS Log Analytics

1. Click on OMS Workspace in Resource Group to view OMS Overview Section.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/190.png)

2. Click on Azure Resources on left side menu to view available Azure Resources.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/191.png)

3. Select your RG name from the dropdown list.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/192.png)

4. Access OMS portal from OMS workspace on left side menu. Click on OMS Workspace > OMS Portal.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/193.png)

5. Once you clicked on OMS Workspace, the page will be redirected to OMS Home Page.

6. There you can see the Logs of Azure SQL and Azure Web apps by clicking on each tab.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/194.png)

7. Click Azure SQL Analytics to view the SQL Server logs.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/195.png)

8. Click sqldb on the left side page to view the detailed information.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/196.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/197.png)

9. Click Home on the left side of the page for Web Apps Analytics.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/198.png)

10. Click Azure Web apps Analytics tab to view each web application logs.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/199.png)

11. Click nodeserver for logs.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/200.png)

12. Go back and click webapplication for logs.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/201.png)

13. Go back and click nodeserver for logs.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/202.png)

14. Click Search tab to search the IoT hub, Event hub and Document DB logs.

15. Click Show legacy language converter.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/203.png)

16. Copy IoT Hub resource name, paste it in the Covert box and click RUN as shown below.

17. Once you clicked on RUN, you will get the IoT Hub information below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/204.png)

18. Copy Event Hub resource name, paste it in the Covert box and click RUN as shown below.

19. Once you clicked on RUN, you will get the Event Hub information below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/205.png)

20. Copy Cosmos DB resource name, paste it in the Covert box and click RUN as shown below.

21. Once you clicked on RUN, you will get the Cosmos DB information below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/206.png)

22. For Stream Analytics logs, first you need to enable the Diagnostics logs.

23. Go to Azure portal, click Stream Analytics job as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/207.png)

24. Click Diagnostics logs on the left pane and Turn on diagnostics as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/208.png)

25. Provide the details as shown below and select your workspace.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/209.png)

26. Click Save.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/210.png)

27. Go to OMS Portal and Click Search tab for Stream Analytics logs.

28. Copy Stream Analytics Job resource name, paste it in the Covert box and click RUN as shown below.

29. Once you clicked on RUN, you will get the Stream Analytics Job information below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/211.png)

### 9.2 Application Insights

1. Go to Azure portal, select your Resource Group and select Application Insights as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/212.png)

2. On Overview page, Summary details are displayed as shown in the following figure.

3. Click Live Stream to view detailed information related to webapp.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/213.png)

4. Here you can see the Live Requests of Web app.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/214.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/215.png)

5. Go back to Application Insights Overview page and click Analytics box in Health tab as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/216.png)

6. This will take you to Application Insights page and click Home Page tab.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/217.png)

7. You can run the following common queries to see the specific logs of application as below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/218.png)

8. For example, Run the Performance query to see the logs.

9. Click RUN on Performance tab.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/219.png)

10. You can see the below graph of application performance. If you modified the query please click on RUN from top left menu to see the updated graph.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/220.png)

11. Similarly, you can run the other common Pre-defined queries by navigating back to the Home Page.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/221.png)

12. Go back to the Application Insights overview page in Azure Portal to view metrics of the application.

13. Click Metrics Explorer on the left side of the page as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/222.png)

14. Click Edit as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/223.png)

15. You can select any of the listed Metrics to view application logs.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/224.png)

16. If you want to add new chart click on Add new chart as shown below and click on Edit to add the specific metrics.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/225.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/226.png)


## 10 Hardening Components

### 10.1 Geo Replication

#### 10.1.1 Setting up Geo-Replication for Cosmos DB

Azure Cosmos DB is a globally distributed, low-latency, high throughput databases services. Azure Cosmos DB provides global distribution, which means you can scale and distribute it across different Azure regions. This enables you to have your data replicated over as many as datacenter per your need, moreover control and access your replicated data seamlessly. Setting up the Geo-Replication is very easy and can be done in a couple of clicks from the Azure Portal.

Follow these steps to set up the Geo-Replication.

1. From the Azure Portal, go to your Resources Group and Open the Azure Cosmos DB database resource.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/227.png)

2. Select Replicate data globally under the Settings option.

3. In the initial state, the Global Distribution map will highlight the Write Region, which is the origin of the Cosmos DB database.

4. Now you can add additional region by simply clicking on Add New Region button which is available under the Read Regions section.

5. But here already one region is added, you can do Failover for it.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/228.png)

6. Click Manual Failover on the top.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/229.png)

7. Here, the Write Region is West US and Read Region is South Central US.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/230.png)

8. Click South Central US region to become a Write Region, Check I understand and agree to trigger a failover on my current Write Region box and click OK.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/231.png)

9. The overall process will take a while and it will depend on the number of regions you selected for your data to be replicated.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/232.png)

10. Once the Geo-Replication is done, you can go back and check all your regions on the Map, further you can add or remove any other regions as per your need.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/233.png)

#### 10.1.2 Setting up Geo-Replication for SQL DB

Azure SQL Database auto-failover groups (in-preview) is a SQL Database feature designed to automatically manage geo-replication relationship, connectivity, and failover at scale. With it, the customers gain the ability to automatically recover multiple related databases in the secondary region after catastrophic regional failures or other unplanned events that result in full or partial loss of the SQL Database service’s availability in the primary region.

To configure active geo-replication by using the Azure portal, you need the following resource:

* An Azure SQL database: The primary database that you want to replicate to a different geographical region.

* Active geo-replication must be between databases in the same subscription.

1. Go to Azure portal, select your Resource Group and select SQL Server as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/234.PNG)

2. Select Failover Groups under the Settings section.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/235.PNG)

3. Click SQL Server as show below.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/236.PNG)

4. Click Failover to switch Secondary database to Primary role. 

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/237.PNG)

5. Click YES.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/238.PNG)

6. After Successful Failover You can go back and check your SQL Servers status.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/239.PNG)

### 10.2 Traffic Manager

**Traffic Manager**

Traffic Manager is an Internet facing solution to load balance traffic between multiple service endpoints. Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services. Traffic Manager utilizes DNS queries and a policy engine to direct traffic to Internet resources. The Internet resource can be located in a single datacenter or across the globe.

**Traffic Manager routing methods**

Traffic-routing methods determine how to route network traffic to the various service endpoints. Traffic Manager applies the traffic-routing method to each DNS query it receives. The traffic-routing method determines which endpoint returned in the DNS response.

**There are four traffic routing methods available in Traffic Manager:**

* **Priority**: Select Priority when you want to use a primary service endpoint for all traffic, and provide backups in case the primary or the backup endpoints are unavailable. 

  By default, Traffic Manager sends all traffic to the primary (highest-priority) endpoint. If the primary endpoint is not available, Traffic Manager routes the traffic to the second endpoint.

* **Weighted**: Select Weighted when you want to distribute traffic across a set of endpoints, either evenly or according to weights, which you define.

  For each DNS query received, Traffic Manager randomly chooses an available endpoint. The probability of choosing an endpoint is based on the weights assigned to all available endpoints. Using the same weight across all endpoints results in an even traffic distribution.

* **Performance**: Select Performance when you have endpoints in different geographic locations and you want end users to use the "closest" endpoint in terms of the lowest network latency.

* **Geographic**: Select Geographic so that users are directed to specific endpoints (Azure, External, or Nested) based on which geographic location their DNS query originates from. 
  This empowers Traffic Manager customers to enable scenarios where knowing a user’s geographic region and routing them based on that is important.

**Traffic Manager End Point Monitoring**

* **Protocol**: Choose HTTP, HTTPS, or TCP as the protocol that Traffic Manager uses when probing your endpoint to check its health. HTTPS monitoring does not verify whether your SSL certificate is valid--it only checks that the certificate is present.

* **Port**: Choose the port used for the request.

* **Path**: This configuration setting is valid only for the HTTP and HTTPS protocols, for which specifying the path setting is required. Providing this setting for the TCP monitoring protocol results in an error. For TCP protocol, give the relative path and the name of the webpage or the file that the monitoring accesses. A forward slash (/) is a valid entry for the relative path. This value implies that the file is in the root directory (default).

* **Probing Interval**: This value specifies how often an endpoint is checked for its health from a Traffic Manager probing agent. You can specify two values here: 30 seconds (normal probing) and 10 seconds (fast probing). If no values are provided, the profile sets to a default value of 30 seconds. Visit the Traffic Manager Pricing page to learn more about fast probing pricing.

* **Tolerated Number of Failures**: This value specifies how many failures a Traffic Manager probing agent tolerates before marking that endpoint as unhealthy. Its value can range between 0 and 9. A value of 0 means a single monitoring failure can cause that endpoint to be marked as unhealthy. If no value is specified, it uses the default value of 3.

* **Monitoring Timeout**: This property specifies the amount of time the Traffic Manager probing agent should wait before considering that check a failure when a health check probe is sent to the endpoint. If the Probing Interval is set to 30 seconds, then you can set the Timeout value between 5 and 10 seconds. If no value is specified, it uses a default value of 10 seconds. If the Probing Interval is set to 10 seconds, then you can set the Timeout value between 5 and 9 seconds. If no Timeout value is specified, it uses a default value of 9 seconds.

Initially when both the node servers i.e primary and secondary are on you will be able to view the logs (data) for both the node servers.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m1.png)

You will also be able to see the live data in the webapp coming from the node server

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m2.png)

We can failover to the secondary node server by stopping the primary node sever Expected output is we should see the logs for the secondary node server, and the live data.In the webapp should come from the secondary node server.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m3.png)

In the following screenshots, The primary node server is turned off and we are able to see the data in the secondary node server logs

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m4.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m5.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m6.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m7.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m8.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m9.png)

We can view the live data in the webapp

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m10.png)

Similarly for the rest api ,we can failover to the secondary but still we can login to the webapp.

In the following screenshots, The primary node server is turned off and we are able to see the data in the secondary node server logs

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m11.png)

If one app of Api server is in ON and other should be off the result should be follows.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m12.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m13.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m14.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m15.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m16.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m17.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m18.png)

When one web app is in on Other should be off result of webapp as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m19.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m20.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m21.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m22.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m23.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m24.png)

![alt text](https://github.com/sysgain/ams-iot/raw/AmsWithExistingCertificates/images/m25.png)
