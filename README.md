[//]: # "Copyright (c) Microsoft Corporation."
[//]: # "Licensed under the MIT License."

# Project

The Microsoft Omnichannel Add-on is transforming customer engagement through Generative AI technology across various communication channels. It serves as an AI-centric contact center solution compatible with any CRM or third-party (3P) software. This add-on enables customers to leverage Dynamics 365 Omnichannel (OC) along with AI functionalities within their preferred CRM system.

Built upon the Dynamics Contact Center Platform (DCCP) infrastructure, the Omnichannel Add-on extends its capabilities by seamlessly integrating OC and AI features with existing 3P solutions. Agents have the flexibility to utilize the add-on in either Embedded mode, where the 3P CRM serves as the primary user experience (UX) with OC/AI functionalities embedded, or Standalone mode, where Dynamics OC/AI capabilities take precedence while maintaining connectivity with 3P CRM data.
You can find more details in (https://microsoft.sharepoint.com/:w:/t/Dynamics365CustomerCareApplications/Ee3vBYzRVh9OqGQgNq0ehj8BSSgmm17L1susO6wn7jKnSQ?e=sii0Le)

# Overall Process 

The following steps will guide you to get the Omnichannel Add-on embedded mode working within Salesforce. You should budget for 40 minutes or more to complete the Required Steps. 

Required Steps: 

1. Setup Dynamics OmniChannel 
   
2. Setup Salesforce (for Embedded Model; optional for Standalone) 

3. Integrate Dynamics Omnichannel Add-on with Salesforce (for Embedded Model; optional for Standalone) 

 Optional Steps: 

4. Make updates to your CRM integrations. 

5. Sync (one-time or as needed) CRM data with Dataverse. 


- The CTI driver serves as a bridge between the Microsoft Omnichannel Add-on and Salesforce CRM, allowing for the integration of telephony features into the CRM environment.
 
Note: These steps can be omitted if the default CTIDriver file is used. 

# Prerequisite
1. Install Node (latest version) <Node-link>
2. git clone <git-url> of repo

# CTIDriver Extention for SF and SN

## SF Extension

1. Navigate to /samples/SFExampleCTIDriver/src

2. Open the file /samples/SFExampleCTIDriver/src/SFExampleCTIDriver.ts

3. Implement your desired functionality within any of the methods provided by the ICTIDriver interface.
    Refer to the [Salesforce OpenCTI Methods Documentation](https://developer.salesforce.com/docs/atlas.en-us.api_cti.meta/api_cti/sforce_api_cti_methods_intro_lightning.htm) for available methods and their usage.

4. Run command npm install
    `npm install`

5. Run command npm run build, dist/SFExampleCTIDriver.js file will get generated inside /SFExampleCTIDriver folder
    `npm run build`
6. Host the compiled file on a CDN and include the CDN URL as a query parameter in the call center definition file imported/seen in step 3 under “Salesforce specific instructions: CTI Adapter instructions” heading. 

    Note: It does not need to be a CDN URL, any URL with public access will also work 
     
    The format of the URL should be: 
     
    `https://<ccaas-domain>/widget/index.html?dynamicsUrl=https://msdynccaasdev.crm.dynamics.com&ctiDriverUrl=<CDN-url>`
    
    ccaas-domain: `https://ccaas-embed-prod.azureedge.net` 
     
    Replace <CDN-url> with the actual URL of the hosted compiled file on the CDN. 

7. Import the call center definition file in the salesforce call center.

   [Call center defination file](https://github.com/microsoft/dynamics-365-contact-center/blob/main/samples/SFCallCenter/Dynamics365CallCenter.xml)
   Update the Salesforce Call Center definition file by replacing the <ctiDriverUrl> parameter with the URL generated in Step 6.

   ![alt text](image.png)

7. Follow Salesforce's instructions to configure your softphone using the integrated SF Extension.
   
8. Your SF Extension integration is now complete and ready to use with Salesforce.


## CTIDriver Implementation for Generic CRM 

1. Copy the code from `samples/GenericExampleCTIDriver`.

2. Navigate to `GenericExampleCTIDriver/src/GenericExampleCTIDriver.ts`.

3. Implement the methods defined in `ICTIInterface` according to your CRM requirements.

4. Run `npm install` to install the project dependencies.

5. Run `npm run build` to compile the project.

6. Host the compiled file on a CDN. Include the CDN URL as a query parameter in the CCaaS URL. For example, the CCaaS URL format should be:
   `https://<ccaas-domain>/widget/index.html?dynamicsUrl=https://msdynccaasdev.crm.dynamics.com&ctiDriverUrl=<CDN-url> `
   Replace <CDN-url> with the actual URL of the hosted compiled file on the CDN.
   
   Note: It does not need to be a CDN URL, any URL with public access will also work 

   ccaas-domain: `https://ccaas-embed-prod.azureedge.net` 

7. Incorporate this URL into the phone/softphone settings of your CRM.


