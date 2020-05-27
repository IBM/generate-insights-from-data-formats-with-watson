# Get recommendations by linking structured & unstructured data

In this code pattern, we will demonstrate a methodology to integrate structured data & unstructured data to generate recommendations. Processing unstructured data coming in different data formats has many challenges with respect to data extract & derive meaning to help us take informed decisions, however the related data would be in the structured format. It would be time consuming process to check different data sources manually for inference and that is where this pattern will be handy. We will showcase a configurable yet scalable process which will help in merging the different data sources and expedite the process of decision making. We have taken the example of HR recruitment process where we use the candidate's resume to be compared with job description & candidate database to identify the best suited candidate for a given job profile. This will help the HR to develop an efficient recruitment plan. Our motto is to select the right candidate which helps in risk mitigation for the organization thereby enhancing the ROI and increases the credibility for the recruitment process. We will be using Watson Studio & Watson NLU to solve this use-case.

When the reader has completed this code pattern, they will understand how to:

* Establish a relation between unstructured data & structured data for generating insights & recommendations.
* Extract and format unstructured data & structured data using configuerable Python functions.
* Use a configuration file to specify the job requirements to initiate data processing for a job profile.
* Use IBM Watson Natural Language Understanding API to extract metadata from documents in Jupyter notebooks.
* Create and run a Jupyter notebook in Watson Studio platform.
* Use Object Storage to access data and configuration files.
* Display the processed output along with recommendations in Watson Studio.

The intended audience for this code pattern is developers who want to learn a new method for scanning the text across different document format and establish a relation with the data stored in the structured format in a database. The distinguishing factor of this code pattern is that it allows a configurable mechanism of search optimization which allows the recruiter to select the best fit candidate for the role.

Some of the other use cases where this methodology can be applied are listed below.

> Drive optimization in the insurance domain by evaluating the information from the claim forms and new applicant forms.

By linking structured & unstructured data we can get recommendations for new leads, process improvements etc. Structured data will be in the form of product offering details & customer database where as the claim forms and new applicant forms will store unstructured data. How do we map them to extract insights, get recommendations, enhance efficiency, increase ROI & generate revenue are some of the highlights.  

* Ensure the application of best practices with rules-driven processes applied across lines of business, products and geographies.
* Automate core claim processes with intelligent case management so that claims operations function at the highest level of efficiency.
* Drive policyholder retention through intent-driven processes that adapt and respond dynamically to each claimant interaction to deliver the best outcome.

> Enhance the efficiency of spare parts in the automobile industry to reduce warranty claims by taking the customer feedback after the service.

Customer feedback is captured in a form which is unstructured where the keywords are extracted from the problem statement and compared with the inventory system having structured information to check the quality and durability. If there are repeated complaints about specific sku's then the manifacturing cycle of the specific sku's should be reviewed for improvements which can enhance the durability of the spare parts and can reduce the warranty claims. This will also help the R & D team to come up with new features for the existing components to deliver superior performance which can enhance the customer experience resulting in increased sales. 

Identifying the key parts causing the failure. Collecting failure descriptions to include:

* Complaint (operating condition report or symptoms)
* Cause (root cause or physical description)
* Corrective action (work accomplished)

Consolidate Warranty Systems & Processes. Minimize the number of automobile spare parts returns resulting in good inventory management. 


# Architecture Diagram
![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/architecture.png)

1. Post the job description with the query to identify suitable candidates
2. Input the candidate database, configuration file & candidate resumes into object storage
3. The query is processed in Watson Studio with the help of Watson NLU to process structured & unstructured data and generate recommendations
4. The recommendations with the suitable candidates are displayed as output which will be consumed by the recruiter to take informed decision.

## Included components

* [IBM Watson Studio](https://www.ibm.com/cloud/watson-studio): Analyze data using RStudio, Jupyter, and Python in a configured, collaborative environment that includes IBM value-adds, such as managed Spark.

* [IBM Cloud Object Storage](https://console.bluemix.net/catalog/infrastructure/cloud-object-storage): An IBM Cloud service that provides an unstructured cloud data store to build and deliver cost effective apps and services with high reliability and fast speed to market.

* [Watson Natural Language Understanding](https://console.bluemix.net/catalog/services/natural-language-understanding/?cm_sp=dw-bluemix-_-code-_-devcenter): A IBM Cloud service that can analyze text to extract meta-data from content such as concepts, entities, keywords, categories, sentiment, emotion, relations, semantic roles, using natural language understanding.

## Featured technologies

* [Data Science](https://developer.ibm.com/code/technologies/data-science/): Systems and scientific methods to analyze structured and unstructured data in order to extract knowledge and insights.
* [Analytics](https://developer.ibm.com/code/technologies/analytics/): Analytics delivers the value of data for the enterprise.
* [Python](https://www.python.org/): Python is a programming language that lets you work more quickly and integrate your systems more effectively.
* [Jupyter Notebooks](http://jupyter.org/): An open-source web application that allows you to create and share documents that contain live code, equations, visualizations and explanatory text.

# Watch the Video

[![](http://img.youtube.com/vi/wj39DepBVBg/0.jpg)](https://youtu.be/wj39DepBVBg)

# Steps

Follow these steps to setup and run this code pattern. The steps are
described in detail below.

1. [Create an account with IBM Cloud](#1-create-an-account-with-ibm-cloud)
1. [Create a new Watson Studio project](#2-create-a-new-watson-studio-project)
1. [Create IBM Cloud services](#3-create-ibm-cloud-services)
1. [Create the notebook](#4-create-the-notebook)
1. [Add the data and configuraton file](#5-add-the-data-and-configuraton-file)
1. [Update the notebook with service credentials](#6-update-the-notebook-with-service-credentials)
1. [Run the notebook](#7-run-the-notebook)
1. [Analyze the results](#8-analyze-the-results)

## 1. Create an account with IBM Cloud

Sign up for IBM [**Cloud**](https://console.bluemix.net/). By clicking on create a free account you will get 30 days trial account.

## 2. Create a new Watson Studio project

Sign up for IBM's [Watson Studio](http://dataplatform.ibm.com/). 

Click on New project and select Data Science as per below.

![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/new_project.png)

Define the project by giving a Name and hit 'Create'.

![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/define_project.png)

By creating a project in Watson Studio a free tier ``Object Storage`` service will be created in your IBM Cloud account. Choose the storage type as Cloud Object Storage for this code pattern.

## 3. Create IBM Cloud services

Create the following IBM Cloud service and name it wdc-NLU-service:

  * [**Watson Natural Language Understanding**](https://console.bluemix.net/catalog/services/natural-language-understanding)

  ![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/bluemix_service_nlu.png)

## 4. Create the notebook

* In [Watson Studio](https://dataplatform.ibm.com), click on `Create notebook` to create a notebook.
* Create a project if necessary, provisioning an object storage service if required.
* In the `Assets` tab, select the `Create notebook` option.
* Select the `From URL` tab.
* Enter a name for the notebook.
* Optionally, enter a description for the notebook.
* Enter this Notebook URL: https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/notebook/get_recommendations.ipynb
* Select the free Anaconda runtime.
* Click the `Create` button.

![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/images/create_notebook_from_url.png)

## 5. Add the data and configuraton file

[Clone this repo](https://github.com/IBM/generate-insights-from-data-formats-with-watson)
Navigate to [data](https://github.com/IBM/generate-insights-from-data-formats-with-watson/tree/master/data).

Use `Find and Add Data` (look for the `10/01` icon)
and its `Files` tab. From there you can click
`browse` and add data files from your computer. `Insert the three files as specified in the notebook.`

![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/add_file.png)

Note: The data files are in the `data` directory

## 6. Update the notebook with service credentials

#### Add the Watson Natural Language Understanding credentials to the notebook
Select the cell below `Add your service credentials from IBM Cloud for the Watson services` section in the notebook to update the credentials for Watson Natural Language Understanding. 

Open the Watson Natural Language Understanding service in your [IBM Cloud Dashboard](https://console.bluemix.net/dashboard/services) and click on your service, which you should have named `wdc-NLU-service`.

Once the service is open click the `Service Credentials` menu on the left.

![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/service_credentials.png)

In the `Service Credentials` that opens up in the UI, select whichever `Credentials` you would like to use in the notebook from the `KEY NAME` column. Click `View credentials` and copy `username` and `password` key values that appear on the UI in JSON format.

![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/copy_credentials.png)

Update the `username` and `password` key values in the cell below `Add your service credentials from IBM Cloud for the Watson services` section.

![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/add_credentials.png)

#### Add the Object Storage credentials to the notebook
* Select the cell below `Add your service credentials for Object Storage` section in the notebook to update the credentials for Object Store.
* Delete the contents of the cell

* Use `Find and Add Data` (look for the `10/01` icon) and its `Files` tab. You should see the file names uploaded earlier. Make sure your active cell is the empty one below `Add...`
* Select `Insert to code` (below your sample_config.txt file).
* Click `Insert Credentials` from drop down menu.
* Make sure the credentials are saved as `credentials_1`.

![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/add_obj_stg_credentials.png)

## 7. Run the notebook

When a notebook is executed, what is actually happening is that each code cell in
the notebook is executed, in order, from top to bottom.

> IMPORTANT: The first time you run your notebook, you will need to install the necessary
packages as mentioned in the notebook and then `Restart the kernel`.

Each code cell is selectable and is preceded by a tag in the left margin. The tag
format is `In [x]:`. Depending on the state of the notebook, the `x` can be:

* A blank, this indicates that the cell has never been executed.
* A number, this number represents the relative order this code step was executed.
* A `*`, this indicates that the cell is currently executing.

There are several ways to execute the code cells in your notebook:

* One cell at a time.
  * Select the cell, and then press the `Play` button in the toolbar.
* Batch mode, in sequential order.
  * From the `Cell` menu bar, there are several options available. For example, you
    can `Run All` cells in your notebook, or you can `Run All Below`, that will
    start executing from the first cell under the currently selected cell, and then
    continue executing all cells that follow.
* At a scheduled time.
  * Press the `Schedule` button located in the top right section of your notebook
    panel. Here you can schedule your notebook to be executed once at some future
    time, or repeatedly at your specified interval.

## 8. Analyze the results

We can evaluate the output for different requirements which will help in taking informed decisions. For ex :- There's a requirement for a user experience designer having 48 months experience and the query is passed onto our system which will showcase the results of two candidate profiles matching the criteria however we can see that candidate 1 has applied before and did not accept offer where as candidate 10 has not applied before and has a greater chance of accepting the offer if selected. HR can shortlist candidate 10 by taking informed decision as per the recommendation by our system which has internally analysed the CV and the candidate database. 

![](https://github.com/IBM/generate-insights-from-data-formats-with-watson/blob/master/doc/source/image/results.png)

The second example would be to query for candidate with good Machine Learning expertise and there are two candidates candidate 11 & candidate 14 fulfilling the requirement. Our system recommends candidate 11 because the candidate has master's degree in statistics and will be a better fit for the role even though candidate 14 has more experience. We are adding inference by reviewing the aspects from the CV to identify the best fit candidate for each role.

To sum up, we have demonstrated one methodology using Watson Natural Language Understanding & Watson Studio to analyze structured & unstructured data to generate recommendations which can be used in different domains for multiple usecases. 


# Related links

[Watson Text Classification](https://developer.ibm.com/patterns/extend-watson-text-classification/)


# Troubleshooting

[See DEBUGGING.md.](DEBUGGING.md)

# License

This code pattern is licensed under the Apache Software License, Version 2.  Separate third party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the Developer [Certificate of Origin, Version 1.1 (DCO)] (https://developercertificate.org/) and the [Apache Software License, Version 2] (http://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache Software License (ASL) FAQ](http://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)
