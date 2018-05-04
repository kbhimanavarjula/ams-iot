# Microsoft

**Table of Contents** 

- [Architecture](#Architecture)
- [Data Flow Architecture Diagram](#data-flow-architecture-diagram)
- [Prerequisites for Deploying ARM Template](#prerequisites-for-deploying-arm-template)
        - [Azure B2C Tenant Creation and Configuration](#azure-b2c-tenant-creation-and-configuration)
		- [	Power BI Configuration](#power-bi-configuration)
		- [Creating an Azure Service Principal](#creating-an-azure-service-principal)
- [Deploying the ARM Template](#deploying-the-arm-template)
- [Prerequisites for Gateway-Middleware](#prerequisites-for-gateway-middleware)
- [Step 1: Configuring the Gateway-Middleware package](#step-1:configuring-the-gateway-middleware-package)
- [Step 2: Configuring WEBAPP](#step-1:configuring-webapp)
- [Step 3: Adding the pre-requisites in the web app](#adding-the-pre-requisites-in-the-web-app)
		- [Adding Gateway](#adding-gateway)
		- [Adding Sensor](#adding-sensor)
		- [Adding Asset to Web App using Mobile Application](#adding-asset-to-Web-app-using-mobile-application)
		- [Adding Assets to a Group](#adding-assets-to-a-group)
		- [Cofiguring the PoweBi Desktop App and Publishing](#cofiguring-the-powebi-desktop-app-and-publishing)
		- [Configuring the flow in web app](#configuring-the-flow-in-web-app)
- [Step 4: Running the gateway middleware](#step-4:running-the-gateway-middleware)
		- [Validating data in iot hub and Node server](#validating-data-in-iot-hub-and-node-server)
- [Step 5: validating the data in web app](step-5:validating-the-data-in-web-app)
- [Step 6: Creating and validating the rule in Web app](#step-6:creating-and-validating-the-rule-in-web-app)
- [Step 7: Configuring the Indoor map in web app](#step-7:configuring-the-indoor-map-in-web-app)
		- [Adding Sensor](#adding-sensor)
		- [Adding Asset to Web App using Mobile Application](#adding-asset-to-Web-app-using-mobile-application)









## Architecture

![alt text](https://raw.githubusercontent.com/sysgain/ams-iot/core_components/images/Architecture_Diagram.jpg?token=AT3nZlb0JsizUqjXdO1PcEpvhJZyyafVks5a9UmOwA%3D%3D)

## Data Flow Architecture Diagram

![alt text](https://raw.githubusercontent.com/sysgain/ams-iot/core_components/images/DataflowArchitectureDiagram.jpg?token=AT3nZlYe4LDYIaQk2p3xFGtgZ8nczgf8ks5a9UnUwA%3D%3D)

## Prerequisites for Deploying ARM Template

  1. The Azure AD B2C Tenant should be created and register your web application. 
  2. Create an account in Power BI 
  3. Create an Azure Service Principal. 

## Azure B2C Tenant Creation and Configuration   

Creating Azure AD B2C tenant is a one-time activity, if you have a B2C Tenant already created by your admin then you should be added into that tenant as Global Administrator to register your app to get the B2C tenant id, application id and sign-in/sign-up policies.  

**Follow Below steps to create Azure AD B2C Tenant:**

1. Create a new B2C tenant in Azure Active Directory B2C. You'll be shown a page with the information on Azure Active Directory B2C. Click Create at the bottom to start configuring your new Azure Active Directory B2C tenant.

![alt text](https://raw.githubusercontent.com/sysgain/ams-iot/core_components/images/1.png?token=AT3nZh7xYeK7ChLfgDAyOGibJKGw_Kj1ks5a9WAXwA%3D%3D)

2. Choose the Organization name, Initial Domain name and Country of Region for your Tenant. 

![alt text](https://raw.githubusercontent.com/sysgain/ams-iot/core_components/images/2.png?token=AT3nZjL5Bs8aemZ5zz0Mp0qdY0hTQHyyks5a9WBhwA%3D%3D)

3. Once the B2C Tenant is created, you will see the below confirmation under the portal login user name.

![alt text](https://raw.githubusercontent.com/sysgain/ams-iot/core_components/images/3.png?token=AT3nZqM1TMLN2Uop00yGy-ohVKNvYTfEks5a9WB4wA%3D%3D)

4. Switch to your created tenant by clicking on it under sign out. Type Azure in search column and select Azure AD B2C.

![alt text](https://raw.githubusercontent.com/sysgain/ams-iot/core_components/images/4.png?token=AT3nZlLzXHPbCwmaWtxxkAzHphdz9X4cks5a9WCOwA%3D%3D)

5. You can see the created tenant overview like below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/5.png)

6.	Click on Sign-up or sign-in policies. Then click on Add to add policy.

![alt text]()

7.	Provide the name and enter the details as shown below.

![alt text]()

8.	Select all the Sign-up attributes as show below.

![alt text]()

9.	Select all the Application claims as shown below.

![alt text]()

10.	After filling all the required details, click on Create.

![alt text]()

11.	Once the deployment is complete, the below screen will appear with sign-up details.

![alt text]()

12.	Click on Profile editing policies, then Add.

![alt text]()

13. Provide a name and fill in the details as shown below.

![alt text]()

14. Select all the Profile attributes and click on OK.

![alt text]()

15. Select all the Application claims and then click on OK.

![alt text]()

16. After filling all the required details, click on Create.

![alt text]()

17. After deployment completes, the below screen will appear.

![alt text]()

18. Click on Password reset policies and click Add.

![alt text]()

19. Provide a name and fill in the details as shown below.

![alt text]()

20. Select all the Application claims and then click on OK.

![alt text]()

21. After filling the details, click on Create.

![alt text]()

22. Once the deployment is completed, the below screen will appear.

![alt text]()

23. Click on Sign-up policies and click on Add.

![alt text]()

24. Provide the name of policy and fill the details as shown in the below screen.

![alt text]()

25. Select all the Sign-up attributes as show below.

![alt text]()

26. Select all Application Claims as shown below.

![alt text]()

27. Click on Create.

![alt text]()

28. Once the deployment is completed, the below screen will appear.

![alt text]()

29. Click on Sign-in policies, then Add.

![alt text]()

30. Provide a name and fill in the details as shown below.

![alt text]()

31. Select all Application claims and click ok

![alt text]()

32. Once done, click on Create.

![alt text]()

33. After deployment completes, the below screen will appear.

![alt text]()

34. Click on the Applications tab and click Add to create a new application. Provide a name for the application.

![alt text]()

35. Under the Web APP/Web API tab, click on Yes to provide a redirect URL for your application. Add an entry in the Redirect URLs section of the B2C application in the followingformat. https://<nameofthewebapp>.azurewebsites.net/redirect.html http://localhost:65159/redirect.html

36. Click Yes under the Native client to include the native client url

**Eg: com.onmicrosoft.<tenant name>.<application name>://redirect/path**

com.onmicrosoft.amsiot1.webapp://redirect/path

37. During the web app registration with PowerBI, we will use this reply URL. **Example: https://webappiot.azurewebsites.net/redirect.html**

38. After that, click on Create. This web app is used for authenticating the Asset management user login/ registration.

![alt text]()

39. When you save that application, it will generate a unique application id and be used while deploying ARM template.

40. Select the application you created and note down the Application ID.

![alt text]()

41. Then click on Keys > Generate key > Save and Copy the secret key.

![alt text]()

## Power BI Configuration

Go to https://dev.powerbi.com/apps and register the web app.

a. Login to your Power BI account with the Azure Login credentials that have Global admin permissions.

b. Provide a name for your web app (This is different from what we created before).

c. Select App type “server-side Web App”.

d. Enter the Redirected URL and Home URL, same as you gave in Azure AD B2C tenant URL without “/redirect.html” for Home URL.

![alt text]()

e. Select check boxes for required API’s (select all check boxes for best practice).

* Read all datasets

* Read and write all data sets

* Read all dashboards

* Read all reports

* Read and Write all reports

* Read all Groups

* Create content

f. Click on Register App.

![alt text]()

g. The Client id and secret key will be generated. Note down these keys locally, as you will use these later in the configuration.

![alt text]()

2. Go to Azure Active Directory from Your Azure Account and click on the App registrations tab. Select the app you just created from the list.

![alt text]()

**NOTE:** To grant permissions to the app you must be a Global Administrator in the Tenant.

3. Click on the app, navigate to all settings, and give the Required permissions.

![alt text]()

4. Enable the following access under delegated permissions in Windows Azure Active Directory.

* Access the directory as the signed in users

* Read directory data

* Read and write all groups

* Read all user’s basic profiles

* Sign in and read user profile

After that click on **Save**

![alt text]()

5. Enable the following access under delegated permissions in Power BI access.

* View all datasets

* View all dashboards

* View content properties

* View all reports

* Create content

* View user groups

* Read and write all datasets

* Read and write all reports

![alt text]()

6. The user can see the number of permissions which have been added.

![alt text]()

7. Click on **Grant Permissions**, then click **Yes**.

![alt text]()

## Creating an Azure Service Principal

To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.

Obtain the following Azure credentials for Cloudera Director:

o Subscription ID - **You can get the subscription ID in the Azure**

o Tenant ID

o Client ID

o Client Secret 1. Log in to your Azure Account through the Azure portal.

2. Select **Azure Active Directory**.

![alt text]()

3. Select **App registrations**

![alt text]()

4. Select **New application registration**

![alt text]()

5. Provide a name and URL for the application. Select either **Web app / API** or **Native** for the type of application you want to create. After setting the values, select **Create**.

![alt text]()

6. You have created your application.

### Get application ID and authentication key

When programmatically logging in, you need the ID for your application and an authentication key. To get those values, use the following steps:

1. From App registrations in Azure Active Directory, select your application

![alt text]()

2. Copy the Application ID and store it in a secure place. This application ID also refers as the client id.

![alt text]()

3. To generate an authentication key, goto settings select Keys.

![alt text]()

4. Provide a description of the key, and a duration for the key. When done, select Save.

![alt text]()

5. After saving the key, the value of the key is displayed. Copy this value because you are not able to retrieve the key later. You provide the    key value with the application ID to log in as the application. Store the key value where your application can retrieve it.

### Get tenant ID

When programmatically logging in, you need to pass the tenant ID with your authentication request.

1. To get the tenant ID, select Properties for your Azure AD tenant.

![alt text]()

2. Copy the Directory ID. This value is your tenant ID.

![alt text]()

### Assign application to role

To access resources in your subscription, you must assign the application to a role. Make sure that it has the contributor role in your Azure subscription, which allows you to create and delete resources.

1. Navigate to the level of scope you wish to assign the application to. For example, to assign a role at the subscription scope, select **Subscriptions**. You could instead select a resource group or resource.

![alt text]()

2. Select the particular subscription (resource group or resource) to assign the application to.

![alt text]()

3. Select Access Control (IAM).

4. Select Add.

![alt text]()

5. Select Contributor role to assign to the application.

6. Search for your application, and select it.

7. Select **Save** to finish assigning the role. You see your application in the list of users assigned to a role for that scope.

![alt text]()

## Deploying the ARM Template

1. Click on below Git hub repo url. **https://github.com/sysgain/ams-iot.git**

2. Take the main-template.json raw file from testing1 branch. 

3. Log into Azure portal **https://portal.azure.com**

4. Navigate to **Create a resource (+)**, search for Template deployment.

5. Click on **create** and click on **Build your own Template**.

![alt text]()

6. Replace the template and click on Save

![alt text]()

![alt text]()

7. Deploy the template by providing the following parameters in custom deployment settings.

![alt text]()

![alt text]()

![alt text]()

8. Once all the parameters are entered, click the terms and conditions check box and click Purchase.

9. Once the deployment is completed, you can start the workflow

## Prerequisites for Gateway-Middleware

1. Visual studio 2015 with c++ dependency.

2. Python with 2.7 vesrion.

3. Nodejs with latest version. (present version 9.11.1)

4. Install **BLE scanner** app in your mobile to view the sensor ID.

5. Install ASTRA app in your mobile. https://projectiot.blob.core.windows.net/ams-iot/AndroidMobileApplication/astra.apk

6. Install CSR 4.0 setup file from the below link to enable **BLE** dongle so that your will act as a Gate way. https://projectiot.blob.core.windows.net/ams-iot/CSR_4.0_Bluetooth_exe/CSR 4.0 setup.zip

7. Download Zadig file from the below link. https://zadig.akeo.ie/

## Step 1: Run the Zadig file

1. Connect the BLE dongle to your system and enable the Bluetooth.

2. Open the zadig file as shown below.

![alt text]()

3. Go to options and check list all devices.

![alt text]()

4. Select the CSR device from the drop down as shown below and click Replace Driver then it will start installing the driver.

![alt text]()

5. After the successful installation of driver you will get the following page.

![alt text]()

6. Again, select the CSR device from the drop down as shown below and click Reinstall Driver then it will start installing the driver.

![alt text]()

7. After successful installation you will get the following page.

![alt text]()

## Step 2: Setup GatewayMiddleware package

Configure the GatewayMiddleware from the below document. https://github.com/sysgain/ams-iot/raw/core_components/documents/Configuring%20the%20GatewayMiddleware%20Package.pdf

## Step 3: Configuring WEBAPP

1. To start the work flow of AMS take the web app URL through portal.azure.com from the deployed resource group.

2. Go to Resource groupàsearch for your resource group name àthen click on it.

![alt text]()

3. Now you can able to see all the resources of that resource group.

4. You can differentiate the resources based on their types. For that choose **Group By Type** option as shown in below.

![alt text]()

5. Now click on the name of the web app that you entered while deploying the template so that you can find the web app URL and copy that URL.

![alt text]()

![alt text]()

6. Now paste the copied URL in a browser to open the web application of the AMS.

7. Click Sign In.

![alt text]()

8. If you are new, use sign-up to login into the web app.(or)if your account is already existed then provide the credentials to login.

9. The web page will take around 5 to 10 minutes to open.

![alt text]()

## Step 4: Adding the pre-requisites in the web app.

1. Go to inventory option in web app.

![alt text]()

2. The page shows the number of gateways and sensors. Here it shows total gateway and sensor counts.

![alt text]()

## Adding Gateway

3. Now click on +Add New to add a new gateway.

![alt text]()

4. We need to configure all these fields to add a gateway.

![alt text]()

5. Click on update so that we can able to add the new gateway.

6. Once we click on update we can able to see the pop up as unit configured successfully and open the Add gateway page.

![alt text]()

7. Enter the gateway Name, Serial No (gateway key ID), Description and then click on submit.

![alt text]()

8. You can able to see the pop up of gateway added and the total gateway count.

![alt text]()

## Adding Sensor

9. Click +Add New to add a new sensor.

![alt text]()

10. Now you need to enter all the fields of sensor

![alt text]()

11. You need to enter the fields as follows and click on **submit.**

12. Open **BLE Scanner** in your mobile and turn on the bluetooth.

13. Power on your **Sensor** and start searching for **CC2650 SensorTag** in BLE scanner by refreshing it.

14. Click **Connect** then it will get connected.

15. In **Add Sensor** window, give the Name as you like.

16. Give **Serial No** that shows in the BLE Scanner under **CC2650 SensorTag** without colons and alphabet should be in lower case as shown below.

![alt text]()

17. Choose your Sensor tag as the Sensor type as shown below.

![alt text]()
![alt text]()

## Adding Asset to Web App using Mobile Application

1. Open the mobile app named as **ASTRA** and enter the **rest server URL**.

2. You can find the rest server URL from the azure portal as follows.

3. Go to deployment àfind the resource group name, there you can find the apiserveràclick on the api server and note the url of the rest server.

![alt text]()

![alt text]()

4. Note the rest server URL and paste it in the mobile application and click submit

![alt text]()

5. Now the mobile app page redirected to microsoft login page.

![alt text]()

6. Enter the credentials to login into application.

![alt text]()

7. Now you can able to view the application page as follows.

![alt text]()

8. Click on Dispatch option to add an asset to the web portal.

![alt text]()

9. Before adding asset to the webportal generate **qrcode** for your sensor and barcode for asset by using the following url’s. 
       **Qrcode** -> https://www.barcodesinc.com/generator/qr 
	   **Barcode** -> https://www.barcodesinc.com/generator/index.php

10. you need to add the sensor by using the **qrcode**. While generating the Qrcode, you need to enter your **Sensor ID** in text box and click **Create QR code**.

11. Then Scan the **QR code** in **ASTRA** app in your mobile.

![alt text]()

![alt text]()

12. Click on **next**.

13. Add asset to the web portal by scanning the barcode as follows.

14. Generate **Barcode** by entering any text in the text box and scan the **Barcode** in **ASTRA** app in your mobile

![alt text]()

![alt text]()

15. Click next.

16. Now you need to link the asset with the sensor so that asset can be added to the web portal.

![alt text]()

![alt text]()

17. Go to web portal and check whether the asset has been added or not.

![alt text]()

## Adding Assets to a Group

18. Now we need to add the asset to a group. For that you need to check the asset so that Add Group option will be enable.

![alt text]()

19. Click on Add group to add asset to a group.

![alt text]()

20. Enter name and description of the group and click submit.

![alt text]()

21. You can able to see the group in the inventory option as follows

![alt text]()

## Cofiguring the PoweBi Desktop App and Publishing


22. Go to Configurations and add the following information.

23. First, we need to enable the firewall of the sqlserver as follows.

24. Go to the resources and choose the resource as sqlserverà Go to firewalls and virtual networks field in the settings option.

![alt text]()

25. Add client IP to enable the firewall.

![alt text]()

![alt text]()

26. click save option to save the firewall values.

![alt text]()

27. Here you can see the successful updation of adding firewall.

![alt text]()

28. To configure the powerbi urls and credentials first we need to configure the powerbi desktop as follows.

29. Download the PowerBI template from the below link. https://projectiot.blob.core.windows.net/ams-iot/AMSLatestcode/HistoricalReport .pbit

30. Run the downloaded powerbi template and enter all the input parameters.

![alt text]()

31. Here the field require sql server name,

Sql database,

Document DB url,

Document DB Name,

Document DB Collection Name.

32. All these values are taken from the azure portal.

33. Go to azure portal and choose your deployment, there you can find all the resources.

34. Now click on sqldb, so that you can find the sql server name and sql db name as follows.

![alt text]()

![alt text]()

35. Note the above two values.

36. Go to document db and note down the values of Collection name and data base name.

![alt text]()

37. Go to keys field in the settings option of document and note down the Document DB url and primary key values.

![alt text]()

38. Now enter all tehse values in powerbi desktop.

![alt text]()

39. Click on load.

40. After loading it will ask for some additional information like cosmos DB account key there you can enter the primary key value of document DB.

![alt text]()

41. Click on connect. A Pop-up occurs for sql authentication as follows. Here you need to choose the authentication type as database.

![alt text]()

42. Enter the sqldb name and password and click connect.

![alt text]()

43. Click on run to load the db tables into the powerbi.

![alt text]()

44. Here you can see the data fetching from db to powerbi.

![alt text]()

45. Once entire data has been fetched the page can be appeared as follows.

46. Here you can click on publish button to publish the powerbi desktop url.fpr that click on **publish.**

![alt text]()

47. Click on **save**.

![alt text]()

48. You can save the powerbi desktop into your local machine.for that choose the file location to save.

![alt text]()

49. After saving the content it will ask for the destination.here the default is workspace and click select.

![alt text]()

50. Then the following url will be appeared.click on the **url** ,there you can find the report id of the powerbi.

![alt text]()

51. The page can be appeared as follows and here we need to note down the id in between reports and report section

![alt text]()

## Configuring the flow in web app

52. Go to web app and click on **configuration** -> choose **powerbi credentials**

53. Enter the values of **powerbi client id, Secret key, username and password (Azure portal credentials).**

54. Click **submit**.

![alt text]()

55. Here you can see the pop up saying configuration added/updated.

![alt text]()

56. Now open **powerbi url** and paste the published url id in the place of report id.

Example: https://app.powerbi.com/reportEmbed?reportId=5a69ed50-c11f-4097-b608-3d9cf94eb6b8

57. click **submit**. There you can see the successful adding of URL.

![alt text]()

## Step 5: Running the gateway middleware

1. Go to portal àclick on apiserverà copy the apiserver URL.

![alt text]()

2. Paste it in the Asset Monitoring Configuration page and add / at the end as shown below.

3. Click submit.

**Note:** If the Asset Monitoring Configuration page is closed, run electron . command in gitbash then you will get the Asset Monitoring Configuration page.

![alt text]()

4. The page will be redirect to Microsoft login page.

5. Ignore the message by click on ok

![alt text]()

![alt text]()

6. Enter the credentials to login. Use the login credentials what we are using to sign up for web app.

![alt text]()

![alt text]()

7. Now close the gateway window and run the electron . in gitbash, so that it will automatically direct to the gateway page with all authentications.

**Note:** the sensor should be in on.

8. Here you can see the data coming from the gateway to iot hub via sensor.

![alt text]()

## Validating data in iot hub and Node server

9. The data in iot can be appeared as follows.

![alt text]()

10. You can also see the live data in node server.

11. To view you need to enable the diagnostic log settings as follows in node server.

![alt text]()

12. Go to log stream and see the data as follows.

![alt text]()

## Step 6: validating the data in web app

1. To see the live data in web app go to reportsàselect group followed by sensor value.

![alt text]()

2. Choose group name.

![alt text]()

3. Choose sensor name.

![alt text]()

4. Here you can find the data coming from iot hub to web application via node server.

5. All the capabilities of sensor data can be viewd as follows.

![alt text]()

![alt text]()

![alt text]()

![alt text]()

![alt text]()

![alt text]()

![alt text]()

![alt text]()

## Step 7: Creating and validating the rule in Web app

1. After viewing the reports create a rule based on some threshold conditions.

2. For that go to rules click +Add New.

![alt text]()

3. Select the group value of assets.

![alt text]()

4. You can set the values to some threshold level.

![alt text]()

![alt text]()

5. Click done.

6. You can see the created rule as follows.

![alt text]()

7. You can see the rules that we created by refreshing the webapp page and click on rules.

![alt text]()

8. Now go to reports and see the capabilities of sensor after adding the rule.

![alt text]()

![alt text]()

![alt text]()

![alt text]()

![alt text]()

![alt text]()

![alt text]()

![alt text]()

## Step 8: Configuring the Indoor map in web app

1. Go to configurationàselect indoor map Configuration

![alt text]()

2. Choose the map from the given file (image).and click add.

![alt text]()

![alt text]()

3. The map can be appeared as follows. The pop up says that indoor map added.

![alt text]()

## Adding gateway rule

4. Now you need to select the gateway id in the indoor map location.

![alt text]()

## Positioning the gateway on the layout

5. Now position the gateway at some location in the map and click **update.**

![alt text]()

6. Here you can see the pop up as gateway mapped successfully.

![alt text]()

## Indoor alert notification	

7. Now Go to dashboard àclick on the flip icon as shown in the below screen shot.

![alt text]()

8. Click on the flip symbol so that you can able to see the gateway,sensor and the range in between them.

![alt text]()

9. Now click on the sensor colored as yellow, you can see all the capabilities of sensor.

![alt text]()

## Alerts checking

10. If any rule get bleached you found the alert as like above screen shot.

11. Go to Alerts àselect the groupàAssetàcapability and click **apply**

![alt text]()

## Asset Status

12. Finally, you can see the status of the asset by using mobile application.

13. Open mobile app and click on the receive option.

![alt text]()

14. Now scan the barcode of the asset as follows.

![alt text]()

15. Then the status of asset can be appeared as follows.

![alt text]()

