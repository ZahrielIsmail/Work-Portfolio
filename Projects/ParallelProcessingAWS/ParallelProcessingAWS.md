# Cryptocurrency News Validation

**Date:** June 10, 2024 

**Data Sources:**  
- X or Twitter (Tweets)  

**Tags:** Machine Learning, Sentiment Analysis, HTCondor, Parallel Processing, Hadoop Environment, AWS Servers

**Deployment:** N/A

---

## Project Overview

This project is an end-to-end pipeline designed to create a HTCondor Cluster built in AWS to do Sentiment Analysis on X (Formerly known as Twitter) data. The goal of this project is to test the viability of the methodology.

---

## Pipeline

Proposed Pipeline:

![Placeholder](/Projects/ParallelProcessingAWS/Image_1.jpg)

The phases are as follows:

- Phase 1 Data Scrapping:

Scrapping the data from twitter Using tweepy, removal of unnecessary or redundant data as well as any preprocessing steps
Load the Data into the RDS Database which also contains the Python files necessary to conduct the modelling

- Phase 2 Data Processing:

Submission Host extracts the Tweets.csv files from the RDS Database and submits the job via "Condor_submit" to distribute the data among three execution hosts as well as directing which model should be used for the processing
Execution Host receives the files and conducts the modelling process, after modelling is complete, certain matrices are noted and exported to the RDS Database
Matrices can be exported from the RDS Database for analysis outside of the AWS Ecosystem.

## Clusters

The clusters setup necessary for Phase 2 require components on the AWS environment with the following settings.

- HTCondorManager
- SubmissionHost // Requires setup of an NFS Kernel in this instance
- ExeuctionHost //Requires At least two instances, used within this proejct is 3 Instances, all three instances require NFS Common and mounting folders from SubmissionHost instance
- RDS Server

HTCondorManager
SubmissionHost // Requires setup of an NFS Kernel in this instance
ExeuctionHost //Requires At least two instances, used within this proejct is 3 Instances, all three instances require NFS Common and mounting folders from SubmissionHost instance
RDS Server

## Central Manager

The central managers role in the cluster is to manage the system resources as well as assigning jobs according to free execution hosts, the overall memory needed in this role is low, which provides a reason for the small memory size allocated to the instance. After the Central Manager node is created, it can be accessed via the EC2 terminal to initiate the setup phase. The following code is required to install HTCondor and set the role as central manager:

![Placeholder](/Projects/ParallelProcessingAWS/Image_2.jpg)

## Submission Host

The submission host will create the job request to be submitted to the execution hosts. It requires the central mangers private IP to form the cluster and also requires a job.sub file to submit the jobs. 

The following code is used to setup the submission host:

![Placeholder](/Projects/ParallelProcessingAWS/Image_3.jpg)

## Execution Host

The execution host are the workers of the cluster and will do the bulk of the processes. It requires the Central Managers IP to connect to the cluster. HTCondor

![Placeholder](/Projects/ParallelProcessingAWS/Image_4.jpg)

## Minor Scripts

The following script was setup to push all new files to github from the EC2 Instance:

![Placeholder](/Projects/ParallelProcessingAWS/Image_5.jpg)

## Sample Outputs

Several different models were used to predict the sentiments of a given tweet the following are some sample outputs of the models from the EC2 Instances:

![Placeholder](/Projects/ParallelProcessingAWS/Image_6.png)

![Placeholder](/Projects/ParallelProcessingAWS/Image_7.png)

A word cloud was also created to identify the distribution of words in positive sentiment tweets.

![Placeholder](/Projects/ParallelProcessingAWS/Image_8.png)

## Outcome

Based on the pipeline created we identified a few things:
- The pipeline is viable for the usecase but requires tuning to the ingestion method as ingestion via Github has its limitations (<500MB File size limit)
- Requires higher performance Execution hosts as time taken to process the tweets can be reduced significantly with higher processing power.

---