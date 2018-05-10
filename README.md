# Microsoft

# Asset Monitoring Solution

**Table of Contents** 

- [1 About Asset Monitoring Solution](#1-about-asset-monitoring-solution)
- [2 Architecture](#2-architecture)
  - [2.1 Data Flow Architecture Diagram](#21-data-flow-architecture-diagram)
- [3 Prerequisites for Deploying ARM Template](#3-prerequisites-for-deploying-arm-template)
  - [3.1 Azure B2C Tenant Creation and Configuration](#31-azure-b2c-tenant-creation-and-configuration)
  - [3.2 Power BI Configuration](#32-power-bi-configuration)
  - [3.3 Creating an Azure Service Principal](#33-creating-an-azure-service-principal)
- [4 Deploying the ARM Template](#4-deploying-the-arm-template)
- [5 Prerequisites for Gateway-Middleware](#5-prerequisites-for-gateway-middleware)
- [6 Step 1 Run the Zadig file](#6-step-1-run-the-zadig-file)
- [7 Step 2 Setup GatewayMiddleware package](#7-step-2-setup-gatewaymiddleware-package)
- [8 Step 3 Configuring WEBAPP](#8-step-3-configuring-webapp)
- [9 Step 4 Adding the pre-requisites in the web app](#9-step-4-adding-the-pre-requisites-in-the-web-app)
	- [9.1 Adding Gateway](#91-adding-gateway)
	- [9.2 Adding Sensor](#92-adding-sensor)
	- [9.3 Adding Asset to Web App using Mobile Application](#93-adding-asset-to-web-app-using-mobile-application)
	- [9.4 Adding Assets to a Group](#94-adding-assets-to-a-group)
	- [9.5 Cofiguring the PoweBi Desktop App and Publishing](#94-cofiguring-the-powebi-desktop-app-and-publishing)
	- [9.6 Configuring the flow in web app](#96-configuring-the-flow-in-web-app)
- [10 Step 5 Running the gateway middleware](#10-step-5-running-the-gateway-middleware)
	- [10.1 Validating data in iot hub and Node server](#11-validating-data-in-iot-hub-and-node-server)
- [11 Step 6 validating the data in web app](#11-step-6-validating-the-data-in-web-app)
- [12 Step 7 Creating and validating the rule in Web app](#12-step-7-creating-and-validating-the-rule-in-web-app)
- [13 Step 8 Configuring the Indoor map in web app](#13-step-8-configuring-the-indoor-map-in-web-app)
	- [13.1 Adding gateway rule](#131-adding-sensor)
	- [13.2 Positioning the gateway on the layout](#132-positioning-the-gateway-on-the-layout)
  - [13.3 Indoor alert notification](#133-indoor-alert-notification)
  - [13.4 Alerts checking](#134-alerts-checking)
  - [13.5 Asset Status](#135-asset-status)
- [14 OMS Log Analytics](#14-oms-log-analytics)
- [15 Application Insights](#15-application-insights)
- [16 Geo Replication](#16-geo-replication)
  - [16.1 Setting up Geo Replication for Cosmos DB](#161-setting-up-geo-replication-for-cosmos-db)
  - [16.2 Setting up Geo Replication for SQL DB](#162-setting-up-geo-replication-for-sql-db)



## 1 About Asset Monitoring Solution

Asset Monitoring and Tracking Solution is a complete smart inventory management tool. The solution provides a web dashboard & a mobile application to Monitor, Locate and Report all the remote assets so that they are completely visible 24x7.

## 2 Architecture

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/1.jpg)

## 2.1 Data Flow Architecture Diagram

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/2.jpg)

## 3 Prerequisites for Deploying ARM Template

  1. The Azure AD B2C Tenant should be created and register your web application. 
  2. Create an account in Power BI 
  3. Create an Azure Service Principal. 

### 3.1 Azure B2C Tenant Creation and Configuration   

Creating Azure AD B2C tenant is a one-time activity, if you have a B2C Tenant already created by your admin then you should be added into that tenant as Global Administrator to register your app to get the B2C tenant id, application id and sign-in/sign-up policies.  

**Follow Below steps to create Azure AD B2C Tenant:**

1. Create a new B2C tenant in Azure Active Directory B2C. You'll be shown a page with the information on Azure Active Directory B2C. Click Create at the bottom to start configuring your new Azure Active Directory B2C tenant.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/3.png)

2. Choose the Organization name, Initial Domain name and Country of Region for your Tenant.

3. Note down your entire Tenant name which is highlighted in the below screenshot, this will be used while deploying the ARM template.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/4.png)

4. Once the B2C Tenant is created, Click Directory and Subscription filter on the top right to see your newly created tenant.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/5.png)

5. Switch to your created tenant by clicking on it. Type Azure in search column and select Azure AD B2C.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/6.png)

6. You can see the created tenant overview like below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/7.png)

7.	Click on sign-up or sign-in policies. Then click on Add to add policy.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/8.png)

8.	Provide the name and enter the details as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/9.png)

9.	Select all the Sign-up attributes as show below.

10.	Note down the policy name that you are creating now, this will be used while deploying the template.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/10.png)

11.	Select all the Application claims as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/11.png)

12.	After filling all the required details, click on Create.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/12.png)

13.	Once the deployment is complete, the below screen will appear with sign-up details.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/13.png)

14. Click on the Applications tab and click Add to create a new application.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/36.png)

15.	Provide a name for the application.

16.	Under the Web APP/Web API tab, click Yes to provide the following two redirect URLs for your application. Add an entry in the Redirect URLs section of the B2C application in the following format.

•	https://<**Website Name**>.azurewebsites.net/redirect.html

Note: **Website Name** should be different from **application name.**

•	http://localhost:65159/redirect.html

17.	During the web app registration with PowerBI, you will use this reply URL.

**Example: https://webappiot.azurewebsites.net/redirect.html**

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/36-1.png)

18. Click Yes under the Native client to include the native client url as shown below.

Eg: com.onmicrosoft.<**tenant name**>.<**application name**>://redirect/path

com.onmicrosoft.**amsiot1**.**webapp**://redirect/path

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/36-2.png)

19.	Before clicking on create, note down the application name, Reply URL’s and Custom Redirect URI.

20. After that, click on Create. This web app is used for authenticating the Asset management user login/ registration.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/37.png)


21. Select the application you created and note down the Application ID.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/38.png)


### 3.2 Power BI Configuration

Go to https://dev.powerbi.com/apps and register the web app.

a. Login to your Power BI account with the Azure Login credentials that have Global admin permissions.

b. Provide a name for your web app (This is different from what we created before).

c. Select App type “server-side Web App”.

d. Enter the Redirected URL and Home URL, same as you gave in Azure AD B2C tenant URL without “/redirect.html” for Home URL.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/40.png)

e. Select check boxes for required API’s (select all check boxes for best practice).

* Read all datasets

* Read and write all data sets

* Read all dashboards

* Read all reports

* Read and Write all reports

* Read all Groups

* Create content

f. Click on Register App.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/41.png)

g. The Client id and secret key will be generated. Note down these keys locally, as you will use these later in the configuration.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/42.png)

2. Go to Azure Active Directory from Your Azure Account and click on the App registrations tab. Select the app you just created in PowerBI.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/43.png)

**NOTE:** To grant permissions to the app you must be a **Global Administrator** in the Tenant.

3. Click on the app, navigate to all settings, and give the Required permissions.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/44.png)

4. Enable the following access under delegated permissions in Windows Azure Active Directory.

* Access the directory as the signed in users

* Read directory data

* Read and write all groups

* Read all user’s basic profiles

* Sign in and read user profile

After that click on **Save**

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/45.png)

5. Enable the following access under delegated permissions in Power BI access.

* View all datasets

* View all dashboards

* View content properties

* View all reports

* Create content

* View user groups

* Read and write all datasets

* Read and write all reports

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/46.png)

6. The user can see the number of permissions which have been added.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/47.png)

7. Click on **Grant Permissions**, then click **Yes**.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/48.png)

### 3.3 Creating an Azure Service Principal

To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.

Note down the following ID's once you create the application in Azure Active Directory. You need to enter these details while deploying the ARM template.

o Subscription ID - **You can get the subscription ID in the Azure**

o Tenant ID

o Client ID

o Client Secret 

1. Go to Azure portal..

2. Select **Azure Active Directory**.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/49.png)

3. Select **App registrations**

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/50.png)

4. Select **New application registration**

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/51.png)

5. Provide a name and URL for the application. Select either **Web app / API** or **Native** for the type of application you want to create. After setting the values, select **Create**.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/52.png)

6. You have created your application.

**Get application ID and authentication key**

When programmatically logging in, you need the ID for your application and an authentication key. To get those values, use the following steps:

1. From App registrations in Azure Active Directory, select your application

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/53.png)

2. Copy the Application ID and store it in a secure place. This application ID also refers as the client id.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/54.png)

3. To generate an authentication key, goto settings select Keys.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/55.png)

4. Provide a description of the key, and a duration for the key. When done, select Save.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/56.png)

5. After saving the key, the value of the key is displayed. Copy this value because you are not able to retrieve the key later. You provide the    key value with the application ID to log in as the application. Store the key value where your application can retrieve it.

**Get tenant ID**

When programmatically logging in, you need to pass the tenant ID with your authentication request.

1. To get the tenant ID, select Properties for your Azure AD tenant.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/57.png)

2. Copy the Directory ID. This value is your tenant ID.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/58.png)

**Assign application to role**

To access resources in your subscription, you must assign the application to a role. Make sure that it has the contributor role in your Azure subscription, which allows you to create and delete resources.

1. Navigate to the level of scope you wish to assign the application to. For example, to assign a role at the subscription scope, select **Subscriptions**. You could instead select a resource group or resource.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/59.png)

2. Select the particular subscription (resource group or resource) to assign the application to.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/60.png)

3. Select Access Control (IAM).

4. Select Add.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/61.png)

5. Select Contributor role to assign to the application.

6. Search for your application, and select it.

7. Select **Save** to finish assigning the role. You see your application in the list of users assigned to a role for that scope.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/62.png)

## 4 Deploying the ARM Template

1. Click below Git hub repo url.

**https://github.com/sysgain/ams-iot.git**

2. Take the main-template.json raw file from testing1 branch. 

3. Go to Azure portal.

4. Navigate to **Create a resource (+)**, search for Template deployment.

5. Click on **create** and click on **Build your own Template**.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/63.png)

6. Replace the template and click on Save

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/64.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/65.png)

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

•	Webapp Name 			        – Enter Website name which you entered in 3.1 section at 16th point (Eg: https://<**Website Name**>.azurewebsites.net/redirect.html)

•	Node Server 			        - Give user defined name.

•	Api Server 			          - Give user defined name.

•	B2C Tenant 			          – Name of the B2C Tenant which you created in 3.1 section at 3rd point. (Eg: amsiot1.onmicrosoft.com)

•	B2C Client id 			      – Enter B2C Client id (Application id) that you got after creating the B2C application in 3.1 section at 21st point.

•	B2C Sign Up Sign In Policy Id 	– Enter Sign Up Sign In Policy name which you created 3.1 section at 8th point.

•	B2C native Redirect URL 	      -  Enter B2C native Redirect URL which you entered while creating the web application in B2C tenant in 3.1 section at 18th point.

•	Ad Subscription Id 		    – Enter your Azure account subscription Id.

•	Ad Tenant Id 			        – Enter your Azure account tenant Id.

•	Ad Client Id 			        – Enter the Client Id that you got from the Azure Active Directory Application in 3.3 section at 2nd point(Get application ID and authentication key).

•	Ad Secret key 			      - Enter the Secret key that you got from the Azure Active Directory Application in 3.3 section at 4th point(Get application ID and authentication key).


![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/66.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/67.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/68.png)

8. Once all the parameters are entered, click the terms and conditions check box and click Purchase.

9. Once the deployment is completed, you can start the workflow

## 5 Prerequisites for Gateway-Middleware

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

## 6 Step 1: Run the Zadig file

1. Connect the BLE dongle to your system and enable the Bluetooth.

2. Open the zadig file as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/72.png)

3. Go to options and check list all devices.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/73.png)

4. Select the CSR device from the drop down as shown below and click Replace Driver then it will start installing the driver.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/74.png)

5. After the successful installation of driver you will get the following page.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/75.png)

6. Again, select the CSR device from the drop down as shown below and click Reinstall Driver then it will start installing the driver.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/76.png)

7. After successful installation you will get the following page.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/77.png)

## 7 Step 2: Setup GatewayMiddleware package

Configure the Gateway from the below document.

https://github.com/sysgain/ams-iot/raw/core_components/documents/Configuring%20the%20GatewayMiddleware%20Package.pdf

## 8 Step 3: Configuring WEBAPP

1. To start the work flow of AMS take the web app URL through portal.azure.com from the deployed resource group.

2. Go to Resource groupàsearch for your resource group name àthen click on it.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/79.png)

3. Now you can able to see all the resources of that resource group.

4. You can differentiate the resources based on their types. For that choose **Group By Type** option as shown in below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/80.png)

5. Now click on the name of the web app that you entered while deploying the template so that you can find the web app URL and copy that URL.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/81.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/82.png)

6. Now paste the copied URL in a browser to open the web application of the AMS.

7. Click Sign In.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/83.png)

8. If you are new, use sign-up to login into the web app.(or)if your account is already existed then provide the credentials to login.

9. The web page will take few minutes to open(refresh the page).

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/84.png)

## 9 Step 4: Adding the pre-requisites in the web app.

1. Go to inventory option in web app.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/85.png)

2. The page shows the number of gateways and sensors. Here it shows total gateway and sensor counts.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/86.png)

### 9.1 Adding Gateway

3. Now click on +Add New to add a new gateway.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/87.png)

4. We need to configure all these fields to add a gateway.(leave them as default)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/88.png)

5. Click on update so that we can able to add the new gateway.

6. Once we click on update we can able to see the pop up as unit configured successfully and open the Add gateway page.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/89.png)

7. Enter the gateway Name(user defined), Serial No (gateway key ID), Description and then click on submit.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/90.png)

8. You can able to see the pop up of gateway added and the total gateway count.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/91.png)

### 9.2 Adding Sensor

9. Click +Add New to add a new sensor.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/92.png)

10. Now you need to enter all the fields of sensor

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/93.png)

11. You need to enter the fields as follows and click on **submit.**

12. Open **BLE Scanner** in your mobile and turn on the bluetooth.

13. Power on your **Sensor** and start searching for **CC2650 SensorTag** in BLE scanner by refreshing it.

14. Click **Connect** then it will get connected.

15. In **Add Sensor** window, give the Name as you like.

16. Give **Serial No** that shows in the BLE Scanner under **CC2650 SensorTag** without colons and alphabet should be in lower case as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/94.png)

17. Choose your Sensor tag as the Sensor type as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/95.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/96.png)

### 9.3 Adding Asset to Web App using Mobile Application

1. Open the mobile app named as **ASTRA** and enter the **rest server URL**.

2. You can find the rest server URL from the azure portal as follows.

3. Go to deployment àfind the resource group name, there you can find the apiserveràclick on the api server and note the url of the rest server.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/97.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/98.png)

4. Note the rest server URL and paste it in the mobile application and click submit

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/99.png)

5. Now the mobile app page redirected to microsoft login page.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/100.png)

6. Enter the credentials to login into application.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/101.png)

7. Now you can able to view the application page as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/102.png)

8. Click on Dispatch option to add an asset to the web portal.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/103.png)

9. Before adding asset to the webportal generate **qrcode** for your sensor and barcode for asset by using the following url’s.

    **Qrcode** -> https://www.barcodesinc.com/generator/qr 

	  **Barcode** -> https://www.barcodesinc.com/generator/index.php

10. you need to add the sensor by using the **qrcode**. While generating the Qrcode, you need to enter your **Sensor ID** in text box and click **Create QR code**.

11. Then Scan the **QR code** in **ASTRA** app in your mobile.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/104.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/105.png)

12. Click on **next**.

13. Add asset to the web portal by scanning the barcode as follows.

14. Generate **Barcode** by entering any text in the text box and scan the **Barcode** in **ASTRA** app in your mobile

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/106.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/107.png)

15. Click next.

16. Now you need to link the asset with the sensor so that asset can be added to the web portal.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/108.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/109.png)

17. Go to web portal and check whether the asset has been added or not.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/110.png)

### 9.4 Adding Assets to a Group

18. Now we need to add the asset to a group. For that you need to check the asset so that Add Group option will be enable.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/111.png)

19. Click on Add group to add asset to a group.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/112.png)

20. Enter name and description of the group and click submit.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/113.png)

21. You can able to see the group in the inventory option as follows

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/114.png)

### 9.5 Cofiguring the PoweBi Desktop App and Publishing


22. Go to Configurations and add the following information.

23. First, we need to enable the firewall of the sqlserver as follows.

24. Go to the resources and choose the resource as sqlserverà Go to firewalls and virtual networks field in the settings option.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/115.png)

25. Add client IP to enable the firewall.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/116.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/117.png)

26. click save option to save the firewall values.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/118.png)

27. Here you can see the successful updation of adding firewall.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/119.png)

28. To configure the powerbi urls and credentials first we need to configure the powerbi desktop as follows.

29. Download the PowerBI template from the below link.

https://projectiot.blob.core.windows.net/ams-iot/AMSLatestcode/HistoricalReport .pbit

30. Run the downloaded powerbi template and enter all the input parameters.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/120.png)

31. Here the fields require,

    **sql server name**

    **Sql database**

    **Document DB url**

    **Document DB Name**

    **Document DB Collection Name**

32. All these values are taken from the azure portal.

33. Go to azure portal and choose your deployment, there you can find all the resources.

34. Now click on sqldb, so that you can find the sql server name and sql db name as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/121.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/122.png)

35. Note down the above two values.

36. Go to document db and note down the values of Collection name and data base name.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/123.png)

37. Go to keys field in the settings option of document and note down the Document DB url and primary key values.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/124.png)

38. Now enter all tehse values in powerbi desktop.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/125.png)

39. Click on load.

40. After loading it will ask for some additional information like cosmos DB account key there you can enter the primary key value of document DB.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/126.png)

41. Click on connect. A Pop-up occurs for sql authentication as follows. Here you need to choose the authentication type as database.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/127.png)

42.	Enter the SQL username and password which you have entered while deploying the template, click connect.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/128.png)

43. Click on run to load the db tables into the powerbi.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/129.png)

44. Here you can see the data fetching from db to powerbi.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/130.png)

45. Once entire data has been fetched the page can be appeared as follows.

46. Here you can click on publish button to publish the powerbi desktop url. Click **publish.**

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/131.png)

47. Click on **save**.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/132.png)

48. You can save the powerbi desktop into your local machine. For that, choose the file location to save.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/133.png)

49. After saving the content it will ask for the destination.Here, the default is workspace and click select.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/134.png)

50. Then the following url will be appeared.click on the **url** ,there you can find the report id of the powerbi.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/135.png)

51. The page can be appeared as follows and here we need to note down the id in between reports and report section

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/136.png)

### 9.6 Configuring the flow in web app

52. Go to web app and click on **configuration** -> choose **powerbi credentials**

53. Enter the values of **powerbi client id, Secret key, username and password (Azure portal credentials).**

54. Click **submit**.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/137.png)

55. Here you can see the pop up saying configuration added/updated.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/138.png)

56.	Now open powerbi url and paste the published url id in the place of report id which you have noted down in 8.5 section at 51st point.

Example: https://app.powerbi.com/reportEmbed?reportId=5a69ed50-c11f-4097-b608-3d9cf94eb6b8

57. click **submit**. There you can see the successful adding of URL.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/139.png)

## 10 Step 5: Running the gateway middleware

1. Go to portal àclick on apiserverà copy the apiserver URL.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/140.png)

2. Paste it in the gateway window(Asset Monitoring Configuration page) and add / at the end as shown below.

3. Click submit.

**Note:** If the gateway window(Asset Monitoring Configuration) page is closed, run electron . command in gitbash then you will get the gateway window(Asset Monitoring Configuration page).

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/141.png)

4. The page will be redirect to Microsoft login page.

5. Ignore the message by click on ok

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/142.png)


6. Enter the credentials to login. Use the login credentials what we are using to sign up for web app.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/143.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/145.png)

7. Now close the gateway window and run the electron . in gitbash, so that it will automatically direct to the gateway page with all authentications.

**Note:** the sensor should be in on.

8. Here you can see the data coming from the gateway to iot hub via sensor.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/147.png)

### 10.1 Validating data in iot hub and Node server

9. Go to Azure Portal and click IoT Hub as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/147-1.png)

10. The data in iot can be appeared as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/148.png)

11. You can also see the live data in node server.

12.	Go to your Resource Group and click nodeserver as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/148-1.png)

13. To view you need to enable the diagnostic log settings as follows in node server.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/149.png)

14. Go to log stream and see the data as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/150.png)

## 11 Step 6: validating the data in web app

1. To see the live data in web app go to reports -> select group followed by sensor value.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/151.png)

2. Choose group name.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/152.png)

3. Choose sensor name.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/153.png)

4. Here you can find the data coming from iot hub to web application via node server.

5. All the capabilities of sensor data can be viewd as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/154.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/155.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/156.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/157.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/158.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/159.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/160.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/161.png)

## 12 Step 7: Creating and validating the rule in Web app

1. After viewing the reports create a rule based on some threshold conditions.

2. For that go to rules click +Add New.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/162.png)

3. Select the group value of assets.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/163.png)

4. You can set the values to some threshold level.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/164.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/165.png)

5. Click done.

6. You can see the created rule as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/166.png)

7. You can see the rules that we created by refreshing the webapp page and click on rules.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/167.png)

8. Now go to reports and see the capabilities of sensor after adding the rule.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/168.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/169.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/170.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/171.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/173.png)


## 13 Step 8: Configuring the Indoor map in web app

1. Go to configuration,select indoor map Configuration

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/176.png)

2. Upload your indoor map and click **Add.**

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/177.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/178.png)

3. The map can be appeared as follows. The pop up says that indoor map added.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/179.png)

### 13.1 Adding gateway rule

4. Now you need to select the gateway id in the indoor map location.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/180.png)

### 13.2 Positioning the gateway on the layout

5. Now position the gateway at some location in the map and click **update.**

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/181.png)

6. Here you can see the pop up as gateway mapped successfully.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/182.png)

### 13.3 Indoor alert notification	

7. Now Go to dashboard -> click on the flip icon as shown in the below screen shot.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/183.png)

8. Once you click the flip symbol, you can able to see the gateway,sensor and the range in between them.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/184.png)

9. Now click on the sensor colored as yellow, you can see all the capabilities of sensor.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/185.png)

### 13.4 Alerts checking

10. If any rule get bleached you found the alert as like above screen shot.

11. Go to Alerts,select the group -> Asset -> capability and click **apply**

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/186.png)

### 13.5 Asset Status

12. Finally, you can see the status of the asset by using mobile application.

13. Open mobile app and click on the receive option.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/187.png)

14. Now scan the barcode of the asset as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/106.png)

15. Then the status of asset can be appeared as follows.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/189.png)


## 14 OMS Log Analytics

1.	Click on OMS Workspace in Resource Group to view OMS Overview Section.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/190.png)

2.	Click on Azure Resources on left side menu to view available Azure Resources.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/191.png)

3.	Select your RG name from the dropdown list.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/192.png)

4.	Access OMS portal from OMS workspace on left side menu. Click on OMS Workspace > OMS Portal.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/193.png)

5.	Once you clicked on OMS Workspace, the page will be redirected to OMS Home Page.

6.	There you can see the Logs of Azure SQL and Azure Web apps by clicking on each tab.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/194.png)

7.	Click Azure SQL Analytics to view the SQL Server logs.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/195.png)

8.	Click sqldb on the left side page to view the detailed information.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/196.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/197.png)

9.	Click Home on the left side of the page for Web Apps Analytics.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/198.png)

10.	Click Azure Web apps Analytics tab to view each web application logs.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/199.png)

11.	Click nodeserver for logs.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/200.png)

12.	Go back and click webapplication for logs.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/201.png)

13.	Go back and click nodeserver for logs.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/202.png)

14.	Click Search tab to search the IoT hub, Event hub and Document DB logs.

15.	Click Show legacy language converter.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/203.png)

16.	Copy IoT Hub resource name, paste it in the Covert box and click RUN as shown below.

17.	Once you clicked on RUN, you will get the IoT Hub information below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/204.png)

18.	Copy Event Hub resource name, paste it in the Covert box and click RUN as shown below.

19.	Once you clicked on RUN, you will get the Event Hub information below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/205.png)

20.	Copy Cosmos DB resource name, paste it in the Covert box and click RUN as shown below.

21.	Once you clicked on RUN, you will get the Cosmos DB information below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/206.png)

22.	For Stream Analytics logs, first you need to enable the Diagnostics logs.

23.	Go to Azure portal, click Stream Analytics job as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/207.png)

24.	Click Diagnostics logs on the left pane and Turn on diagnostics as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/208.png)

25.	Provide the details as shown below and select your workspace.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/209.png)

26.	Click Save.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/210.png)

27.	Go to OMS Portal and Click Search tab for Stream Analytics logs.

28.	Copy Stream Analytics Job resource name, paste it in the Covert box and click RUN as shown below.

29.	Once you clicked on RUN, you will get the Stream Analytics Job information below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/211.png)


## 15 Application Insights

1.	Go to Azure portal, select your Resource Group and select Application Insights as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/212.png)

2.	On Overview page, Summary details are displayed as shown in the following figure.

3.	Click Live Stream to view detailed information related to webapp.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/213.png)

4.	Here you can see the Live Requests of Web app.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/214.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/215.png)

5.	Go back to Application Insights Overview page and click Analytics box in Health tab as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/216.png)

6.	This will take you to Application Insights page and click Home Page tab.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/217.png)

7.	You can run the following common queries to see the specific logs of application as below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/218.png)

8.	For example, Run the Performance query to see the logs.

9.	Click RUN on Performance tab.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/219.png)

10.	You can see the below graph of application performance. If you modified the query please click on RUN from top left menu to see the updated graph.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/220.png)

11.	Similarly, you can run the other common Pre-defined queries by navigating back to the Home Page.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/221.png)

12.	Go back to the Application Insights overview page in Azure Portal to view metrics of the application.

13.	Click Metrics Explorer on the left side of the page as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/222.png)

14.	Click Edit as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/223.png)

15.	You can select any of the listed Metrics to view application logs.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/224.png)

16.	If you want to add new chart click on Add new chart as shown below and click on Edit to add the specific metrics.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/225.png)

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/226.png)


## 16 Geo Replication

### 16.1 Setting up Geo-Replication for Cosmos DB

Azure Cosmos DB is a globally distributed, low-latency, high throughput databases services. Azure Cosmos DB provides global distribution, which means you can scale and distribute it across different Azure regions. This enables you to have your data replicated over as many as datacenter per your need, moreover control and access your replicated data seamlessly. Setting up the Geo-Replication is very easy and can be done in a couple of clicks from the Azure Portal.

Follow these steps to set up the Geo-Replication.

1. From the Azure Portal, go to your Resources Group and Open the Azure Cosmos DB database resource.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/227.png)

2. Select Replicate data globally under the Settings option.

3. In the initial state, the Global Distribution map will highlight the Write Region, which is the origin of the Cosmos DB database.

4. Now you can add additional region by simply clicking on Add New Region button which is available under the Read Regions section.

5. But here already one region is added, you can do Failover for it.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/228.png)

6. Click Manual Failover on the top.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/229.png)

7. Here, the Write Region is West US and Read Region is South Central US.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/230.png)

8. Click South Central US region to become a Write Region, Check I understand and agree to trigger a failover on my current Write Region box and click OK.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/231.png)

9. The overall process will take a while and it will depend on the number of regions you selected for your data to be replicated.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/232.png)

10. Once the Geo-Replication is done, you can go back and check all your regions on the Map, further you can add or remove any other regions as per your need.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/233.png)


## 16.2	Setting up Geo-Replication for SQL DB

Azure SQL Database auto-failover groups (in-preview) is a SQL Database feature designed to automatically manage geo-replication relationship, connectivity, and failover at scale. With it, the customers gain the ability to automatically recover multiple related databases in the secondary region after catastrophic regional failures or other unplanned events that result in full or partial loss of the SQL Database service’s availability in the primary region.

To configure active geo-replication by using the Azure portal, you need the following resource:

•	An Azure SQL database: The primary database that you want to replicate to a different geographical region.

•	Active geo-replication must be between databases in the same subscription.

1. Go to Azure portal, select your Resource Group and select SQL Server as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/234.PNG)

2. Select Failover Groups under the Settings section.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/235.PNG)

3. Click SQL Server as show below.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/236.PNG)

4. Click Failover to switch Secondary database to Primary role. 

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/237.PNG)

5. Click YES.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/238.PNG)

6. After Successful Failover You can go back and check your SQL Servers status.

![alt text](https://github.com/sysgain/ams-iot/raw/Monitoring_ha/images/239.PNG)