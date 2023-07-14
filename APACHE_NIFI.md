# Apache Nifi 
* **Data Flow :-** Moving of data from source to destination.


* **Data Pipeline :-** Trasformation of data from source to destination in between.

* **ETL** :-

* ### Four V'S of nifi
* **Volume:** Volume refers to the amount of data that Apache NiFi can handle. NiFi is designed to efficiently handle large volumes of data, making it suitable for big data processing and real-time data streaming scenarios.

* **Velocity:** Velocity represents the speed at which data can be ingested, processed, and routed through Apache NiFi. NiFi is built to handle high-velocity data flows, allowing for real-time processing and streaming analytics.

* **Variety:** Variety refers to the diverse types and formats of data that NiFi can handle. NiFi supports a wide range of data formats, including structured, semi-structured, and unstructured data. It can handle data from various sources such as databases, files, sensors, APIs, and more.

* **Veracity:** Veracity represents the trustworthiness and reliability of data flowing through NiFi. NiFi provides mechanisms for data validation, cleansing, enrichment, and quality monitoring. It allows users to apply business rules and ensure the accuracy and consistency of data as it moves through the system.

* **what is Apache NIFI?**

    Apache NiFi is an open-source data integration and dataflow automation tool developed by the Apache Software Foundation. It provides a visual interface for designing, building, and managing data flows, allowing users to easily connect, route, transform, and process data from various sources and systems.

    NiFi was built to automate the flow of data between systems. It can propagate any data content from any source to any destination.


* ### Core Nifi Technologies 
* **Flow-based programming:** NiFi follows a flow-based programming model, where data flows through interconnected processors, which perform various operations on the data.
* **Data Provenance:** NiFi provides data provenance capabilities, which allow you to track the origin and history of data as it flows through the system. This feature is useful for auditing, troubleshooting, and data governance.

* **Processors:** Processors are the building blocks of dataflows in NiFi. They perform operations such as data transformation, routing, enrichment, filtering, and integration with external systems. NiFi comes with a rich set of built-in processors, and you can also develop custom processors.

* **FlowFile:** A FlowFile represents a unit of data in NiFi. It encapsulates the data payload and its associated metadata. FlowFiles flow through the system and are processed by processors.

* **Connections and queues:** NiFi uses connections and queues to transfer data between processors. Connections define the relationships between processors and control how data flows from one processor to another. Queues hold the data in transit, allowing NiFi to handle large volumes of data without overwhelming downstream systems.


* **Process Group** In Apache NiFi, a Process Group is a container or grouping mechanism that allows you to organize and manage a set of processors, connections, and other components as a single unit within a NiFi dataflow. It provides a way to modularize and encapsulate a portion of the overall dataflow, enabling easier management and reuse.

* **Controller Services:** Controller Services are reusable components that provide common services or resources to processors within a NiFi dataflow. They encapsulate functionality that can be shared across multiple processors, reducing redundancy and promoting reusability. Some common use cases for Controller Services include database connections, API credentials, encryption services, and data lookup services.


* What are input and output port?

* **Templates** :- Templates are the way to download the flow we have created  and we can share it with any one.

* **Funnal**:- In Apache NiFi, a funnel is a component that is used to merge multiple data flows into a single flow. It acts as a collection point where data from different sources or processors can be combined into a single stream for further processing or routing.


* **variable Registery**:- There are two ways to create variable Registery 

    1. By create a file inside the config folder and then add that file inside the nifi.properties at the enc inside the variable register , if you have multiple file you can use the , 

    2. If just by left click and add variable through UI.

* **Flow File Expiration**:- 

* **Data Provenance**:- Data Provenance is the feature to debug the flow for example there flow of 1-10 step so if you click on any processor there is an option of data provenance or in global menu so when you click you see the flow file in the graphical representation that what happen to the the flow file in the first step and so on.

* **Nifi Registery** :-


* **Nifi Cluster Config** :- 
There is file look in it called nifi cluster config

* Creating a custom processer:- 
    By using mavan archtype:- 


## Interview question 
* **What is Apache NiFi?**

    Apache NiFi is an open-source data integration tool that provides a web-based interface for designing, controlling, and monitoring data flows. It enables the automation of data movement between various systems, making it easy to ingest, transform, and route data in real-time.

* **What are the key features of Apache NiFi?**

    Key features of Apache NiFi include:

    * Powerful web-based user interface (UI) for designing and managing data flows.

    * Data provenance to track the origin and transformation of data.

    *  Scalability and high availability.

    * Data buffering and prioritization.

    * Built-in security and authentication mechanisms.

    * Extensible architecture with support for custom processors and extensions.

    * Integration with various data storage systems, messaging platforms, and analytics tools.

* How does NiFi handle dataflow failures?

    * NiFi provides several mechanisms to handle dataflow failures:

    * Data provenance allows you to track the flow of data and identify the point of failure.

    * Retry mechanisms can be configured at different points in the flow to reattempt processing.

    * Backpressure can be applied to slow down data producers to match the processing capabilities of downstream components.

    * Failure handling strategies such as routing to error queues or triggering notifications can be implemented using processors like HandleHttpRequest and HandleHttpResponse.

* Explain the concept of flowfiles in NiFi.

    Flowfiles are the fundamental unit of data in NiFi. They represent individual data packets or records flowing through a dataflow. A flowfile contains the data content along with attributes that provide metadata about the data. Flowfiles can be processed, transformed, and routed to different destinations based on the configured dataflow logic.

* What are NiFi processors?
    Processors are the building blocks of a NiFi dataflow. They perform specific operations on flowfiles, such as data transformation, enrichment, filtering, routing, or interaction with external systems. Processors can be chained together to form a data processing pipeline.

* How does NiFi ensure data security?
  NiFi provides several security features to protect data:

  * Secure Sockets Layer (SSL) encryption for data transmission.
  * Access control policies to restrict user permissions and control data access.
  * Encryption of sensitive data within flowfiles.
Integration with external authentication mechanisms like     LDAP or Kerberos.
  * Secure storage of sensitive properties using encrypted configuration files.
* Explain the concept of data provenance in NiFi.
    Data provenance in NiFi refers to the ability to track and trace the lineage of data as it moves through the dataflow. It allows you to understand where the data came from, what transformations were applied, and where it was sent. Provenance data includes attributes like source, processor, and event timestamps, enabling detailed auditing, debugging, and troubleshooting.

* How can NiFi handle large volumes of data?
    NiFi is designed to handle large volumes of data efficiently:

    * It uses a streaming architecture that enables data processing in real-time, without storing the entire data in memory.

    * NiFi's data buffering capabilities allow it to handle bursts of data by storing them temporarily until the downstream components are ready to process.

    * Parallel processing can be utilized by configuring multiple instances of processors to process data in parallel, distributing the workload.
* What is the role of NiFi's content repository?

    The content repository in NiFi is responsible for storing flowfile content securely and durably. It provides storage for the actual data content of flowfiles, enabling efficient and reliable data movement. NiFi supports multiple content repositories, including disk-based and distributed repositories like Apache Hadoop HDFS or Apache Cassandra.

* How can NiFi integrate with external systems?
    NiFi offers a wide range of processors and extensions to integrate with external systems:

    Processors for reading and writing data from various data storage systems, databases, messaging systems, and APIs.
    Custom processors can be developed using NiFi's Java-based development framework to interact with specific external systems or implement custom business logic.
    Integration with external systems can also be achieved using NiFi's processors for executing scripts, running command-line tools, or invoking custom scripts or programs.
    These are just a few sample questions that cover different aspects of Apache NiFi. Remember to adapt your answers based on your own experience and the specific requirements of the job you're interviewing for.



* How can NiFi handle dataflow scalability?
    NiFi provides scalability through its cluster management capabilities. By configuring a NiFi cluster, you can distribute the processing workload across multiple nodes, allowing for parallel processing and increased throughput. The nodes in the cluster communicate with each other to coordinate the flow of data and ensure high availability.

* Explain the concept of data routing in NiFi.
    Data routing in NiFi involves directing flowfiles to different paths based on defined conditions. NiFi offers various routing processors such as RouteOnAttribute, RouteOnContent, and RouteText, which evaluate flowfile attributes or content to determine the appropriate destination. Routing can be based on simple conditions like attribute values or complex rules using expression language and regular expressions.

* How does NiFi handle data prioritization?
    NiFi supports data prioritization through the use of prioritizers. Prioritizers determine the order in which flowfiles are processed based on defined criteria. For example, you can prioritize flowfiles based on their arrival time, size, or other custom attributes. This allows you to allocate processing resources to critical data or prioritize certain data over others when resources are limited.

* Can you explain the concept of data lineage in NiFi?
    Data lineage in NiFi refers to the ability to track the complete history and transformation of a specific flowfile. It allows you to trace the flowfile's journey through the dataflow, identifying all the processors and operations it went through, as well as the corresponding timestamps and attributes. Data lineage helps with data auditing, compliance, and troubleshooting by providing a clear understanding of how data was processed and transformed.

* How can NiFi handle fault tolerance and data recovery?
    NiFi offers built-in fault tolerance mechanisms to ensure data reliability:

    Data replication: You can configure data replication across multiple nodes in a NiFi cluster, allowing for data redundancy and resilience against node failures.
    Checkpointing: NiFi periodically saves checkpoint information, including the state of flowfiles, to disk. In the event of a failure, NiFi can recover from the last saved checkpoint, minimizing data loss.
    Data provenance: By capturing detailed data provenance information, NiFi can help in identifying and recovering from failures by providing insights into the flow of data and potential failure points.
    These additional questions cover more aspects of Apache NiFi, including scalability, routing, prioritization, data lineage, and fault tolerance. Make sure to prepare for a wide range of questions and practice providing clear and concise answers based on your understanding and experience with NiFi.


* How can you handle data transformation in NiFi?
    NiFi provides a variety of processors for data transformation, such as ConvertRecord, ReplaceText, SplitText, and JSONPathReader. These processors enable you to convert data formats, manipulate field values, split or merge data, extract information using expressions, and perform other transformations. By chaining these processors together, you can build complex data transformation pipelines within NiFi.

* Can you explain the concept of data buffering in NiFi?
    Data buffering in NiFi involves temporarily storing data to handle fluctuations in data flow rates. NiFi employs a combination of memory-based and disk-based buffering to manage data efficiently. When the incoming data rate exceeds the processing speed, NiFi stores the excess data in memory or on disk until the downstream components are ready to process it. This buffering mechanism ensures data integrity and prevents data loss.

* How can NiFi handle data enrichment?
NiFi offers processors for data enrichment, such as LookupRecord, which can enrich data using external data sources or lookup tables. The LookupRecord processor can match values in a flowfile against a lookup table and append additional information to the flowfile attributes. This allows you to augment data with additional context or metadata from external sources, enhancing its value and relevance.

* What is the role of NiFi's Flow Controller?
    The Flow Controller in NiFi is responsible for managing the overall flow of data within a NiFi instance. It controls the movement of flowfiles between processors, manages the scheduling of processors, and handles flowfile prioritization and routing decisions. The Flow Controller ensures that the dataflow adheres to the configured rules and maintains the desired processing behavior.

* How can you monitor and manage NiFi clusters?
    NiFi provides various monitoring and management capabilities for clusters, including:

    Cluster manager: A dedicated node responsible for managing the cluster and coordinating the communication between nodes.
    Cluster monitoring dashboard: A web-based interface that displays real-time metrics, status, and performance statistics of the cluster nodes.
    Load balancing: NiFi clusters automatically distribute the processing load across available nodes, ensuring efficient resource utilization.
    Node isolation: In case of failures or network issues, NiFi can isolate a node from the cluster to prevent potential disruptions to the overall dataflow.
