# Azure DevOps
This task is going to leverage the functionality of Azure DevOps service. 

## Prerequisites
1. Azure account. If you don't have one please register it for free [here](https://azure.microsoft.com/en-us/free/). You will receive 12-months free usage of Azure services within 200$ budget
2. Sign in to you Azure account
3. Make sure that you can access Azure portal - portal.azure.com
4. Using Azure Portal create new DevOps organization and project

    Hit "Create a Resource":

    ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops.PNG)

    Search for "DevOps" and click on "DevOps project"

    ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-1.PNG)

    Click "Create":

    ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-2.PNG)

    Choose one of the already created sample project (.NET for instance) - most easy way:

    ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-3.PNG)

    Or scroll down and choose "Bring your own code" (In case you already have a project) - little bit harder:

    ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-4.PNG)

    Select .NET Framework (I would go with ASP.NET Core):

    ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-5.PNG)

    Select Azure service where to deploy an application (Most easy way to select Windows or Linux Web App)
    > Linux is available since ASP.NET Core is a cross-platform and open-source web framework

    ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-6.PNG)    

    Finish creating new web app with entering project name and creating new web app service:

     ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-7.PNG)    

    Azure has been started to provision all nesessary resources:

     ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-8.PNG)    



## Build and test Go projects with Azure DevOps pipelines
1. 



## Useful links
1. https://docs.microsoft.com/en-us/azure/devops/user-guide/?view=azure-devops
2. 