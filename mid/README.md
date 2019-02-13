# Jenkins in Azure

This task is going to leverage the functionality of Azure Jenkins instance.

## Prerequisites

1. Azure account. If you don't have one please register it for free [here](https://azure.microsoft.com/en-us/free/). You will receive 12-months free usage of Azure services within 200$ budget
2. Sign in to you Azure account
3. Make sure that you can access Azure portal - portal.azure.com
4. Using Azure Portal create new Jenkins server instance:
    * Hit "Create a Resource":

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/entry/img/create-azure-devops.PNG)

    * Search for "Jenkins" and click on "Jenkins"

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins.PNG)

    * generate ssh keys using the following instruction (https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html)

    * Fill server name, resource group and insert your public ssh key. Click "OK"

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-2.PNG)

    * Fill additional settings: Domain name and JDK version should be "OpenJDK"

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-3.PNG)

    * Leave integration settings without any changes

    * Vaidate all settings and confirm deployment. Wait till Azure finish all deployment steps

    * Go to resource group with Jenkins and find a virtual machine.

    * Find DNS name of jenkins server copy and paste it to the browser.

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-4.PNG)

    * You'll see a blue window that server was deployed without secure https connection. Follow the instructions on the screen:

         ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-5.PNG)

      Connect by SSH to jenkins server and establish secure tunnel with port forwarding using following command `ssh -L 127.0.0.1:8080:localhost:8080 -i <PATH TO YOUR PRIVATE KEY> <YOUR USERNAME>@<JENKINS SERVER DNS NAME>` :

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-6.PNG)

    * Execute following command and copy password:
        `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-8.PNG)


    * Navigate to http://localhost:8080 using browser and let's finish our jenkins configuration. Insert copied password here and click "Continue"


        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-7.PNG)


    * Agree with "Install suggested plugins"

    * Created admin user with password (Don't use your main password!!!)

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-9.PNG)

    * Jenkins is almost ready. Since it's our temporary server and you didn't use your main password we can make it available without SSH tunnel. Go to Azure Portal to Resource group with virtual machine and find the `jenkins-nsg` Network Security Group resource. Click on that resource and under the settings find "Inbound security rules":

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-10.PNG)

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-11.PNG)

    * Click on "Add" and leave all parameters with default values:

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-12.PNG)

    * Now we can access our jenkins without SSH tunnel using http link like http://http://jenkins-my.westeurope.cloudapp.azure.com:8080 We need this functionality later.


    * Let's prepare our jenkins server with some parameters. First of all you need to install maven build tool and set JAVA_HOME. How to do it you can find here? for example (https://www.rosehosting.com/blog/how-to-install-maven-on-ubuntu-16-04/).

    * Open Jenkins console. Go to "Manage Jenkins" -> "Configure system". Find "Jenkins URL" field and set it with public DNS with port 8080. Save.

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-13.PNG)

    * Go again to "Manage Jenkins" -> "Global tools configuration". Configure JDK installation with your $JAVA_HOME and Maven with $MAVEN_HOME:

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-15.PNG)

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-14.PNG)

5. Create Azure Web App service to deploy WebApp (Simulate production env)
  
    * Hit "Create a Resource"

    * Search for WebApp

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-16.PNG)

    * Enter app name, use existing jenkins resource group, OS Linux, Publish Code, Runtime Stack Tomcat 8.5

        ![create-jenkins](https://github.com/elluvium/cicd-workshop/blob/master/mid/img/create-jenkins-17.PNG)

    * Wait for deployment

6. Create build and deploy pipeline from example Maven WebApp

    * In Jenkins click on "Create new item", enter a job name and select type "Pipeline". Click "Ok".

    * Inside Pipeline Script insert content from `pipeline/build-deploy.jenkinsfile`. Also, you need to set `appName` variable inside `Deploy to Azure WebApp` stage

    * Click save and schedule a build

    * After successfull build and deploy stages navigate to the app service URL with WebApp artifact name. For instance https://my-super-app.azurewebsites.net/WebApp


## Extra task
* Push changes to the repo and rebuild Jenkins job. See changes in your WebApp


## Cleanup
Don't forget to delete created resources in Azure by deleting all resource groups


## Useful links
1. https://tutorials.visualstudio.com/jenkins-azure/new/solution-template