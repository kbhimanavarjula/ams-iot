# Microsoft

**Table of Contents** 

- [Architecture](#architecture)
- [Data Flow Architecture Diagram](#data-flow-architecture-diagram)
- [Prerequisites for Deploying ARM Template](#prerequisites-for-deploying-arm-template)
    - [Azure B2C Tenant Creation and Configuration](#azure-b2c-tenant-creation-and-configuration)
	- [	Power BI Configuration](#power-bi-configuration)
	- [Creating an Azure Service Principal](#creating-an-azure-service-principal)
- [Deploying the ARM Template](#deploying-the-arm-template)
- [Prerequisites for Gateway-Middleware](#prerequisites-for-gateway-middleware)
     - [Step 1 Configuring the Gateway-Middleware package](#step-1 configuring-the-gateway-middleware-package)
     - [Step 2 Configuring WEBAPP](#step-2 configuring-webapp)
     - [Step 3 Adding the pre-requisites in the web app](#step-3 adding-the-pre-requisites-in-the-web-app)
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

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/6.png)

7.	Provide the name and enter the details as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/7.png)

8.	Select all the Sign-up attributes as show below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/8.png)

9.	Select all the Application claims as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/9.png)

10.	After filling all the required details, click on Create.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/10.png)

11.	Once the deployment is complete, the below screen will appear with sign-up details.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/11.png)

12.	Click on Profile editing policies, then Add.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/12.png)

13. Provide a name and fill in the details as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/13.png)

14. Select all the Profile attributes and click on OK.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/14.png)

15. Select all the Application claims and then click on OK.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/15.png)

16. After filling all the required details, click on Create.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/16.png)

17. After deployment completes, the below screen will appear.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/17.png)

18. Click on Password reset policies and click Add.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/18.png)

19. Provide a name and fill in the details as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/19.png)

20. Select all the Application claims and then click on OK.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/20.png)

21. After filling the details, click on Create.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/21.png)

22. Once the deployment is completed, the below screen will appear.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/22.png)

23. Click on Sign-up policies and click on Add.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/23.png)

24. Provide the name of policy and fill the details as shown in the below screen.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/24.png)

25. Select all the Sign-up attributes as show below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/25.png)

26. Select all Application Claims as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/26.png)

27. Click on Create.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/27.png)

28. Once the deployment is completed, the below screen will appear.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/28.png)

29. Click on Sign-in policies, then Add.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/29.png)

30. Provide a name and fill in the details as shown below.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/30.png)

31. Select all Application claims and click ok

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/31.png)

32. Once done, click on Create.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/32.png)

33. After deployment completes, the below screen will appear.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/33.png)

34. Click on the Applications tab and click Add to create a new application. Provide a name for the application.

![alt text](https://github.com/sysgain/ams-iot/raw/core_components/images/34.png)
