
This multi-tenant sample demonstrates how to store Outlook mail attachment files of Office 365  on a custom storage.

This sample contains two codes sources:
* An Office 365 Outlook App compatible with Office 2013 Client and Office Web App.
* An ASP.NET Web API backend used to store Outlook attachment files. The API Backend is used only as an example. It's a fake API provided for demo purpose.


## Prerequisite

To run this sample you will need:
* Microsoft Visual Studio 2013 R4
* An Azure subscription (a free trial is sufficient)

Every Azure subscription has an associated Azure Active Directory tenant. If you don't already have an Azure subscription, you can get a free subscription by signing up at http://www.windowsazure.com. All of the Azure AD features used by this sample are available free of charge.


## How To Run This Sample

Follow Steps 1 to 4.

### Step 1: Clone or download this repository
From your shell or command line:  `git clone https://github.com/nabilbo/keeper.git`


### Step 2: Register the Outlook App with your Azure AD tenant

* 1.Sign in to the Azure management portal.
* 2.Click on Active Directory in the left hand nav.
* 3.Click the directory tenant where you wish to register the sample application.
* 4.Click the Applications tab.
* 5.In the drawer, click Add.
* 6.Click "Add an application my organization is developing".
* 7.Enter a friendly name for the application, for example `TheFilesKeeper-OutlookApp`, select "Web Application and/or Web API", and click next.
* 8.For the sign-on URL, enter the base URL for the sample, which is by default  `https://localhost:44305/` .
* 9.For the App ID URI, enter  `https://<your_tenant_name>/TheFilesKeeper-OutlookAapp`, replacing  <your_tenant_name>  with the name of your Azure AD tenant.
* 10.While still in the Azure portal, click the Configure tab of your application.
* 11.Find the Client ID value and copy it to the clipboard.
* 12. Download the Manifest file
* 13. Edit the Manifest File to Enable the OAuth2 implicit grant : search for the  `oauth2AllowImplicitFlow`  property. You will find that it is set to  false ; change it to  true  and save the file.
* 14. Upload the modified Manifest file.
* 15. Turn On `Multi-tenant App`

All done! Before moving on to the next step, you need to find the Client ID of your application.

### Step 3 : Register the Web Api Sample with your Azure AD tenant

The same as Step 2 except for steps **7, 8, 9** and **13** :
* 7.Enter a friendly name for the application, for example `TheFilesKeeper-WebAPI`, select "Web Application and/or Web API", and click next.
* 8.For the sign-on URL, enter the base URL for the sample, which is by default  `https://localhost:44318/` .
* 9.For the App ID URI, enter  `https://<your_tenant_name>/TheFilesKeeper-WebAPI`, replacing  <your_tenant_name>  with the name of your Azure AD tenant.
* 13.Edit the Manifest File to Enable the OAuth2 implicit grant : search for the  oauth2AllowImplicitFlow  property. Set to  false ; change it to  true  and save the file. You have also to declare the Web Api Sample as ressource for the Outlook App : Edit 'KnowClientApplications' section to add the Outlook App Client ID (Step 2.11). For example :   `"knownClientApplications": ["1caf8bf7-7a79-4e6e-9309-637372852ca6"],`



### Step 4: Configure the Visual Studio Solution.

* 1. Open the visual studio solution : `[VS_SOLUTION]\TheFilesKeeper.Outlook.App\TheFilesKeeper.Outlook.App.sln`
* 2. Edit the config.js `[VS_SOLUTION]\TheFilesKeeper.Outlook.App\TheFilesKeeper.Outlook.AppWeb\Common\config.js`
to run this sample, you will only need to modify the lines flaged **"edit here"**


```javascript
/* The Files Keeper App configuration */

// STORAGE_PREFIX : prefix used to cache app data and to identify storage URI.
// if you change this value, don't forget to also change RegExValue on the Outlook app manifest.xml file.
var STORAGE_PREFIX = "keeper"; 

// OUTLOOK_APP_CLIENT_ID : Outlook App Client ID eg : 'f997c817-0695-4e70-87df-3e9e9e04649a' 
// this Client ID was created at the Step 2.11. 
OUTLOOK_APP_CLIENT_ID = '00000000-0000-0000-0000-000000000000';  /////////  => edit here

// BACKEND_URI eg : '"https://mytenant.onmicrosoft.com/TheFilesKeeper-WebAPI".
// this URI was created at the Step 3.9.
BACKEND_URI= "https://xxxxxxxxxxxxxxxxxxxxx.onmicrosoft.com/TheFilesKeeper-WebAPI";  /////////  => edit here

// BACKEND_CLIENT_ID : Web API Sample Client ID eg : 'f997c817-0695-4e70-87df-3e9e9e04649a' 
// This Client ID was created at the Step 3.11
BACKEND_CLIENT_ID = '00000000-0000-0000-0000-000000000000';  /////////  => edit here

//ENDPOINTS : Service api endpoints
var ENDPOINTS = {
    "https://localhost:44318/": BACKEND_URI,
};

//STS_ENDPOINT : Service api STS_ENDPOINT eg : https://query.microsoft.com/
var STS_ENDPOINT = "https://localhost:44318/api/azure/keystone"; 
```

3. Run the app **F5**. That's All !


## How to deploy it to Azure
Coming soon.




## About the Code
We will only describe the Outlook App Source Code :

* /AppCompose/ : contains the Outlook App used to compose an email and save attachment into the external Storage.
* /AppRead/ : contains the Outlook App used to read attachment files.
* /Common/ : contains common features, ressources, ...
 * /Services/ : web api consumption
 * /Translations/ : contains language ressources in French and English.
 * /AngularApp.js : contains the angular app initialization, and routes.
 * /Config.js : app configuration.
 
## Licence
Microsoft Public License (MS-PL).

## Ressources
These ressources have been used to develop theFilesKeeper :

### Code Samples
* [singlePageApp-DotNet](https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet "SinglePageApp-DotNet")

### Libraries
* [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js "Adal.js")
* [angular.js](https://angularjs.org/ "angular.js")
* [angular-file-upload](https://github.com/nervgh/angular-file-upload "https://github.com/nervgh/angular-file-upload")
* [boostrap.css](http://getbootstrap.com/ "boostrap.css")
* [animate.css](https://daneden.github.io/animate.css/ "animate.css")
