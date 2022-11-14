# Designing-A-Data-Pipeline

According to a [McKinsey Global Institute study](https://www.mckinsey.com/capabilities/growth-marketing-and-sales/our-insights/five-facts-how-customer-analytics-boosts-corporate-performance), data-driven businesses are 23 times more likely to acquire new customers, nine times more likely to keep customers, and 19 times more likely to be profitable. However, data volumes (and sources) are on the rise. As a result, organizations must seek the most efficient way to collect, transform, and extract value from data to stay competitive.

A data pipeline is a sequence of components that automate the collection, organization, movement, transformation, and processing of data from a source to a destination to ensure data arrives in a state that businesses can utilize to enable a data-driven culture.

Data pipelines are the backbones of data architecture in an organization. Implementing a well-designed, robust, and scalable data pipeline in your organization can help your organization effectively manage, analyze, and organize the copious amount of data to deliver business value.

# Common Data Pipeline Use Cases
Data pipelines have use cases in virtually any industry or company today. It could be as simple as transferring data from a source to a destination or as complex as transforming data for machine learning recommendation engines that improve product offerings. Some common data pipeline use cases include:

Processing and storing transaction data to power reporting and analytics to enhance business products and services.
Consolidating data from multiple sources (SaaS tools, databases) to a big data store (data warehouses, data lakes) to provide a single source of truth for the organization’s data
Improving overall backend system performance by migrating data to large data stores, reducing the load on operational databases
Ensuring data quality, reliability, and consistency for faster data access across business units

# Six Components of a Data Pipeline

## Data sources
The first component of the modern data pipeline is where the data originates. Any system that generates data your business uses could be your data source, including:

- Analytics data (user behavior data)
- Transactional data (data from sales and product records)
- 3rd party data (data your company doesn’t collect directly but uses)
## Data collection/ingestion
The next component in the data pipeline is the ingestion layer responsible for bringing data into the data pipeline. This layer leverages data ingestion tools such as Striim to connect to various data sources (internal and external) over a variety of protocols. For example, this layer can ingest batch (data at rest) and streaming (data in motion) data and deliver it to big data storage targets.

## Data processing 
The processing layer is in charge of transforming data into a consumable state through data validation, clean-up, normalization, transformation, and enrichment. Depending on the company’s specific architecture, ETL (Extract Transform Load) vs. ELT (Extract Load Transform), the data pipeline can do this processing component before or after data is stored in the data store.

In an ETL-based processing architecture, the data is extracted, transformed, then loaded into the data stores; this is mainly used when the data storage is a data warehouse. In ELT-based architectures, data is first loaded into data lakes and then transformed to a consumable state for various business use cases.

## Data storage
This component is responsible for providing durable, scalable, and secure storage for the data pipeline. It usually consists of large data stores like data warehouses (for structured data) and data lakes ( for structured or semi-structured data ).

## Data consumption
The consumption layer delivers and integrates scalable and performant tools for consuming from the data stores. In addition, the data consumption layer provides analytics across the business for all users through purpose-built analytics tools that support analysis methodologies such as SQL, batch analytics, reporting dashboards, and machine learning.

## Data governance 
The security and governance layer safeguards the data in the storage layer and all other layers’ processing resources. This layer includes access control, encryption, network security, usage monitoring, and auditing mechanisms. The security layer also keeps track of all other layers’ operations and creates a complete audit trail. In addition, the other data pipeline components are natively integrated with the security and governance layer.

# How to Design a Data Pipeline in Eight Steps

There are many factors to consider when designing data pipelines, and early decisions have tremendous implications for future success. The following section is meant to be a reference point for asking the right questions from the start of the data pipeline design process.

For this guide, we’ll be designing a data pipeline for a hypothetical movie streaming company called “Strimmer.” Strimmer will offer a library of films and television series for subscribers to watch and will be available on all platforms (Web, iOS, and Android). As Strimmer developers, we want to implement a data pipeline that provides the data for the ML (machine learning) recommendation engine to improve movie recommendations for users.

Step 1: Determine the goal

When designing a data pipeline, the priority is to identify the outcome or value the data pipeline will bring to your company or product. At this stage, we ask relevant questions such as:

- What are our objectives for this data pipeline?
- How do we measure the success of the data pipeline?
- What use cases will the data pipeline serve (reporting, analytics, machine learning)?

*Strimmer:* For our Strimmer application, the data pipeline will provide data for the ML recommendation engine, which will help Strimmer determine the best movies and series to recommend to users.

Step 2: Choose the data sources

We then consider the possible data sources that’ll enter the data pipeline. At this stage, it’s critical to ask questions such as:

- What are all the potential sources of data?
- In what format will the data come in (flat files, JSON, XML)?
- How will we connect to the data sources?

*Strimmer:* For our Strimmer data pipeline, our data sources would include:

User historical data, such as previously watched movies and search behaviors stored in operational databases like SQL, NoSQL
User behavior data/analytics, such as when a user clicks a movie detail
3rd party data from social media applications and movie rating sites like IMDB

Step 3: Determine the data ingestion strategy

With the pipeline goal and data sources understood. We need to ask questions about how the pipeline will collect the data. At this point, we ask questions such as :

- What communication layer will we be using to collect data ( HTTP, MQTT, gRPC)?
- Would we be utilizing third-party integration tools to ingest the data?
- Are we going to be using intermediate data stores to store data as it flows to the destination?
- Are we collecting data from the origin in predefined batches or in real time?

*Strimmer:* For our Striimmer data pipeline, we’ll be using Striim, a unified real-time data integration and streaming tool, to ingest both batch and real-time data from the various data sources.

Step 4: Design the data processing plan

Once data has been ingested, it has to be processed and transformed for it to be valuable to downstream systems. At this stage, it’s necessary to ask questions such as:

- What data processing strategies are we utilizing on the data (ETL, ELT, cleaning, formatting)?
- Are we going to be enriching the data with specific attributes?
- Are we using all the data or just a subset?
- How do we remove redundant data?

*Strimmer:* To build the data pipeline for our Strimmer service, we’ll use Striim’s streaming ETL data processing capabilities, allowing us to clean and format the data before it’s stored in the data store. Striim provides an intuitive interface to write streaming SQL queries to correct deficiencies in data quality, remove redundant data, and build a consistent data schema to enable consumption by the analytics service.

Step 5: Set up storage for the output of the pipeline

Once the data has been processed, we must determine the final storage destination for our data to serve various business use cases. At this step, we ask questions such as:

- Are we going to be using big data stores like data warehouses or data lakes?
- Would the data be stored on cloud or on-premises?’
- Which of the data stores will serve our top use cases?
- In what format will the final data be stored?

*Strimmer:* Because we’ll be handling structured data sources in our Strimmer data pipeline, we could opt for a cloud-based data warehouse like Snowflake as our big data store.

Step 6: Plan the data workflow

We then need to design the sequencing of processes in the data pipeline. At this stage, we ask questions such as:

- What downstream jobs are dependent on the completion of an upstream job?
- Are there jobs that can run in parallel?
- How do we handle failed jobs?

*Strimmer:* In our Strimmer pipeline, we can utilize a third-party workflow scheduler like Apache Airflow to help schedule and simplify the complex workflows between the different processes in our data pipeline via Striim’s REST API. For example, we can define a workflow that independently reads data from our sources, joins the data using a specific key, and writes the transformation output to our data warehouse.

Step 7: Implement a data monitoring and governance framework

In this step, we establish a data monitoring and governance framework, which helps us observe the data pipeline to ensure a healthy and efficient channel that’s reliable, secure, and performs as required. In this step, we determine:

- What needs to be monitored?
- How do we ensure data security?
- How do we mitigate data attacks?
- Is the data intake meeting the estimated thresholds?
- Who is in charge of data monitoring?

*Strimmer:* We need to ensure proper security and monitoring in our Strimmer data pipeline. We can do this by utilizing fine-grained permission-based access control from the cloud providers we use, encrypting data in the data warehouse using customer-managed encryption keys, storing detailed logs, and monitoring metrics for thresholds using tools like Datadog.

Step 8: Plan the data consumption layer

This final step determines the various services that’ll consume the processed data from our data pipeline. At the data consumption layer, we ask questions such as:

- What’s the best way to harness and utilize our data?
- Do we have all the data we need for our intended use case?
- How do our consumption tools connect to our data stores?

*Strimmer:* The consumption layer in our Strimmer data pipeline can consist of an analytics service like Databricks that feeds from data in the warehouse to build, train, and deploy ML models using TensorFlow. The algorithm from this service then powers the recommendation engine to improve movie and series recommendations for all users.

# Flexibility and Scalability are the Keys to Sustainable Data Pipelines

Data pipelines allow companies to make better and faster decisions, gain a competitive advantage, and garner significant value from their ever-growing amounts of data. Therefore, designing a future-proof data pipeline that scales as your data volume increases and is flexible to meet the ever-changing data use cases is paramount.
