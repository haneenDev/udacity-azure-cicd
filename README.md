# udacity-azure-cicd
![Python application test with Github Actions](https://github.com/Haneen-97/udacity-azure-cicd/workflows/Python%20application%20test%20with%20Github%20Actions/badge.svg)


This is my submission for the 'Building a CI/CD Pipeline' project as part of the 'DevOps Engineer for Microsoft Azure' nanodegree program from [Udacity](https://udacity.com).

This project contains a python application that is designed to predict housing prices in Boston (I did not create the python app myself). This repo will enable you to:
- Deploy the app in Azure CloudShell
- Deploy the app as an Azure App Service

Any commits to the GitHub repo trigger automated code testing using GitHub Actions. A pipeline has been created in Azure DevOps, and the updated code is also automatically tested in Azure DevOps and deployed to the Azure App Service. 

Here is an architectural diagram:
![architectural-diagram.png](architectural-diagram.png)

A [Trello](https://trello.com/b/CjgPIZxU/building-a-ci-cd-pipeline) board has been created to keep track of tasks to be completed.

A [spreadsheet](project-schedule.xlsx) has been created to manage the project schedule.

See [here](https://youtu.be/FHRAl93XgG8) for a YouTube video demonstrating the project.


# Overview

This is my submission for the 'Building a CI/CD Pipeline' project as part of the 'DevOps Engineer for Microsoft Azure' nanodegree program from [Udacity](https://udacity.com).

This project contains a python application that is designed to predict housing prices in Boston (I did not create the python app myself). This repo will enable you to:
- Deploy the app in Azure CloudShell
- Deploy the app as an Azure App Service

Any commits to the GitHub repo trigger automated code testing using GitHub Actions. A pipeline has been created in Azure DevOps, and the updated code is also automatically tested in Azure DevOps and deployed to the Azure App Service. 
## Project Plan
<TODO: Project Plan

A [Trello](https://trello.com/b/xtbJ4xMa/building-a-ci-cd-pipeline-udacity-project) board has been created to keep track of tasks to be completed.

A [spreadsheet](project-schedule-h.xlsx) has been created to manage the project schedule.

## Instructions
Here is an architectural diagram:
![arch diagram](https://user-images.githubusercontent.com/43758373/104777577-f016dc00-578c-11eb-82f7-f6da3ba19f5c.PNG)

## Deploy the app in Azure Cloud Shell
In Azure Cloud Shell, clone the repo:
```
git clone git@github.com:Haneen-97/udacity-azure-cicd.git
```
![screenshot-gitClone-AzureCloud](https://user-images.githubusercontent.com/43758373/104778534-8c8dae00-578e-11eb-9b3f-fbd59bde16fd.PNG)


Change into the new directory:
```
cd udacity-azure-cicd
```

Create a virtual environment:
```
python3 -m venv ~/.myrepo
```

Activate the virtual environment:
```
source ~/.myrepo/bin/activate
```

Install dependencies in the virtual environment and run tests:
```
make all
```
![make-all](https://user-images.githubusercontent.com/43758373/104778690-d5456700-578e-11eb-8159-63181a2c61c0.PNG)
![make-all2](https://user-images.githubusercontent.com/43758373/104778688-d4acd080-578e-11eb-9bde-f13800ba9c31.PNG)
![make-all3](https://user-images.githubusercontent.com/43758373/104778685-d4143a00-578e-11eb-924d-5c4c813f2f01.PNG)
![make-all4](https://user-images.githubusercontent.com/43758373/104778682-d37ba380-578e-11eb-836d-8e9bc715f55c.PNG)


Start the application in the local environment:
```
python app.py
```

Open a separate Cloud Shell and test that the app is working:
```
./make_predict_azure_app.sh
```

The output should match the below:

![screenshot-prediction](https://user-images.githubusercontent.com/43758373/104778892-2ce3d280-578f-11eb-8441-51b95f34f267.PNG)


## Deploy the app to an Azure App Service

Create an App Service in Azure. In this example the App Service is called rob-udacity-webapp and the resource group is called rob-udacity-project:
```
az webapp up -n rob-udacity-webapp -g rob-udacity-project
```

Next, create the pipeline in Azure DevOps. More information on this process can be found [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops&WT.mc_id=udacity_learn-wwl). The basic steps to set up the pipeline are:

- Go to [https://dev.azure.com](https://dev.azure.com) and sign in.
- Create a new private project.
- Under Project Settings create a new service connection to Azure Resource Manager, scoped to your subscription and resource group.
- Create a new pipeline linked to your GitHub repo.

Screenshot of the App Service in Azure:

![screenshot-webapp-service](https://user-images.githubusercontent.com/43758373/104779603-6a952b00-5790-11eb-9f6a-6a31b506364c.PNG)

Screenshot of a successful run of the project in Azure Pipelines:

![screenshot-azure-pipeline-deployment](https://user-images.githubusercontent.com/43758373/104779545-55200100-5790-11eb-9dd8-ca3e0153e3df.PNG)

To test the app running in Azure App Service, edit line 28 of the make_predict_azure_app.sh script with the DNS name of your app. Then run the script:
```
./make_predict_azure_app.sh 
```

If it's working you should see the following output:

![screenshot-prediction](https://user-images.githubusercontent.com/43758373/104778892-2ce3d280-578f-11eb-8441-51b95f34f267.PNG)

You can also visit the URL of the App Service via the browser and you should see the following page:

![screenshot-browser](https://user-images.githubusercontent.com/43758373/104779465-36216f00-5790-11eb-8561-2869ad9dd09d.PNG)

View the app logs:

in the browser bar type: https://<app-name>.scm.azurewebsites.net/api/logs/docker


![screenshot-log-webapp](https://user-images.githubusercontent.com/43758373/104779427-2a35ad00-5790-11eb-8da3-69c7bc269d51.PNG)


> 

## Enhancements

Currently, there is only a single branch in GitHub. In the future it would be good to create multiple branches, so code can initially be tested and deployed in a staging environment. If it works correctly in the staging environment the changes could then be merged into the production branch and the code deployed into the production environment.

## Demo 

<TODO: Add link Screencast on YouTube>



