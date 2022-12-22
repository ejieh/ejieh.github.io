---
layout: post
tags: data-warehouse
---

Most modern data warehouses run on the cloud and often times, they have consumption based pricing model. Basically, some credits are pre-purchased and those credits are spent over time based on consumption. These data warehouses are often usually composed of storage and compute with the later being the major driver of cost. These costs tend to get out of hand over time as the business evolves. 
 
This phenomenon of runaway cloud costs is not just unique to modern data warehouses but other cloud platforms. In a recent survey from [Wanclouds](https://venturebeat.com/data-infrastructure/report-81-of-it-teams-directed-to-reduce-or-halt-cloud-spending-by-c-suite/), 4 in 5 IT leaders say they have been directed to reduce or take on no additional cloud spending. As rising costs and inflation soar, IT leaders have been tasked with keeping a tight watch on cloud costs. Consequently, a new discipline  of financial governance has emerged to manage the cost of running services on the cloud. 

The major goal of financial governance is to get a grip of cloud costs. It also has some secondary objectives around enabling improved budgeting and planning and also traceability - knowing the details about where those costs come from.

Below is a framework to get started on rolling out financial governance for your modern data warehouse. Kindly note, this can be extended to any cloud platform that is consumption based.

![Alt Text](/assets/img/financial_governance_2.png "Fig. 1: Framework for Financial Governance")


The framework shows the major components of financial governance. It is an iterative process that starts with monitoring cloud costs, controlling it and then optimizing it. Using the modern data warehouses, these 3 components are discussed in more details below

## Monitoring Costs of Modern Data Warehouses
Monitoring is the initial step in financial governance. This is basically getting insight into the cost of running your data processing, transportation and storage on the cloud. Most modern data warehouses have a view for monitoring costs and many times, it's a billing dashboard. 

Most times these out of the box billing dashboards show trends of consumption over time, the high detailed components of that costs (by region, database, compute) and a forecast for the year and (or) month. This is often not often detailed enough to enable traceability of costs which is a key goal of financial governance as stated earlier. With most of the out of the box billing views, it's bit difficult to know which team is responsible for most of the spending, how the costs are split across different tasks and most importantly link the spend to strategic objectives or value creation. For example, from the out of the box admin billing view, you can see the cost of query processing went up in a certain month but you wouldn't necessarily see why that happened.  

To improve traceability, there is a need for a more customized and business-centric view of the billing dashboard. To achieve this, there has to be a mature and sometimes creative implementation of access management in your modern data warehouse. This involves using resource tagging, defining access policies and role based assignment of resources when possible. This will enable you query the meta data table of the data warehouse with better customized filters based on these tags/policies to get a more granular and detailed billing dashboard. This will improve traceability and let you know more about costs - who, what, when and how. 

## Controlling Costs of Modern Data Warehouses
Monitoring the costs is good and controlling it takes it a step further. A huge selling point of running data workloads in the cloud is the easy of spinning up new services at will or scaling up on infrastructure demand. This is good and makes life easy. In the past, highly specialized skill set is needed to create new infrastructure but that's not the case anymore. New compute resources can be provisioned with a click of a button and sometimes, without even any human intervention. This is a nightmare when it comes to financial management. 

The first step in controlling cost is to properly define roles and permissions. A moderated approach in which users submit a request to an admin to spin up services will help control costs. Not all users of the tool or service should have permissions to spin up new databases or scale up compute. This might prove restrictive based on the scale of operations but it is often worth it. To make this a little bit less restrictive, a controlled sandbox can be provisioned for all users with a predefined a amount of credit per user to spend per month. The users have free reign to tryout any service for learning and development or experimental purposes. 

The next step is to provision the right amount and type of service for each of the business use cases you want to accomplish. A review of the development workflow and environments will be useful in this stage as well as the business goal. For example, the compute requirement for running embedded external facing customer reporting need to be always online and elastic. This is different from compute needed to run quarterly financial reports which can be scheduled.

So far, we have discussed the proactive approach to controlling costs. There is also the reactive part of controlling costs. Most modern data warehouses have some form of alerting mechanism when a predefined threshold is reached. For example, an email can be sent out when the budget allotment for a specific service in a time period is exceeded. These tools can be leveraged to help limit spending and apply corrective measures that will help reduce costs in the whenever there are outliers.

## Optimizing Costs of Modern Data Warehouses

Optimizing costs touches on driving efficiency and performance in your data operations on the cloud. It's great that you can monitor and trace costs. It's beautiful that costs are controlled. But, are you running efficient data workloads? Can you do more with the service you have provisioned without impacting the bottom lines?

The first step in optimizing costs is to identify and remove data processing workloads that are no more useful or have been orphaned. Those pipelines that feed a use case that's not relevant should be shut down. A decomissioning plan should be made for this where all stakeholders are aware. I've seen where just doing this has reduced cloud costs by up to 30%.

Another way to optimize costs is to revisit the data architecture. If a lot of cold data is noticed in the data warehouse (data that is not being consumed by the business), a data lake can be brought into the architecture to take in these cold data. Furthermore, as part of revisiting the data architecture, you can review the cadence of the batch processing of data along with the business stakeholders. It's been shown that processing a big batch once is cheaper than processing multiple mini-batches multiple times. 

Understanding the internals of your specific cloud data warehouse will help you write the queries in a way that optimizes for how the data warehouse was built. For example, here is a quote from the product documentation of Big Query:

> Applying a `LIMIT` clause to a `SELECT *` query does not affect the amount of data read. You are billed for reading all bytes in the entire table

This means that if I have a table of 10 million rows and I limit by 1 in my filter, I will be charged for reading 10 million rows using Big Query. 

Understanding the internal workings of your specific data warehouses can't be overstated as it will help you with some common data warehouse performance optimization practices such as table schema optimization, data clustering, query plans examination and compute resources scale optimization. These help to reduce costs too.

Running a data warehouse on the cloud brings huge benefits to any data-driven business. Financial Governance of the data warehouse will go a long way in reaping those benefits.
