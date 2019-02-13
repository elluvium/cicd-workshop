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

    When Azure finished all deployments under your Resource Groups blade you will find 2 groups:
    * One with Azure App Service called by you on previous steps (In my case my-web-app-sample-rg)
    * Another one with DevOps Project and Organization resources (with auto generated name, like VstsRG-clt-....)
    
         ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-9.PNG)


## Build and test projects with Azure DevOps pipelines
Since you're finished all steps in prerequisites part, we're ready to start with digging into pipelines.

1. Go inside "VstsRG-clt...." named resource group. You'll find 2 resources:

    * Azure DevOps organization 
    * DevOps project for your application

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-10.PNG)

2. Click on DevOps project resource. You'll find:

    * CI/CD Pipeline definition
    * Your Azure Web App service (Prod, where your application is running)
    * Repository with code
    * Application Insights resource with Web App requests logs

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-11.PNG)

    You can click on "Browse" button and navigate to your web site running on Azure Web App service

3. Investigate Build and Release pipelines by clicking on corresponding buttons
4. Investigate source code by clicking on "Code" button
5. Clone source code and make some changes to trigger build pipeline:

    *  Click on Clone button, hit "Generate Credentials", enter your new password and copy clone link

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-12.PNG)

    * Use your clone link to clone source code locally:

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-13.PNG)
        > Use `git clone` command

    * Open project using text editor and make change to `Application\aspnet-core-dotnet-core\Views\Home\Index.cshtml` file. For instance, let's change word "Success" on the main page to "This text is delivered here by Azure DevOps". Find approriate html tag (`<div class="success-text">Success!</div>`) and change content:

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-14.PNG)

    
    * Push changes to the repo with git commands (`git add .`, `git commit -m "<YOUR MESSAGE>"`, `git push origin master`):

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-15.PNG)

    * Make sure that build pipeline triggered:

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-16.PNG)

    * Check build logs:

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-17.PNG)

    * Check build status:

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-18.PNG)

    * Check deploy pipeline (logs and status)

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-19.PNG)


    * Check your e-mail to see the notification regarding successfull build

    * Navigate to the Application Endpoint to see your change:

    * Check deploy pipeline (logs and status)

        ![create-devops](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops-20.PNG)

    * You're awesome :)

## Extra task
1. Make change in the source code with intentional mistake, commit and see what will happen.





## Useful links
1. https://docs.microsoft.com/en-us/azure/devops/user-guide/?view=azure-devops
2. https://azure.microsoft.com/en-us/features/devops-projects/
3. https://docs.microsoft.com/en-us/azure/devops/pipelines/get-started/what-is-azure-pipelines?toc=/azure/devops/pipelines/toc.json&bc=/azure/devops/boards/pipelines/breadcrumb/toc.json&view=azure-devops