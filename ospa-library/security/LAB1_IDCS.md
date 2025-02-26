 ![](./media/securitytitle.png)
# Lab 1:  Oracle Identity Cloud Service

## Table of Contents

- [Module 1: User Management](#module-1--user-management)
- [Module 2: Configure SSO and Provisioning for Salesforce](#module-2--configure-sso-and-provisioning-for-salesforce)

***** 

**Disclaimer:  This lab is designed ONLY for large learning groups and assumes the groups are sharing the Oracle Cloud environment to execute this lab.**

## Mama Maggy's Identity Management business needs

Shannon Kim, Director/Manager of IT is seeking to reduce users and privileges' provisioning timeframe while improving security controls and governance.
Mama Maggy's current Identity Management solution cannot scale to the cloud.
Line-of-business has complained about the number of user ids and passwords that they must manage across its heterogeneous environment.
CIO has identified an exponential trend on the help desk calls for user ids and passwords reset since they have starting to move the workload to the cloud, so he asked Shannon to implement a solution that can help them not only consolidate on-premises and Cloud services user management but also help them to improve productivity and user experience.
Mama Maggy has acquired Oracle Identity Cloud Services to manage their enterprise infrastructure, regardless if its in the cloud or on-prem. 
As part of the new project, the CIO office is looking to implement Single Sign-On with their main SaaS applications, which will reduce not only the help desk calls but the average login timeframe.
You as the IdM Manager must set up Oracle Identity Cloud Service to allow users to log in to third-party services using Open Standards and to manage user id and privileges provisioning.


 
# Lab Configuration and Details

For the workshop lab exercises, the current version of the Oracle Identity Cloud Service (IDCS) is being demonstrated.
 
This workshop is hosted in the Oracle Public Cloud (OPC). It includes a combination of cloud services, hosted on-premises software and 3rd party software. Aside from the Identity Cloud Service, the remaining components are included to enable demonstrating integration, including identity synchronization, federation, authentication, SSO and more.

This workbook is primarily designed to provide the necessary instructions and context to allow you to complete the labs in the Oracle Identity Cloud Service Workshop. If you would like additional information about the Oracle solution, you can contact your local Oracle account team and/or review some of the following publicly available information about the solution.

Due to environment privileges constraints, user id creation/modification/deletion and application registration assignments have been already implemented in this tenant.
The instructor will guide you through the process of creating a new account and onboarding a new application into IDCS. These steps have been highlighted within this workshop for your reference.
The tasks labeled as **DEMO** will be instructor guide, while the exercises labeled as **EXERCISE** are assignments that you as the learner must complete.


The following summarizes the components in our workshop:
 

  * [Oracle Identity Cloud Service](https://cloud.oracle.com/en_US/identity)

  * Salesforce – used for IDCS Application Integration and CASB Create
    and Monitor a sanctioned Application use-cases

 The following configuration information is provided to assist with
 accessing lab assets:

  * Workshop Actors
    
      * IDCS End Users (e.g. employees, customers, partners, etc.)
    
      * IDCS Administrators

*NOTE: This lab contains two main modules with optional exercises. Due to timing constraints, we encourage you to complete first the mandatory modules and then go back to the optional tasks.*

# Overview: Oracle Identity Cloud Service

## Introduction

 Identity Cloud Service is Oracle’s next generation comprehensive security and identity platform that provides an innovative, fully integrated service that delivers all the core identity and access management capabilities through a Cloud platform “as a service. The design of Identity Cloud Service (IDCS) is based on micro service architecture which is naturally aligned with Cloud principles of Scalability, Elasticity, Resilience, Ease of Deployment, Functional Agility, Technical Adoption and Organization Alignment.
 
 At high level, Oracle Identity Cloud Service offers the following functionalities:

  * Identity & Access Management

  * Integration with on-prem Active Directory or 3rd party Identity
    Systems

  * Single-Sign-On (SSO)

  * User Authentication Service

  * Identity Federation service (SAML)

  * OAuth services

  * Auditing & Reporting Services

### Concepts and Terminology

  * **OAUTH 2.0** – OAUTH is a standard protocol for delegating authorization. It’s a way for an entity to be authorized to access resources (services, API, data) stored in a remote provider. For example, an on-premises application might leverage the IDCS REST API to retrieve information about users or groups from IDCS for use within its application. The REST API is protected by the OAUTH service, to ensure the client application is registered and authorized to a specific scope of REST API. Thus, OAUTH prevents internet-visible services (such as IDCS REST API) from being consumed by an unauthorized user or application.

  * **SAML 2.0** – SAML stands for *Security Assertion Mark-up Language*. It is a standard for federating user authentication. SAML defines two participating entities, the Service Provider and the Identity Provider. When a user attempts to access an application or service (at the Service Provider) which is configured for SAML, rather than log the user in through local ID/PW, the SP causes the user authentication to be performed by the Identity Provider. There is therefore a trust relationship established between SP and IDP. Oracle IDCS can be configured to take the role of Service Provider and/or Identity Provider. As a service provider, IDCS enables self-service profile management, password reset, etc.

  * **Identity Provider (IdP)** – This type of provider, also known as an Identity Assertion provider, provides identifiers for users who want to interact with Oracle Identity Cloud Service using a website that's external to Oracle Identity Cloud Service.

  * **Service Provider (SP)** - Third-party actor who provides a service. Offers application services but does not act as identity provider.

  * **Federation** - Federation in identity management enables two or more partners to work together, exchanging identity information securely across internet domains providing secure single sign-on (SSO). Common to a SAML federation are the concepts of identity provider (IdP) and service provider (SP)


# Business Drivers

 In new competitive business landscape organizations are trying to launch new services in a quickest timeframe to take early bird advantage. They want to reach out to more *users* and endorse their brand through social media. They want to launch mobile applications to give better services to their *customers* and get competitive advantage. Most of these organizations are developing and hosting these services using PaaS/SaaS model so that can avoid hassles of developing or managing them in-house.
 
 Security is one of the most critical and important aspects for every new initiative. Data loss & leakage risks, unauthorized access through ***misuse of credentials*** and ***improper access controls***, hijacking of accounts and malicious insiders are some of the biggest concerns that are always present in the ever faster delivery of these
 new services.
 
 Identity & Access Management (IAM) can provide a single aggregated view of identities to all systems, it enables multi-channel access and provides a platform to define and enforce policies at one layer to ensure consistency. An important consideration for these organizations is to define how IAM is implemented for these new initiatives/services. They can implement security for each application in a monolithic, distinct and unique fashion for that application or they can leverage a platform approach which can give them a shared single identity across multiple applications, shared services, and
 shared policies across multiple applications and provide cross channel visibility. The ability to enable business and drive new opportunities through a solid secure infrastructure and a platform designed for this kind of business agility is where the new business opportunity lies today.
 
 This workshop shows how **Oracle Identity Cloud Service (IDCS)** enable organizations to rapidly develop fast, reliable and secure services for their new business initiatives.

### **DEMO** - Navigation between IDCS and Cloud My Services Dashboards

During the following exercises we will cover the following Personas:
 
 * IDCS Administrator
 * IDCS End User
 
 Let’s first get used to how to access IDCS from within Oracle’s Cloud console and how to move between the two dashboards.
 
 * Login to your Oracle Cloud Account:
 [Login to your Cloud Account](https://cloud.oracle.com/en_US/sign-in)

![](./media/idcs5.jpeg)
<p align="center"> Figure 1-1 </p>

 * On the login page, enter your user name and password and click **Sign In**
 
 * You will be presented with a dashboard displaying the various cloud services available to this account.
 
 ![](./media/idcs6.png)
 <p align="center"> Figure 1-2 </p>
 
 * From the **Cloud My Services** dashboard, click on **Users** in the upper right-hand corner. Then click on **Identity Console** button located towards upper right-hand corner again.

![](./media/idcs7.png)
<p align="center"> Figure 1-3 </p>

 * If you have logged in using your administrator Account, the users are shown up in IDCS admin console. Other admin console sections are also available.
 
 ![](./media/idcs8.jpeg)
 <p align="center"> Figure 1-4 </p>
 
 * In the upper left-hand corner select the navigator menu or sometimes referred to as the "General Menu”. Select **Dashboard**. This will display the **Identity Cloud Service** dashboard.
 
 * Click on the navigator menu to hide it.

![](./media/idcs9.jpeg)
<p align="center"> Figure 1-5 </p>

* To return to the Cloud Console, do the following:

  *  Select the **My Home** menu from the upper right corner of the
    screen.

![](./media/idcs10.jpeg)
<p align="center"> Figure 1-6 </p>

  *  Then select the Dashboard button at top right of screen. This will
    return you to the **Cloud My Services** dashboard. Or just use your
    bookmarked URL as suggested earlier.

 ![](./media/idcs11.jpeg)
 <p align="center"> Figure 1-7 </p>

# IDCS Quick Tour

 Return to the IDCS dashboard and click on the navigator menu
 (hamburger menu).

![](./media/idcs12.jpeg)
<p align="center"> Figure 1-8 </p>

 You may navigate around IDCS from the dashboard screen items or through the menu on the left. Note the **My Services** link at the bottom of the menu list. This provides a shortcut to **Cloud My Services** dashboard.
 
 The IDCS documentation may be accessed through the **Learn More** button on the dashboard.
 
 Click on the following menus and just get familiar with the content:

  * Users

  * Groups

  * Settings

  * Security

 We’ll get into the details shortly, but this will give you a quick
 navigation overview of the menus and services available.

# Module 1:  User Management

 It is often a requirement for organizations to on-board an employee or contractor or some identity manually into a central identity systems like IDCS. In this use case, an IDCS user administrator will manually add a new user in IDCS service. Typically, this would occur through automated provisioning, bulk flat-file import or synchronization with your on- premises Active Directory.
 
 The IDCS features are built 100% using the IDCS REST API service. Therefore, any task we perform interactively in the web interface could also be performed via custom app, using these same REST API calls. It’s a clear advantage of Oracle’s API-first architecture with IDCS.
 
 IDCS supports user (also groups) on-boarding from on-premises **Active Directory**, using file upload, REST API, on-premises **Oracle Identity Management** solution, or manually from IDCS admin console. For the workshop we will be using file upload option and API calls user management.

### **DEMO** - Create User in UI (Persona: Administrator)

*  Go to IDCS Admin console using your administrator account credentials. Select the **Users** menu on the left and click **+Add** or select the **Add a user** icon from the dashboard.

![](./media/idcs13.png)
<p align="center"> Figure 1-9 </p>

*  Fill in all required fields and click **Finish**. For this lab purposes, create a dummy account using your personal email address (e.g. *name@gmail.com*). We will use this account as part of our Single Sign-On module.

 ![](./media/idcs14.png)
 <p align="center"> Figure 1-10 </p>

*  Verify user creation
    
      * Go to the **Users** tab in admin console. Verify that the new users are visible on the console.

 ![](./media/idcs15.jpeg)
 <p align="center"> Figure 1-11 </p>

****

## API User administration with REST API’s (Persona: Administrator)


The following exercise has been developed to showcase IDCS API capabilities.
This use case involves making API calls to IDCS using a REST client; in this case Postman. The Postman collection of relevant REST API calls is provided to each participant.

*NOTE: If you don't have POSTMAN installed in your system, please visit [POSTMAN Website](https://www.getpostman.com/products) download and install it following the site instructions.*


### **DEMO** - Register a client POSTMAN application in IDCS

*  Navigate to your tenant https://**yourtenant**/ui/v1/adminconsole
 
 ![](./media/idcs23.jpeg)
 <p align="center"> Figure 1-12 </p>

*  Select the Applications tab from the IDCS dashboard presented after log in

![](./media/idcs24.png)
<p align="center"> Figure 1-13 </p>

*  Click the **Add** button to create a new application for Postman use. In order for Postman to be able to call IDCS REST APIs, it first requires to have a **CLIENT_ID** and **CLIENT_SECRET** that authorize Postman to do so. This can be achieved by creating a Confidential Application type into IDCS with specific authorization grant types as you will see into the following steps.

 ![](./media/idcs25.jpeg)
 <p align="center"> Figure 1-14 </p>

*  Select Confidential Application from the pop-up menu of application types:

![](./media/idcs26.jpeg)
<p align="center"> Figure 1-15 </p>

*  Set the **Name** to “Postman”. Then click **Next**

 ![](./media/idcs27.jpeg)
 <p align="center"> Figure 1-16 </p>

*  Click “**Configure this application as a client now**” in order toprovide the authorization grant types and the API role.

![](./media/idcs28.jpeg)
<p align="center"> Figure 1-17 </p>

![](./media/idcs29.jpeg)
<p align="center"> Figure 1-18 </p>

*  Select all the Allowed Grant Types checkboxes and set Redirect URL to [**https://localhost.**](https://localhost/) Go to “**Grant the client access to Identity Cloud Service Admin APIs**” section (bottom of the page) and add the following API role “**Identity Domain Administrator**”. This way you are basically granting access for this IDCS app to the full set of IDCS APIs.

*  Finally, click **Next**.

![](./media/idcs30.jpeg)
<p align="center"> Figure 1-19 </p>

*  Make no changes in the next screens and click **Next**

 ![](./media/idcs31.png)
 <p align="center"> Figure 1-20 </p>

* For finalizing the IDCS app that grants API roles to Postman via Auth2.0 standard click **Finish.**

![](./media/idcs32.jpeg)
<p align="center"> Figure 1-21 </p>

* Once the application is created, note down the **Client ID** and the **Client Secret** then click **Close.** These will be used by Postman desktop application to call IDCS APIs using the Auth2.0 standard protocol.

![](./media/idcs33.jpeg)
<p align="center"> Figure 1-22 </p>

* Click the **Activate** button. Don’t forget to activate the application

![](./media/idcs34.jpeg)
<p align="center"> Figure 1-23 </p>

* Confirm the application activation

![](./media/idcs35.png)
<p align="center"> Figure 1-24 </p>

* The application is now active and ready to use.
 
 ![](./media/idcs36.jpeg)
 <p align="center"> Figure 1-25 </p>
 
* Sign out from IDCS

###  **EXERCISE** - Configure Postman - Who Should Complete This Lab:  All Participants
    
*  Open **Postman**. Ignore all startup messages if any.

![](./media/idcs37.jpeg)
<p align="center"> Figure 1-26 </p>

*  First we need to import IDCS Postman environment variables, global variables and IDCS API collection. Click the Import button on the left upper corner:

 ![](./media/idcs38.jpeg)
 <p align="center"> Figure 1-27 </p>

*  Select “**Import from Link**” and provide the following URL to import the environment variables:
   
    https://github.com/oracle/idm-samples/raw/master/idcs-rest-clients/example_environment.json

    * and then click **Import**

*  To import the Oracle Identity Cloud Service REST API Postman
    collection, on the Postman main page, click **Import**.

*  In the Import dialog box, select “**Import From Link**”, paste the
    following GitHub Postman collection URL into the box, and then click
    **Import**:

https://github.com/oracle/idm-samples/raw/master/idcs-rest-clients/REST_API_for_Oracle_Identity_Cloud_Service.postman_collection.json

 
 ![](./media/idcs39.png)
 <p align="center"> Figure 1-28 </p>

*  To import the global variables file, click **Import**.

*  In the Import dialog box, select **“Import From Link”,** paste the following GitHub Postman Globals URL into the box, and then click **Import**:

 https://github.com/oracle/idm-samples/raw/master/idcs-rest-clients/oracle_identity_cloud_service_postman_globals.json


*  Click on the **Settings** button (cogwheel icon) to **Manage Environments**

 ![](./media/idcs40.png)
 <p align="center"> Figure 1-29 </p>

*  Click on the newly created environment which will be like “Oracle Identity Cloud Service Example Environment with Variables” and it will probably be the only one available in your cases.

![](./media/idcs41.png)
<p align="center"> Figure 1-30 </p>

* Set the following parameters current values in order to be able to obtain an IDCS access token and click **Update**:

 HOST: https://**your IDCS tenant** 

 Ex: https://idcs-8ba16123120745658135edd99d8a5c78.identity.oraclecloud.com 

 CLIENT_ID: **the Postman IDCS Client application CLIENT_ID** 

 CLIENT_SECRET: **the Postman IDCS Client application CLIENT_SECRET** 

 USER_LOGIN: **Your Oracle Cloud User Id**

 USER_PW: **Your Oracle Cloud Password**


![](./media/idcs42.png)
<p align="center"> Figure 1-31 </p>

* Click the **Environment** drop-down list, and then select the updated environment from the list.

 ![](./media/idcs43.png)
 <p align="center"> Figure 1-32 </p>

*  Request an Access Token
    
    * On the **Collections** tab, expand **OAuth**, and then **Tokens**.
    
    * Select **Obtain access_token (client credentials),** and then click **Send**. The access token is returned in the response from Oracle Identity Cloud Service.
    
    * Highlight the access token content between the quotation marks, and then **right-click**. In the shortcut menu, select **Set: Oracle Identity Cloud Service Example Environment with Variables**.

    * In the secondary menu, select **access_token**. The highlighted content is assigned as the access token value.

 ![](./media/idcs44.jpeg)
 <p align="center"> Figure 1-33 </p>

*  Search an IDCS User via API
    
    * On the **Collections** tab, expand **Users**, and then **Search**.
    * Click on **Search all users (return specific attributes)**
    * Add the key **Count** and the Value **1000**
    * Click on **Send**
    * On the result windown search your user id (e.g. alejandro.casas@oracle.com) and copy the id value without the quotes
    

![](./media/idcs45.png)
 <p align="center"> Figure 1-34 </p>

*  Modify an IDCS User via API
    * On the user collection select **Modify** and **Update user (replace single attribute)**
    * On the patch parameters replace **{{userID}}** with your ID string copied in the previous step
    * Select the Body Tab and update the Phone value number as shown on the screen
    * Click **Send**

![](./media/idcs46.png)
 <p align="center"> Figure 1-35 </p>


* You will receive an email with the profile update confirmation

![](./media/idcs47.png)
 <p align="center"> Figure 1-36 </p>

* Open your profile to see the changes

![](./media/idcs48.png)
 <p align="center"> Figure 1-37 </p>


At this point you are able to make REST application programming interface (API) calls to Oracle Identity Cloud Service using Postman to create, delete and modify users.
For further information about using IDCS REST interface with postman, please visit [Using the Oracle Identity Cloud Service REST APIs with Postman](https://www.oracle.com/webfolder/technetwork/tutorials/obe/cloud/idcs/idcs_rest_postman_obe/rest_postman.html)


# Module 2:  Configure SSO and Provisioning for Salesforce

 Oracle Identity Cloud Service (IDCS) provides integration with any service that can be integrated via **SAML** (Security Access Markup Language) protocol. Administrations will be able to manage users into various applications via single control panel and end users will be able get to applications via single click.
 
 IDCS provides support for standard SAML 2.0 Browser POST Login & Logout Profiles.
 
 Please note, that though IDCS supports SAML and OpenID Connect/OAuth, there are many times when a non-SAML enabled system requires SSO. IDCS App Gate provides support for non-SAML systems that use header-based, cookie-based or form-fill SSO. App Gate is an Nginx-based, software appliance deployed in a proxy configuration that can be deployed on AWS, OCI, OCI-C or on-premises in VMWare or Oracle Virtualbox. It is delivered via Identity Cloud Service and available for IDCS Standard customers.
 
 This lab is intended to demonstrate federated Single Sign-on (SSO) with a 3rd party SaaS application. The purpose is to illustrate the business value of having IDCS as a central Identity Provider for your growing portfolio of Oracle and non-Oracle.
 
 In this hands-on exercise, we will setup integration with **Salesforce** using SAML. IDCS will act as **IdP** (Identity Provider) and Salesforce org as **SP** (Service Provider also known as a Relying Party)

### **DEMO** - Enable SSO on SalesForce

* Download IDCS Metadata to a local XML file. Metadata is available from the following location - https://**yourtenant**/fed/v1/metadata. Depending on the browser you are using,the simplest way of doing this is to right click anywhere on the page and chose “Save as” option provide a name and save it as XML file. Try not to use the copy / paste option as the xml file may be altered.

 ![](./media/idcs47.jpeg)
 <p align="center"> Figure 2-1 </p>

* Navigate to [Developer SalesForce](https://developer.salesforce.com/)
    * Click the **Sign-up** button in the top right corner
    * Enter the required information
    * Click **Sign me up**

**Note: You must sign-up with your personal account (e.g. Gmail, Yahoo, Outlook)**

![SF registration](./media/sf_registration.png)
<p align="center"> Figure 1-24 </p>  


* You will get an email to confirm your account. Click **Verify Account**


![SF verification](./media/sf_verification.png)
<p align="center"> Figure 1-25 </p>  


* Create a password for your account

![SF Create Password](./media/sf_password.png)
<p align="center"> Figure 1-26 </p>  

 
* Access Salesforce application using the URL provided after registration, click on the profile menu as per below print screen and select the option: **“Switch to Salesforce Classic”**.

![](./media/idcs49.jpeg)
<p align="center"> Figure 2-3 </p>

*  Go to **Setup** into the upper tab menu, near the profile.

*  Register a custom Domain. Go to **Domain Management**, **My Domain** and register a domain of your choosing. This is to have a custom application URL dedicate for our use case.

 
 ![](./media/idcs50.jpeg)
 <p align="center"> Figure 2-4 </p>

*  Check your email for the domain login and login.

*  Bring up the **setup** page.

![](./media/idcs51.jpeg)
<p align="center"> Figure 2-5 </p>

*  From side menu bar, go to **Security Controls**, **Single Sign-On Settings**

![](./media/idcs52.jpeg)
<p align="center"> Figure 2-6 </p>

*  Click on **Edit** and enable **Federated Single Sign-On Using SAML** option.

![](./media/idcs53.png)
<p align="center"> Figure 2-7 </p>

* Click on **New from Metadata File** button to import IDCS metadata. Select the downloaded metadata file using **Choose File** button. Click on **Create**.

![](./media/idcs54.png)
<p align="center"> Figure 2-8 </p>

* Update the **Entity ID** with the domain information registered in the previous steps (e.g *https://acasas-dev-ed.my.salesforce.com*) and click **Save**

![](./media/idcs55.jpeg)
<p align="center"> Figure 2-9 </p>

* Below are the details for this example. Note, your URLs and domain information will be different.

![](./media/idcs56.jpeg)
<p align="center"> Figure 2-10 </p>

![](./media/idcs57.jpeg)
<p align="center"> Figure 2-11 </p>

* Make note the following:

  * Organization ID value

  * Org Domain Name value.

![](./media/idcs58.jpeg)
<p align="center"> Figure 2-12 </p>

Now that the Salesforce configurations are done, we need to configure IDCS to be aware of the Salesforce application.

* Go to IDCS admin console, navigation menu, **Applications**

 ![](./media/idcs59.jpeg)
 <p align="center"> Figure 2-13 </p>

* Click on **Add** button and select **App Catalog** and search for Salesforce. Click on **Add.**

 ![](./media/idcs60.jpeg)
 <p align="center"> Figure 2-14 </p>

* On the first page of configuration screen provide the **Organization**

 **ID** and **Domain Name** values that you made note of from within Salesforce.

![](./media/idcs61.jpeg)
<p align="center"> Figure 2-15 </p>

* Click on **Next** to move to the SSO configuration

 ![](./media/idcs62.jpeg)
 <p align="center"> Figure 2-16 </p>

* Click on **Finish** button

* **Activate** the application

 ![](./media/idcs63.png)
 <p align="center"> Figure 2-17 </p>

### **DEMO** - Assign Apps to Group (Persona: Administrator)

In IDCS you have the option to assign access to users directly, by direct assignment to a specific application, or indirectly using dedicated groups. For the purpose of the use case we’ll be using groups to provide users access to Salesforce application.

*  Go to IDCS admin console, **Groups** menu

*  Add a group labeled **Employee**. Check the box **User can request access**.

 ![](./media/idcs64.png)
 <p align="center"> Figure 2-18 </p>

*  Click on **Finish**

*  Go to the **Access** tab. Click on **Assign**.

*  Select **Salesforce** and click on **OK**.

![](./media/idcs65.jpeg)
<p align="center"> Figure 2-19 </p>

Moving back to Salesforce in order to create a corresponding account for one that we have into IDCS.

*  **Login** into **Salesforce** as an administrator.

*  Go to **Setup**.

*  On the left panel, click on **Manage Users**, then on **Users** and then on **New User**.

*  Create a user as shown below. Be sure to use the email address as the login and use one that matches the account created in IDCS in Module 1. In this case, We’ve used *oracleuser3003@gmail.com*

*  Set the **User License** to **Salesforce Platform**.

![](./media/idcs66.jpeg)
<p align="center"> Figure 2-20 </p>

Now that the account is available in Salesforce and IDCS has the authenticated account you are ready to test.

### **EXERCISE** - Request Group Access (Persona: End User) - Who Should Complete This Lab:  All Participants

Remember that we have created the **Employee** group into IDCS which is having access to Salesforce application but there is no user assigned yet to it. Since we chose the option
 
**“User can request access”** at the creation of the group, now we should be able to request access to it and implicitly to the alesforce application.

*  Close your browser to clear the cache and then login into IDCS https://**Your IDCSInstance**.identity.oraclecloud.com/ui/v1/myconsole.

*  From **My Apps** page, click on **+ Add** access request button.

![](./media/idcs67.jpeg)
<p align="center"> Figure 2-21 </p>

*  From the **Groups** tab, select **Employee** group and select the **+** sign.

![](./media/idcs68.jpeg)
<p align="center"> Figure 2-22 </p>

*  Click on + sign to request access to the group. Provide justification on the resulting popup page. Click on **OK**. This is an auto approved request and access should be granted immediately without the need of and administrator intervention.

 ![](./media/idcs69.jpeg)
 <p align="center"> Figure 2-23 </p>

*  Go to **My Profile** section from menu located top-right

![](./media/idcs70.jpeg)
<p align="center"> Figure 2-24 </p>

*  Ensure that **Employee** group is visible under **My Access** sub-tab

 ![](./media/idcs71.png)
 <p align="center"> Figure 2-25 </p>

*  Ensure that Salesforce applications are visible now on the **MyApps** page

![](./media/idcs72.png)
<p align="center"> Figure 2-26 </p>

### **EXERCISE** - Verify SSO Configuration (Persona: End User) Who Should Complete This Lab:  All Participants

*  Click on the **Salesforce Chatter** app from **My Apps** page

*  Ensure that user is automatically logged into Salesforce Chatter (**SSO**)

![](./media/idcs73.jpeg)
<p align="center"> Figure 2-27 </p>

You should now see the same user profile information, that you started within IDCS, within Salesforce without having had to log into Salesforce.

## Configuring Provisioning and Synchronization – OPTIONAL

The following exercise has been developed to showcase the extend of IDCS Single Sign-On capabilities by integrating the provisioning and synchronization services with third-party apps.

### **DEMO** - Configure Provisioning and Synchronization (Persona: Administrator) - OPTIONAL

*  Obtaining Host Name, Organization ID, and Domain Name from Salesforce

A host name, organization ID, and a domain name are required before you can configure the Salesforce app in Oracle Identity Cloud Service. You obtain these values from Salesforce.

*  Login to [Developer Salesforce](https://developer.salesforce.com). In the left navigation menu of the home page, search and click Single Sign-On Settings. The Single Sign-On Settings page appears.

![](./media/idcs74.jpeg)
<p align="center"> Figure 2-28 </p>

*  Under the SAML Single Sign-On Settings section, **click** the name that you provided for your identity provider in the **Single Sign-On Settings page**. The SAML Single Sign-On Settings page appears.

*  Make note of the host name from the value given in the **Entity ID** 

* Field: https://Host_Name

*  Under the Endpoints section, make note of the domain name and the organization ID from the **Salesforce Login URL**: https://**Domain_Name**.my.salesforce.com?so=**Organization_ID**
The domain name appears at the beginning and the organization ID appears at the end of the URL.

![](./media/idcs75.png)
<p align="center"> Figure 2-29 </p>

*  Obtaining the Consumer Key and Consumer Secret from Salesforce

**Consumer key** and **consumer secret** values are required before you enable provisioning for the Salesforce app. You obtain these values from Salesforce.

* Switch to **Lightning Experience** in Salesforce, click the **cogwheel** on the top right corner of the page and select **Setup**.

![](./media/idcs76.jpeg)
<p align="center"> Figure 2-30 </p>

*  In the left navigation menu of the home page, search and click **AppManager**. The Lightning Experience App Manager page appears.

![](./media/idcs77.jpeg)
<p align="center"> Figure 2-31 </p>

*  In the right corner of the page, click **New Connected App**. The New Connected App page appears.

![](./media/idcs78.png)
<p align="center"> Figure 2-32 </p>

*  Under the Basic Information section, enter the Connected App Name of the app that you want to connect.

*  Enter the **Contact Email** of the administrator.

* Under the API(Enable OAuth Settings) section, select the **Enable OAuth Settings** Check box.

* Enter any public domain URL that receives the access token from the authorization server in the **Callback URL** field. For example, https://login.salesforce.com

* In the Selected OAuth Scopes field, select Full access(full) under the **Available OAuth** Scopes list, and then click Add to give full access to modify the OAuth.

![](./media/idcs79.jpeg)
<p align="center"> Figure 2-33 </p>

* Scroll down and click **Save**.

* Wait for 2-10 minutes for the changes to take effect on the server before using the connected app, and then click **Continue**. The newly created app page appears.

* Under the API (Enable OAuth Settings) section, click “**Click to reveal**” next to the **Consumer Secret** field.

![](./media/idcs80.png)
<p align="center"> Figure 2-34 </p>

* Make note of the **Consumer Key** and **Consumer Secret** values.

### **DEMO** - Deriving the Administrator Password from Salesforce

 A security token must be appended to the administrator password before you enable provisioning and synchronization for Salesforce app. You obtain the token value from Salesforce.
 
 The final value will look like this:
 
 `yourSalesforceAdminPassword + securityToken`
 (ex: LKdMzECdjFKYSj028WJhU1GG)

* In the upper-right corner of the **Salesforce** home page, click the user icon, and then click Settings from the drop-down list.

![](./media/idcs82.jpeg)
<p align="center"> Figure 2-35 </p>

* In the left navigation menu, search and click **Reset My Security Token.**

 ![](./media/idcs83.jpeg)
 <p align="center"> Figure 2-36 </p>

* On the Reset My Security Token page, click **Reset My Security Token**. A security token is sent to the email address of the administrator.

* Make note of the security token, and append the security token to the administrator password.

 `yourSalesforceAdminPassword + securityToken`
 (ex:LKdMzECdjFKYSj028WJhU1GG) 
 NOTE: the + must not be included

###  **DEMO** - Enabling Provisioning and Synchronization for Salesforce - OPTIONAL

 Provisioning will provide you with the following available operations:
 
 **Create Account**: Automatically creates a Salesforce account when
 Salesforce access is granted to the corresponding user in Oracle
 Identity Cloud Service.
 
 **De-activate Account**: Automatically deactivates or activates a
 Salesforce account when the Salesforce access is deactivated or
 activated for the corresponding user in Oracle Identity Cloud Service.
 
 **Delete Account:** Automatically removes an account from Salesforce
 when Salesforce access is revoked from the corresponding user in
 Oracle Identity Cloud Service.
 
 Beside this you have the ability to map attributes between the user
 account fields defined in Salesforce and the corresponding fields
 defined in Oracle Identity Cloud Service.

* Go to IDCS admin console

* Select the Salesforce applications that you have created previously

* On the Provisioning page, select **Enable Provisioning**.

* A window will pop up. Click “**Grant Consent**”

* Fill in the **Host Name (e.g. acasas-dev-ed.my.salesforce.com), Administrator Username**, **Administrator Password** that you derived in the previous steps from Salesforce, **Client ID** and **Client Secret** from the Salesforce app created in the previous section. 

![](./media/idcs84.jpeg)
<p align="center"> Figure 2-37 </p>

* Click **Test Connectivity** to verify the connection with Salesforce. Oracle Identity Cloud Service displays a confirmation message.

* Scroll down on the Provisioning page, select **Enable Synchronization**.

 ![](./media/idcs85.jpeg)
 <p align="center"> Figure 2-38 </p>
 
 This option will synchronize the existing account details from
 Salesforce and link them to the corresponding Oracle Identity Cloud
 Service users.

###  **DEMO** - Testing Synchronization in IDCS - OPTIONAL

*  On the applications page, select **Import**.

![](./media/idcs86.png)
<p align="center"> Figure 2-39 </p>

*  Click on **Import** and wait for a moment

*  Click **Refresh**

![](./media/idcs87.png)
<p align="center"> Figure 2-40 </p>

*  The imported users that were imported from IDCS will be displayed.

![](./media/idcs88.jpeg)
<p align="center"> Figure 2-41 </p>


****
**You have successfully connected and provision IDs on third-party app and enable Single Sign-On to easily login to other vendor services.**

***END OF LAB***

[Back to Top](#table-of-contents)   