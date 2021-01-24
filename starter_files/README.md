# Operationalizing Machine Learning in Microsoft Azure

The aim of this project is to operationalizing machine learning by creating a model and deploying it, so that we can get an endpoint URL that can easily be accessible by the end-user. In this project, we will be building an end-to-end Machine Learning Model on a dataset (i.e. Bank Marketing Dataset) and will be creating a model, deploying it, and consuming it, also we will be creating, publishing, and consuming a pipeline by creating a pipeline endpoint.

Following step will be followed in the project:

1. Creating Automated ML model
2. Deploy the model
3. Consuming the deployed model (Configuring Swagger documentation)
4. Create Pipeline
5. Consume created Pipeline and Deploy it

## Dataset
### Data Set Information:

The data is related with direct marketing campaigns of a Portuguese banking institution. The marketing campaigns were based on phone calls. Often, more than one contact to the same client was required, in order to access if the product (bank term deposit) would be ('yes') or not ('no') subscribed.

The classification goal is to predict if the client will subscribe (yes/no) a term deposit (variable y).

### Attribute Information:
#### Input variables:

#### bank client data:
1. age (numeric)
2. job : type of job (categorical: 'admin.','blue-collar','entrepreneur','housemaid','management','retired','self-employed','services','student','technician','unemployed','unknown')
3. marital : marital status (categorical: 'divorced','married','single','unknown'; note: 'divorced' means divorced or widowed)
4. education (categorical: 'basic.4y','basic.6y','basic.9y','high.school','illiterate','professional.course','university.degree','unknown')
5. default: has credit in default? (categorical: 'no','yes','unknown')
6. housing: has housing loan? (categorical: 'no','yes','unknown')
7. loan: has personal loan? (categorical: 'no','yes','unknown')

#### related with the last contact of the current campaign:
8. contact: contact communication type (categorical: 'cellular','telephone')
9. month: last contact month of year (categorical: 'jan', 'feb', 'mar', ..., 'nov', 'dec')
10. day_of_week: last contact day of the week (categorical: 'mon','tue','wed','thu','fri')
11. duration: last contact duration, in seconds (numeric). Important note: this attribute highly affects the output target (e.g., if duration=0 then y='no'). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.
    
#### other attributes:
12. campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
13. pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)
14. previous: number of contacts performed before this campaign and for this client (numeric)
15. poutcome: outcome of the previous marketing campaign (categorical: 'failure','nonexistent','success')
social and economic context attributes
16. emp.var.rate: employment variation rate - quarterly indicator (numeric)
17. cons.price.idx: consumer price index - monthly indicator (numeric)
18. cons.conf.idx: consumer confidence index - monthly indicator (numeric)
19. euribor3m: euribor 3 month rate - daily indicator (numeric)
20. nr.employed: number of employees - quarterly indicator (numeric)
    
#### Output variable (desired target):
21. y - has the client subscribed a term deposit? (binary: 'yes','no')


## Architectural Diagram
Following is Architecture Diagram of the project which will help have a glance over the steps performed in this project to achieve the desired output:

![Architecture Diagram](images/ArchitectureDiagram.png)

1. AutoML Run: In this we create a Automated ML model by selecting the Bank Marking dataset from Registered Dataset and create a compute cluster (Standard_DS12_v2) and 1 as maximum number of nodes. We will be run the Automated run as a Classification and setting the Exit Criterion to 1 hour and the Concurrency to 1.
2. Select the Best Model & Deploy: On completion of AutoML run, we will be selecting the best model and we will be deploying it and while deploying we will be using "Azure Container Instances" (ACI) and we will also enable "Authentication".
3. Enabling Application Insights: In order to Enable Application Insights we will be downloading config.json file by going into subscription details and then we need to change the deployed model name in logs.py file and set enable_application_insights to True. And run logs.py file this will enable application insights logs for deployed model.
4. Setup Swagger & interact with it: Then we will be using the swagger documentation endpoint provided in Azure for deployed model and copy content of it and create a swagger.json file and set the swagger documentation for your project by running its bash script and serve.py to serve the content of your projects swagger.json file.
5. Consume Model Endpoint: Next is we will consuming the deployed model we will do this the adding the uri and key in endpoints.py file by copying from deployed model's consume section.
6. Create pipeline via notebook: We will be uploading the notebook provided in the starter files and then modifying at required cells and then will be running the cells which will create the pipeline.
7. Consume created Pipeline: Once the pipeline is created we will runs the cells provided in notebook itself to consume the pipeline.
8. Publish Pipeline: Once pipeline is consumed we will then run the cells provided in notebook to publish the pipeline.

## Key Steps
### 1. Registered Datasets

Following are registered datasets

![Registered Datasets](images/Udacity_Registered_datasets.PNG)

### 2. Create Automated ML Experiment
Automated ML Experiment Run completed:
In this step, we created an Automated ML model using a registered dataset, creating a compute cluster, and running the model.

![Automated ML Experiment](images/Udacity_run_successfull.PNG)

Automated ML Experiment Run details

![Automated ML Experiment Details](images/Udacity_run_successfull_2.PNG)

### 3. Best Run Model
Best Run Model

![Best Run Model](images/Udacity_best_model.PNG)

### 4. Enable Application Insights
Update logs.py file to enable application insights and running it.
![Updates in logs.py](images/Udacity_logs_dot_py.PNG)

Application Insights Enabled Successfully for logging
![Application Insights Enabled](images/Udacity_application_insights_enabled.PNG)

### 7. Configuring Swagger Docs
Configuring swagger 
![Swagger default docs](images/Udacity_swagger_default.PNG)
![Swagger project docs](images/Udacity_swagger.PNG)

### 6. Consuming Endpoints
After adding endpoint uri and key in endpoints.py file and running the file

![Modifying Endpoints.py](images/Udacity_Endpoint_py.png)

![Consuming Endpoints](images/Udacity_endpoints.PNG)

### 7. Pipeline Created, Deployed and Consumed

![Pipeline created](images/Udacity_pipeline_created.PNG)

![Pipeline endpoint created](images/Udacity_pipeline_endpoint.PNG)

![Pipeline endpoint overview](images/Udacity_published_endpoint_overview.PNG)

## Screen Recording
Following is the url for screen recording: [link](https://shorturl.at/dpyGO) 


## Standout Suggestions
- Resolving data imbalance issue in the dataset can prevent the bais and could improve the model prediction even more.
- Trying out deep learning (neural net) option when training the model, this could improve the accuracy.
- Try setting the featurization parameter of the AutoMLConfig class to 'auto', meaning that the featurization step should be done automatically.
