# udacity-azure-cicd
![Python application test with Github Actions](https://github.com/Haneen-97/udacity-azure-cicd/workflows/Python%20application%20test%20with%20Github%20Actions/badge.svg)


# Overview

This project is submitted by me Haneen, a part for earning a nanodegree of Building a CI/CD Pipeline for 'DevOps Engineer for Microsoft Azure' program from Udacity.

This project consists of flask application that is developed to predict housing prices in Boston (the model is already created by the instructor). 

This repositry demonstrate:
- Deploying the app in Azure CloudShell
- Deploying the app as a web server using Azure App Service.

Once anything has been changed (commits) in the github repositry, it will trigger an action for test automation (CI). A pipeline has been created using Azure DevOps tool, and also any changes will be tested in the pipeline and deployed to app service. All these steps are explianed well in the demo below. 
 

## Project Plan

A [Trello](https://trello.com/b/xtbJ4xMa/building-a-ci-cd-pipeline-udacity-project) board has been created to keep track of the tasks.

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

Create a virtual environment:
```
python3 -m venv ~/.myrepo
```

Activate the virtual environment:
```
source ~/.myrepo/bin/activate
```

Change into the new directory:
```
cd udacity-azure-cicd
```

Install dependencies in the virtual environment and run tests:
```
make all
```
![make-all](https://user-images.githubusercontent.com/43758373/104778690-d5456700-578e-11eb-8159-63181a2c61c0.PNG)
![make-all2](https://user-images.githubusercontent.com/43758373/104778688-d4acd080-578e-11eb-9bde-f13800ba9c31.PNG)
![make-all3](https://user-images.githubusercontent.com/43758373/104778685-d4143a00-578e-11eb-924d-5c4c813f2f01.PNG)
![make-all4](https://user-images.githubusercontent.com/43758373/104778682-d37ba380-578e-11eb-836d-8e9bc715f55c.PNG)

A successful GitHub build test 
![screenshot-build-success-actiongithub](https://user-images.githubusercontent.com/43758373/104843616-9ae9e000-58dc-11eb-8b4b-9e1a2628cd4d.PNG)

## Deploy the app to an Azure App Service

Create an App Service in Azure. In this example the App Service is cicd-nanodegree-haneen and the resource group is flask-app, you can either create it using Azure cloudShell or the portal itself.
In the Azure cloudShell type:

```
az webapp up -n cicd-nanodegree-haneen -g flask-app
```

Next, create the pipeline in Azure DevOps. More information on this process can be found [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops&WT.mc_id=udacity_learn-wwl). The basic steps to set up the pipeline are:

- Go to [https://dev.azure.com](https://dev.azure.com) and sign in.
- Create a new private project.
-Create a new service connection to Azure Resource Manager, select subscription and the app service.
- Create a new pipeline linked to your GitHub repo using GiThub YAML File.

Screenshot of the App Service in Azure:

![screenshot-webapp-service](https://user-images.githubusercontent.com/43758373/104779603-6a952b00-5790-11eb-9f6a-6a31b506364c.PNG)

Screenshot of a successful deployment of the project in Azure Pipelines:

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
Improving the model performance.

## Load testing

We can use locust to do a load test against our application locally. 

Install locust:
```
pip install locust
```
Ensure the app is running:
```
python app.py
```

Start locust:
```
locust
```
Open a browser and go to [http://localhost:8089](http://localhost:8089). Enter the total number of users to simulate, spawn rate, set the host to your <app-service>, and click Start Swarming:

![screenshot-loadtest](https://user-images.githubusercontent.com/43758373/104845357-0be1c580-58e6-11eb-99f6-dfdb58850aa1.PNG)

You can then watch the load test:

![screenshot-locust](https://user-images.githubusercontent.com/43758373/104845329-e1900800-58e5-11eb-9947-c5effbcfcea3.png)


## Demo 

A [Demo]



