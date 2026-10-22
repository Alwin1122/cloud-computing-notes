# Unit 5 — Edge Cloud Services: 1-mark MCQ bank

Three chapters from the Unit 5 notes: **Amazon Web Services**, **Microsoft Azure**, and **Google App Engine**.

**How to sit this.** Cover the answer pages. Choose the **best** option. Then read the one-line reason. A 1-mark paper gives the mark for the right job of the right service. If you can say the reason aloud, a reworded question still falls the same way.

There is **no negative marking** assumed. One question, one mark.

Four ideas unlock almost every question:

1. **Same job, three clouds.** Learn the row (virtual machine, serverless function, object storage, IoT hub, edge runtime, stream, monitor, ML). The product name is just the column.
2. **Edge acts now and sends less. Cloud remembers, compares sites, and trains.** Latency, bandwidth, reliability, and scale are the four reasons. Do not swap them.
3. **Security is not one product.** EC2 uses a virtual firewall. S3 uses bucket controls and IAM. IoT Core uses X.509 certificates. IAM itself starts from **deny**.
4. **App Engine hierarchy.** Application contains services. A service contains versions. A version runs on instances. Traffic splitting tests a new version without throwing away the old one.

---

# Chapter A — Amazon Web Services

Compute, storage, IoT, edge, streaming, monitoring, security, industrial data, and the digital twin.

### A1
In this chapter, Amazon Web Services is best understood as

a) one virtual-machine product and nothing else  
b) a cloud platform covering compute, storage, networking, databases, IoT, analytics, AI/ML, monitoring, security, and edge computing  
c) an on-premises cable protocol such as Modbus  
d) a 3D file format

### A2
A team wants virtual computers, a choice of Linux or Windows from a template, and the ability to grow or shrink that capacity in minutes. The service is

a) AWS Lambda  
b) Amazon EC2  
c) AWS IoT TwinMaker  
d) Amazon CloudWatch

### A3
An Amazon Machine Image (AMI) is

a) a template used to launch an EC2 instance with an operating system such as Linux or Windows  
b) the bill for a function that is not running  
c) a JSON permissions document  
d) a buffer inside a live data stream

### A4
Elasticity of EC2 means

a) capacity scales up or down within minutes as application traffic changes  
b) the operating system is rewritten on every request  
c) objects become visible to readers only after a day  
d) the edge box keeps working and never needs to synchronise

### A5
The EC2 pricing models named in the notes are

a) On-Demand, Spot Instances, and Savings Plans  
b) Device Shadow, Registry, and Rules Engine  
c) Standard and Flexible  
d) a single price for a physical server you must purchase

### A6
You pay EC2 for

a) the capacity you actually use  
b) nothing at all, even while an instance is running, because EC2 is always free  
c) the number of X.509 certificates only  
d) 3D models imported into a scene

### A7
The protection the EC2 notes attach to the workload is

a) a virtual firewall  
b) an X.509 certificate on the device gateway  
c) traffic splitting between application versions  
d) a stream shard

### A8
AWS Lambda is

a) an event-driven, serverless Function-as-a-Service: you provide code, and you do not provision or manage the servers  
b) a virtual computer you patch and keep running  
c) object storage addressed from the Internet  
d) a 3D operational twin of a factory

### A9
Lambda’s event-driven model, in the order given in class, is

a) Trigger, then Execution, then Action  
b) Registry, then Shadow, then Broker  
c) Filter, then train a model for a year, then stop the machine  
d) Workspace, then Scene, then Connector

### A10
Which set contains only Lambda triggers named in the notes?

a) a file uploaded to Amazon S3, an HTTP request through Amazon API Gateway, a new row in Amazon DynamoDB  
b) choosing an AMI, bidding on a Spot Instance, buying a Savings Plan  
c) OPC-UA, Modbus, and a Grafana panel  
d) version rollback, traffic splitting, and scale-to-zero

### A11
During Execution, AWS runs the Lambda code in

a) an isolated, lightweight container using Firecracker MicroVM technology  
b) a virtual machine you launched and configured yourself that morning  
c) the device’s offline JSON document  
d) a content-delivery cache

### A12
When the Lambda function has finished its task, it

a) shuts down, and you pay nothing while the code is not running  
b) stays logged-in so you can administer its operating system  
c) is saved automatically as an AMI  
d) must be rebuilt as a 3D scene before it can run again

### A13
The Lambda bill is calculated from

a) the number of requests and the execution duration in milliseconds  
b) the AMI size, whether or not any code runs  
c) a yearly fee for the building that houses the servers  
d) how many users sit in one IAM group

### A14
Lambda grows from one request a day to tens of thousands of requests a second. The point of that claim is that

a) scaling is automatic and the architecture does not have to be redesigned  
b) each new traffic level needs a new application design  
c) scaling works only after you abandon every native language  
d) each extra request needs a new IAM user with a permanent password

### A15
Lambda’s native languages include Python, Node.js, Java, Go, C#, and Ruby. Another language is still possible through

a) the Custom Runtime API  
b) an EC2 virtual-firewall rule  
c) SiteWise Monitor  
d) a lifecycle rule on a bucket

### A16
Choose Lambda rather than EC2 when

a) the code should run for an event, you do not want to manage servers, and you do not want a bill while it sits idle  
b) you need a chosen operating system, a virtual firewall, and a machine that stays yours to run  
c) you need a publish/subscribe broker for millions of devices  
d) you need to drape live readings on a 3D building model

### A17
Choose EC2 rather than Lambda when

a) the workload is a virtual computer launched from an AMI, protected by a virtual firewall, and scaled as capacity you pay for while you use it  
b) the only work is a short function after an S3 upload, then shutdown  
c) an application must read a device’s desired state while the device is offline  
d) the only work is an interactive search of log text

### A18
Amazon S3 is

a) object storage for storing and retrieving any amount of data from anywhere on the Internet  
b) the MQTT entry point for devices  
c) the function runtime that shuts down after each event  
d) the hierarchy of industrial assets

### A19
Strong consistency in S3 means

a) a read immediately after a write sees that update  
b) readers are promised stale data for a long time  
c) every object is public unless someone remembers to lock it  
d) objects cannot be organised in buckets

### A20
The S3 security tools named together in the notes are

a) Block Public Access, bucket policies, and IAM roles  
b) Firecracker, shards, and Scene Composer  
c) On-Demand, Spot Instances, and Savings Plans  
d) nucleus, lite, and the component SDK

### A21
Versioning, lifecycle rules, and object lock appear in the notes as S3’s

a) advanced options  
b) pricing models  
c) device protocols  
d) alarm types

### A22
AWS IoT Core, unlike Greengrass, is there to

a) connect devices and let them communicate securely with the AWS Cloud and with other AWS services  
b) be the local runtime that filters every sensor loop on the factory PC  
c) paint the 3D scene  
d) capture a camera feed for machine learning

### A23
The Device Gateway lets devices connect with

a) MQTT, HTTP, and WebSockets  
b) only an AMI  
c) GLB, CAD, and BIM  
d) Savings Plans

### A24
High-throughput, low-latency publish/subscribe for millions of devices is the job of the

a) Message Broker  
b) Scene Composer  
c) CloudWatch alarm  
d) S3 lifecycle rule

### A25
SQL-like filtering that routes device messages to Lambda or S3 is the job of the

a) Rules Engine  
b) Device Shadow  
c) Registry  
d) EC2 virtual firewall

### A26
The application must read or write a device’s state while the device is powered off or offline. Use the

a) Device Shadow, which keeps a virtual JSON state  
b) Registry alone, which organises identity and metadata but is not the offline state  
c) pricing model called Spot  
d) video store

### A27
The Registry is used to

a) organise device identities, attributes, and metadata  
b) run a function inside a Firecracker microVM  
c) deliver a stream into Redshift  
d) split user traffic between two releases of a web app

### A28
IoT Core’s own security statement is

a) end-to-end encryption and mutual authentication with X.509 certificates  
b) Block Public Access on a bucket  
c) a virtual firewall around an EC2 instance  
d) scale-to-zero of a sandboxed web runtime

### A29
Greengrass exists so that

a) local processing, messaging, data management, synchronisation, and ML inference can happen on the edge instead of sending everything to the cloud  
b) every reading must reach the cloud before any decision is allowed  
c) IAM users obtain permanent passwords  
d) web files are cached at viewers

### A30
A Greengrass core device is

a) an edge computer that runs the Greengrass software locally, for example an industrial PC, a Raspberry Pi, or another x86 or ARM machine  
b) one shard of a live stream  
c) a set of IAM users who share permissions  
d) one release of a web microservice

### A31
The notes say Greengrass Core software can run on

a) Linux and Windows, and on ARM and x86  
b) only a cloud region, never on the device itself  
c) only a browser tab  
d) only a machine that cannot run Linux

### A32
Sensor processing, filtering, aggregation, local analytics, ML inference, and data transformation are work for

a) Greengrass components at the edge  
b) IAM policies  
c) S3 Block Public Access  
d) EC2 Savings Plans

### A33
The link to the cloud fails. Greengrass should

a) keep operating locally, store the data, and synchronise with AWS IoT Core when connectivity returns  
b) freeze, because no local action is allowed without a round trip  
c) delete the device registry  
d) turn the core device into an AMI

### A34
“Local compute and action” on Greengrass means

a) Lambda functions, Docker containers, or native processes respond on the device without waiting for the cloud  
b) only a dashboard is allowed to run  
c) only an IAM role is allowed to run  
d) only a warehouse query is allowed to run

### A35
A small, resource-constrained Linux device should run aws-greengrass-lite because it is

a) a C runtime that uses small daemons on a system bus  
b) the Java runtime that manages deployments, process life cycles, and local IPC  
c) a billing plan for idle virtual machines  
d) the SQL dialect of the rules engine

### A36
aws-greengrass-nucleus, the usual Java runtime, is responsible for

a) local deployments, starting and stopping applications, and local interprocess communication  
b) importing CAD into a scene  
c) issuing long-term IAM passwords  
d) replacing object storage

### A37
Which pairing of Greengrass building blocks is correct?

a) shadow-manager keeps local offline state; secret-manager keeps encrypted Secrets Manager credentials on the device  
b) shadow-manager compiles container images; secret-manager allocates stream shards  
c) both are App Engine environments  
d) both are EC2 price lists

### A38
The software catalog and the component SDK differ because

a) the catalog indexes ready-made components; the SDK (C, C++, Rust) builds small custom components that use local IPC  
b) the catalog is a cloud region; the SDK is an AMI  
c) both are alarms on one metric  
d) the SDK is only a monthly bill

### A39
You must take in gigabytes per second from thousands of sources and buffer them, using shards or on-demand capacity. Choose

a) Amazon Kinesis Data Streams  
b) Amazon Data Firehose  
c) AWS IAM  
d) TwinMaker Scene Composer

### A40
A serverless delivery path should land the live data in Amazon S3 or Redshift. Choose

a) Amazon Data Firehose  
b) the IoT Registry  
c) an EC2 virtual firewall  
d) S3 object lock

### A41
A continuous SQL or Apache Flink program should analyse the stream as it arrives. Choose

a) Amazon Managed Service for Apache Flink  
b) S3 Block Public Access  
c) an AMI  
d) CloudFront

### A42
Video and audio from connected devices, stored so that machine learning can use them, belong in

a) Amazon Kinesis Video Streams  
b) an IAM group  
c) a Savings Plan  
d) the Greengrass component SDK

### A43
From the moment Kinesis ingests data to the moment a consumer can use it, the notes claim

a) sub-second latency  
b) a wait until the next month  
c) that you must own the disks before the first byte arrives  
d) the startup time of a Flexible environment virtual machine

### A44
Kinesis capacity and price, as stated in class, are

a) serverless growth to match volume, and pay-as-you-go on throughput or data volume  
b) one fixed server that is not allowed to grow  
c) free whenever a Spot Instance is also running  
d) charged once per IAM user

### A45
CloudWatch metrics, logs, alarms, and dashboards are, in that order,

a) numbers over time; text records of events; a rule on one metric that can notify or act; one view of many resources  
b) video files; AMIs; price lists; 3D scenes  
c) certificates; buckets; shards; software versions  
d) microservices; traffic splits; running copies; cloud projects

### A46
A CloudWatch alarm

a) watches a single metric and can fire a notification or an action such as Auto Scaling  
b) is the object store  
c) is the MQTT gateway  
d) is the digital-twin graph

### A47
You want to query log text quickly and interactively. Use

a) CloudWatch Logs Insights  
b) Anomaly Detection  
c) cross-account observability  
d) Scene Composer

### A48
Anomaly Detection and cross-account observability differ in that

a) Anomaly Detection uses machine learning to flag unusual metric behaviour; cross-account observability watches across AWS accounts and regions  
b) both are S3 advanced options  
c) Anomaly Detection issues X.509 certificates  
d) cross-account observability is the C runtime for tiny devices

### A49
AWS IAM is a free security service. Authentication and authorization mean

a) who can sign in, and which actions they may perform  
b) both words for object lock  
c) the shard count and the video format  
d) the two App Engine environments

### A50
Before a policy explicitly allows an action, IAM

a) denies it  
b) allows it for every new account  
c) publishes the resource on the Internet  
d) starts a Spot Instance

### A51
A person or an application with a password or a long-term access key is an IAM

a) user  
b) role  
c) policy  
d) alarm

### A52
Several people should share one set of permissions. Put the users in an IAM

a) group  
b) Firecracker microVM  
c) Kinesis shard  
d) 3D workspace

### A53
A trusted AWS service should get temporary credentials. Give it an IAM

a) role to assume  
b) user’s permanent password pasted into the source code  
c) dashboard  
d) bucket lifecycle rule

### A54
An IAM policy is

a) a JSON document, attached to an identity or a resource, that allows or denies actions  
b) a running virtual machine  
c) a unit of stream capacity  
d) a container for 3D models and entities

### A55
AWS IoT SiteWise is for

a) collecting, storing, organising, and monitoring industrial equipment data at scale  
b) renting a general-purpose virtual machine  
c) hosting a public website as PaaS  
d) delivering web content to browsers

### A56
SiteWise ingests industrial readings over

a) OPC-UA, MQTT, and Modbus, via SiteWise Edge or IoT Core rules  
b) GLB files only  
c) IAM groups only  
d) traffic splits between web versions

### A57
Asset modeling in SiteWise means

a) a virtual stand-in for equipment, including hierarchy, measurements, and computed metrics  
b) a Firecracker microVM  
c) a log-text query  
d) an AMI

### A58
While the cloud link is down, SiteWise’s edge processing is meant to

a) keep the on-premises data path and the local view alive  
b) erase history so the twin stays light  
c) cancel every EC2 instance  
d) change IAM’s default from deny to allow

### A59
No-code operational dashboards for this industrial data are built with

a) AWS IoT SiteWise Monitor or a tool such as Grafana  
b) the Custom Runtime API  
c) a Savings Plan  
d) object lock

### A60
Use TwinMaker rather than SiteWise alone when you need to

a) lay real-time, video, and enterprise data onto a 3D scene without moving that data out of the systems that already store it  
b) boot a Linux AMI  
c) pay for a function by the millisecond  
d) create a long-term access key

### A61
A TwinMaker workspace is

a) the container for the 3D models, data connections, and entities of the twin  
b) an EC2 price option  
c) a Kinesis shard  
d) an S3 lifecycle rule

### A62
Model Builder’s result is

a) entities and relationships that form a digital-twin graph  
b) a set of virtual firewalls  
c) a Spot bid  
d) the MQTT certificate store as its main product in this chapter

### A63
The built-in TwinMaker data connectors named in the notes are

a) AWS IoT SiteWise and Amazon Kinesis Video Streams  
b) Azure Blob Storage and Azure Monitor  
c) App Engine Standard and Flexible  
d) IAM users and IAM groups

### A64
Timestream and Snowflake appear in the TwinMaker notes as

a) further data sources a connector can reach, beyond the built-in ones  
b) EC2 pricing models  
c) Greengrass runtimes  
d) App Engine services

### A65
Scene Composer imports

a) 3D assets such as GLB, CAD, BIM, and point clouds  
b) IAM policies  
c) Lambda language runtimes  
d) Savings Plans

### A66
In the sample design, Amazon CloudFront is included for

a) content delivery  
b) ML inference on a Raspberry Pi  
c) mutual authentication of sensors  
d) Modbus collection

### A67
A vibration limit is crossed and the machine must be stopped at once. Place that decision

a) at the edge: a cloud round trip adds delay, and the link may be down  
b) only in next month’s warehouse report  
c) inside an IAM policy  
d) in a traffic split between two website versions

### A68
Forwarding every raw sample to the cloud is a weak design because

a) it wastes bandwidth; the edge should filter and aggregate, and forward the useful result  
b) object storage is unable to hold numbers  
c) Greengrass is not allowed to read a sensor  
d) IAM physically blocks radio signals

### A69
A year of readings from many plants, used to train a model, belongs in the cloud because

a) long-term multi-site data and the training job need scale; the finished model can still be inferred locally  
b) training is the emergency stop and must finish in a millisecond on the motor controller  
c) edge computers are the only disks in the design  
d) CloudFront is the training product

### A70
Which placement matches the case-study tests of latency, bandwidth, reliability, and scale?

a) Edge: immediate action, filtering, local inference, and survival of an outage. Cloud: stored history, cross-site analytics, training, and central monitoring.  
b) Edge: a year of training for every plant. Cloud: the emergency stop.  
c) Put the whole factory inside IAM, because IAM is free.  
d) Put the whole factory inside Scene Composer, because it imports CAD.

---

# Chapter B — Microsoft Azure

The same edge-cloud jobs, named as Azure services, plus the smart-factory split.

### B1
In this chapter, Microsoft Azure is

a) Microsoft’s cloud platform for compute, storage, networking, databases, AI/ML, analytics, IoT, monitoring, security, and edge computing  
b) a field protocol used by one sensor  
c) another name for an EC2 AMI  
d) the sandboxed App Engine runtime

### B2
The Azure match for Amazon EC2 is

a) Azure Virtual Machines  
b) Azure Functions  
c) Azure IoT Edge  
d) Azure Monitor

### B3
The Azure match for AWS Lambda is

a) Azure Functions  
b) Azure Blob Storage  
c) Azure IoT Hub  
d) Azure Machine Learning

### B4
The Azure match for Amazon S3 is

a) Azure Blob Storage  
b) Azure Stream Analytics  
c) Azure Event Hubs  
d) Azure IoT Edge

### B5
The Azure match for AWS IoT Core is

a) Azure IoT Hub  
b) Azure IoT Edge  
c) Azure Monitor  
d) Azure Functions

### B6
The Azure match for AWS IoT Greengrass is

a) Azure IoT Edge  
b) Azure IoT Hub  
c) Azure Event Hubs  
d) Azure Blob Storage

### B7
Azure Stream Analytics matches

a) Amazon Kinesis Data Analytics and the Managed Service for Apache Flink  
b) Amazon EC2  
c) AWS IAM  
d) Amazon CloudFront

### B8
Azure Event Hubs matches

a) Amazon Kinesis Data Streams, the large-scale ingest path  
b) Amazon S3  
c) AWS IoT TwinMaker  
d) Amazon CloudWatch

### B9
Azure Machine Learning matches

a) Amazon SageMaker  
b) AWS Lambda  
c) Amazon Kinesis Video Streams  
d) AWS IAM

### B10
Azure Monitor matches

a) Amazon CloudWatch  
b) AWS IoT Greengrass  
c) Amazon Data Firehose  
d) AWS IoT SiteWise

### B11
Which row is the wrong pairing?

a) Virtual Machines with EC2, Functions with Lambda, Blob Storage with S3  
b) IoT Hub with IoT Core, IoT Edge with Greengrass, Monitor with CloudWatch, Azure Machine Learning with SageMaker  
c) IoT Hub with Greengrass, and IoT Edge with IoT Core  
d) Event Hubs with Kinesis Data Streams, and Stream Analytics with stream processing such as Flink

### B12
Event Hubs and Stream Analytics are neighbours. The correct split is

a) Event Hubs takes in events and telemetry at large scale; Stream Analytics processes the live stream  
b) Event Hubs trains models; Stream Analytics stores CAD files  
c) both products are virtual machines you patch  
d) Event Hubs is the local runtime; Stream Analytics is the file store

### B13
Which list is the **edge** list in the Azure smart-factory notes?

a) local processing, filtering, aggregation, anomaly detection, local AI inference, immediate response  
b) long-term storage, historical analytics, model training, centralised monitoring, cross-site analysis, device management  
c) only device management and a year of training  
d) only blob archives and a monitoring tenant

### B14
Which task is a **cloud** task on that same list?

a) cross-site analysis of stored history  
b) stopping the machine the instant a limit is crossed  
c) dropping useless samples before they are transmitted  
d) producing a local inference result while the wide-area link is down

### B15
Immediate response stays at the edge because of

a) latency, and because the link may be down when the response is needed  
b) a rule that blob storage cannot hold a number  
c) a ban on using IoT Hub at all  
d) App Engine’s scale-to-zero behaviour

### B16
Filtering and aggregation stay at the edge because of

a) bandwidth: the cloud should receive a smaller stream, not every raw sample  
b) the default of an identity system  
c) the need to edit AMI templates  
d) the file types a scene editor imports

### B17
Model training is placed in the cloud, while local AI inference can stay at the edge, because

a) training wants long history and scale; inference wants a fast local answer  
b) training is the emergency stop  
c) inference is forbidden on an edge device  
d) blob storage cannot keep a CSV file

### B18
The case-study line that assigns the three Azure roles is

a) IoT Hub connects and manages devices; IoT Edge processes locally; the Azure cloud stores, analyses, and learns  
b) IoT Hub processes locally; IoT Edge only sends the bill; the cloud is unused  
c) all three exist only to draw dashboards  
d) IoT Edge removes the need for device identity

### B19
Azure IoT Hub provides a central cloud service for

a) device connectivity, device identity, device management, telemetry, cloud-to-device messages, and device-to-cloud messages  
b) executing the workload on the factory computer  
c) storing images and CSV files as its defining job  
d) building a digital-twin scene

### B20
Cloud-to-device and device-to-cloud communication are both duties of

a) Azure IoT Hub  
b) Azure Blob Storage  
c) one metric alarm  
d) a scene editor

### B21
Azure IoT Edge is the right service when

a) a cloud workload must be deployed and executed on the edge device, and the IoT Edge runtime manages that workload  
b) the only need is a cloud registry and no code runs on the device  
c) the only need is a place for unstructured files  
d) the only need is a log query

### B22
IoT Edge does not make IoT Hub unnecessary, because

a) Hub remains the cloud point that connects and manages devices; Edge is the local runtime  
b) Edge is a storage account for images  
c) Hub is a 3D file format  
d) the two names refer to Blob Storage

### B23
Choose Azure Functions when

a) code should run because an event happened, and you do not provision a server for it  
b) you need a virtual machine you administer  
c) you need to keep years of machine records as files  
d) you need the plant-wide device directory in the cloud

### B24
Choose Azure Blob Storage for

a) large unstructured data: sensor logs, CSV files, images, machine records, and historical IoT data  
b) real-time processing of a continuous stream  
c) temporary credentials  
d) a release of a web microservice

### B25
Stream Analytics fits IoT data because

a) the data is generated continuously, so processing it as a stream is the natural approach  
b) every device needs a password that never expires  
c) 3D models must be imported as point clouds  
d) an operating system must be picked from an image template

### B26
Azure Monitor becomes more important in an edge-cloud system because

a) many edge devices are spread out, and you still need health, performance, logs, metrics, and alerts  
b) a device outside the data centre cannot be observed by definition  
c) Monitor replaces IoT Edge and runs the local inference  
d) an alert is stored as a blob and needs no rule

---

# Chapter C — Google App Engine

Platform as a Service, the application hierarchy, Standard and Flexible, neighbouring Google Cloud services, and the three-cloud map.

### C1
Google App Engine is

a) Platform as a Service: developers concentrate on application code while Google manages much of the infrastructure  
b) a product that exists so you can create and patch every virtual machine yourself  
c) an industrial field protocol  
d) a JSON policy language

### C2
The notes contrast ordinary hosting with App Engine by saying that

a) the platform can scale the application, so the developer does not have to create servers by hand  
b) App Engine allows only one user  
c) ordinary hosting cannot be written in a programming language  
d) App Engine runs only while a factory network is offline

### C3
From the top of the hierarchy downward, an App Engine application is organised as

a) Application, then Services, then Versions, then Instances  
b) Instances, then Versions, then Services, then Application  
c) Shards, then delivery stream, then Flink, then video  
d) User, then Group, then Role, then Policy

### C4
The application itself is

a) the top-level container, created in a Google Cloud project, for the services, versions, and instances  
b) one running copy of one release  
c) the experimental release called v3  
d) a unit of stream capacity

### C5
Services are used to

a) divide a large application into logical components or microservices, each with its own function  
b) force every request to create a new cloud project  
c) apply object lock to a file  
d) authenticate a sensor with a certificate

### C6
In the shopping example, a User Service for login and a Product Service for the catalogue are

a) two services of one application  
b) two instances of one version  
c) two IAM roles  
d) two Kinesis shards

### C7
Versions of a service exist for

a) testing, deployment, rollback, staging, and traffic splitting  
b) storing images  
c) MQTT publish and subscribe  
d) Spot pricing

### C8
v1 is production, v2 is the release under test, and v2 fails. The move the notes describe is

a) send traffic back to v1  
b) delete the Google Cloud project  
c) convert the service into an AMI  
d) turn automatic scaling off for good

### C9
An instance is

a) a running copy of a version; when traffic rises, App Engine can run more of them  
b) the cloud project  
c) the microservice boundary  
d) an old release kept only so you can roll back

### C10
Automatic scaling means

a) the platform adds instances as the workload grows, without you creating those servers yourself  
b) you buy one instance and extra requests are discarded  
c) scaling starts only after the app is rewritten as an Azure virtual machine  
d) each new user requires a brand-new service

### C11
The Standard environment runs the application

a) in sandboxed instances, on supported runtimes  
b) as physical servers you patch in a lab  
c) as a fieldbus  
d) as an IAM role

### C12
Which bundle belongs to the Standard environment?

a) fast deployment, very fast startup, rapid scaling, strong isolation, scale-to-zero for a suitable app, and languages such as Python, Java, Go, Node.js, PHP, and Ruby  
b) slower startup on a virtual machine, custom Docker, and direct control of CPU and memory  
c) OPC-UA together with a device shadow  
d) On-Demand, Spot, and Savings Plans

### C13
Standard is the better environment when

a) the work is a web app or an API that must scale quickly, and the developer wants to stay on application code  
b) the work needs a custom runtime, unusual libraries, and a Docker image the sandbox will not run  
c) the work is a PLC protocol  
d) the work is a data warehouse

### C14
The Flexible environment runs App Engine instances on

a) Compute Engine virtual machines  
b) the Standard sandbox with no virtual machine underneath  
c) Azure IoT Hub  
d) IAM roles

### C15
You need control of CPU, memory, runtime, Docker, custom libraries, and networking. Choose

a) Flexible  
b) Standard, because its restrictions are what this requirement asks for  
c) a stream shard  
d) an IAM group

### C16
Which comparison agrees with the notes?

a) Standard starts very fast and is more restricted; Flexible starts more slowly, scales automatically, and allows custom Docker runtimes and more configuration  
b) Flexible starts faster and is not allowed to scale; Standard cannot run Python  
c) neither environment scales automatically  
d) Standard is a scene editor and Flexible is a device broker

### C17
“Can scale to zero for suitable applications” is stated for

a) the Standard environment  
b) every Flexible virtual machine, as the notes’ main claim for Flexible  
c) EC2 Spot Instances  
d) Kinesis Video Streams

### C18
Where the developer spends attention differs because

a) on Standard the focus is mainly the application code; on Flexible it is the code plus some environment configuration  
b) on Standard the focus is firewall rules, and Flexible forbids code  
c) both environments forbid other Google Cloud services  
d) Flexible forbids Docker

### C19
App Engine does not stand alone. Files for the application belong in

a) Cloud Storage  
b) a device shadow  
c) an AMI  
d) Modbus

### C20
Structured application data belongs in

a) Cloud SQL or Firestore  
b) Cloud Monitoring  
c) a virtual firewall  
d) the Greengrass C runtime

### C21
A warehouse for analysis, and a separate channel for events, are

a) BigQuery, and Pub/Sub  
b) Pub/Sub for the warehouse, and BigQuery for the event channel  
c) both IAM policies  
d) both Greengrass nuclei

### C22
The application’s health, metrics, and activity records are watched with

a) Cloud Monitoring and Cloud Logging  
b) an industrial asset model  
c) Spot Instances  
d) a certificate on a PLC

### C23
A further small piece of event-driven code beside App Engine can be

a) Cloud Functions  
b) an EC2 virtual firewall  
c) object lock  
d) a shard

### C24
Which list is a real set of App Engine advantages from the notes?

a) less infrastructure to manage, automatic scaling, versioning with traffic control, services as microservices, integration with other Google Cloud services, and monitoring and logging  
b) you administer the guest operating system of every instance  
c) only one programming language is permitted  
d) a bad version cannot have its traffic moved back

### C25
On the three-cloud map, application PaaS is

a) Google App Engine, AWS Elastic Beanstalk, Azure App Service  
b) Cloud Functions, AWS Lambda, Azure Functions  
c) Compute Engine, Amazon EC2, Azure Virtual Machines  
d) Cloud Run, Amazon ECS / Fargate, Azure Container Apps

### C26
On that map, cloud virtual machines are

a) Compute Engine, Amazon EC2, Azure Virtual Machines  
b) App Engine, Elastic Beanstalk, App Service  
c) BigQuery, Redshift, Synapse Analytics  
d) Vertex AI, SageMaker, Azure Machine Learning

### C27
On that map, serverless functions are

a) Cloud Functions, AWS Lambda, Azure Functions  
b) App Engine, Lambda, Blob Storage  
c) Cloud Run, EC2, IoT Hub  
d) Firestore, DynamoDB, Cosmos DB

### C28
On that map, a container application platform is

a) Cloud Run, Amazon ECS / AWS Fargate, Azure Container Apps  
b) App Engine, Elastic Beanstalk, App Service  
c) Cloud Storage, S3, Blob Storage  
d) Pub/Sub, Kinesis, Event Hubs

### C29
On that map, object storage is

a) Cloud Storage, Amazon S3, Azure Blob Storage  
b) BigQuery, Amazon Redshift, Azure Synapse Analytics  
c) Cloud SQL, Amazon RDS, Azure SQL Database  
d) Firestore, DynamoDB, Cosmos DB

### C30
On that map, the data warehouse is

a) BigQuery, Amazon Redshift, Azure Synapse Analytics  
b) Cloud Storage, S3, Blob Storage  
c) Cloud Monitoring, CloudWatch, Azure Monitor  
d) Cloud Functions, Lambda, Azure Functions

### C31
On that map, the cloud database row is

a) Cloud SQL / Firestore, Amazon RDS / DynamoDB, Azure SQL Database / Cosmos DB  
b) Cloud Storage, S3, Blob Storage  
c) BigQuery, Redshift, Synapse Analytics  
d) Vertex AI, SageMaker, Azure Machine Learning

### C32
On that map, monitoring is

a) Cloud Monitoring, Amazon CloudWatch, Azure Monitor  
b) Vertex AI, SageMaker, Azure Machine Learning  
c) Pub/Sub, Kinesis, Event Hubs  
d) Cloud Run, Fargate, Container Apps

### C33
On that map, the machine-learning platform is

a) Vertex AI, Amazon SageMaker, Azure Machine Learning  
b) Cloud Monitoring, CloudWatch, Azure Monitor  
c) App Engine, Elastic Beanstalk, App Service  
d) Compute Engine, EC2, Azure Virtual Machines

### C34
Cloud IoT connectivity on that map is

a) the Google Cloud IoT ecosystem and partner solutions, AWS IoT Core, and Azure IoT Hub  
b) three local PLCs and no cloud hub  
c) Cloud Storage, S3, and Blob Storage  
d) BigQuery, Redshift, and Synapse Analytics

### C35
The edge runtime on that map is

a) Google Distributed Cloud or Google’s edge solutions, AWS IoT Greengrass, and Azure IoT Edge  
b) App Engine, Elastic Beanstalk, and App Service  
c) Cloud Functions, Lambda, and Azure Functions  
d) Firestore, DynamoDB, and Cosmos DB

### C36
Streaming and event processing on that map is

a) Pub/Sub and Dataflow, Kinesis, and Event Hubs with Stream Analytics  
b) Cloud Storage, S3, and Blob Storage  
c) three copies of a virtual firewall  
d) Scene Composer, Grafana, and a CAD file

### C37
A university site handles about 2,000 requests an hour on a normal day and about 20,000 in exam week. Staff will not manage virtual machines, operating systems, or capacity, and they want controlled releases. The fitting platform is

a) App Engine  
b) one virtual machine sized only for a quiet day, with no release mechanism  
c) SiteWise, on the grounds that students are industrial sensors  
d) a device shadow

### C38
App Engine meets the jump from 2,000 to 20,000 requests an hour by

a) increasing the number of instances  
b) asking staff to order ten times as many servers that week  
c) deleting the production version  
d) writing the lecture videos into an IAM policy

### C39
Assignment submission should be its own part of the application. A new edition of that part should be introduced as

a) a new version of that service, with only some traffic pointed at it while the current version still serves the rest  
b) a new cloud project that throws away the whole university system  
c) an EC2 Spot Instance  
d) a Kinesis shard

### C40
Traffic splitting earns its place because

a) a fraction of students can try the new version; if it fails, traffic is moved back to the previous version  
b) it is the store for lecture videos  
c) it is the protocol that reads vibration sensors  
d) it removes the need for instances

### C41
For this portal — pages and APIs, fast growth, little operations work, ordinary supported languages — choose

a) the Standard environment  
b) the Flexible environment, because every website must bring its own Docker host  
c) neither environment, because App Engine cannot host a web application  
d) the Greengrass C runtime

### C42
Choose Flexible for a module of that same portal only when

a) the module needs a custom runtime, special libraries, or Docker that the Standard sandbox does not allow  
b) the priority is the fastest startup and the least configuration  
c) scale-to-zero is the main requirement named for that choice  
d) the module is an MQTT broker for sensors

### C43
Lecture videos and files to download belong in

a) Cloud Storage, beside the App Engine application  
b) the only copy on an instance’s temporary disk  
c) an IAM user’s password  
d) a Modbus register

### C44
Against managing virtual machines by hand, a tenfold spike when results are published is easier on App Engine because

a) instances follow demand, versions remain under traffic control, and staff are not patching servers or guessing capacity  
b) App Engine refuses every request above 2,000 an hour  
c) neither environment is allowed to scale  
d) publishing results deletes the previous version by itself

### C45
A sound sketch of the university system is

a) users reach the App Engine application; its services and versions run on instances; Cloud Storage holds the files; Cloud SQL or Firestore holds the records; Cloud Monitoring and Cloud Logging watch the app  
b) users reach the portal through Modbus and a device shadow, and App Engine is absent  
c) one machine image, with no versions and no store  
d) a single metric alarm and no application

---

# Answers — Chapter A

| Q | Answer | Why this is the best option |
|---|---|---|
| A1 | **b** | The opening slide lists the platform areas. AWS in this unit is the whole set, not one product. |
| A2 | **b** | EC2 rents instances. The OS comes from an AMI. Elasticity is the scale-in-minutes claim. Lambda is not that rented machine. |
| A3 | **a** | An AMI is the template. Linux and Windows are the examples in the notes. |
| A4 | **a** | Elasticity is a change in compute capacity as traffic changes, within minutes. |
| A5 | **a** | On-Demand, Spot Instances, and Savings Plans are the three models named with EC2. |
| A6 | **a** | The notes: pay for the capacity you use. “Always free while running” is Lambda’s idle claim, not EC2’s. |
| A7 | **a** | EC2’s security bullet is the virtual firewall. X.509 belongs to IoT Core. Traffic splitting belongs to App Engine. |
| A8 | **a** | Lambda is event-driven FaaS. You do not provision, configure, or manage the servers. |
| A9 | **a** | Trigger, Execution, Action. The function then shuts down. |
| A10 | **a** | The three example triggers are an S3 upload, an API Gateway HTTP request, and a new DynamoDB row. |
| A11 | **a** | Execution uses an isolated lightweight container on Firecracker MicroVM technology. You do not launch that VM yourself. |
| A12 | **a** | The action finishes and the function shuts down. No running code means no charge. |
| A13 | **a** | Requests plus duration in milliseconds. Idle code is not a bill. |
| A14 | **a** | The notes say this range needs zero architecture modifications. |
| A15 | **a** | Anything outside the native list uses the Custom Runtime API. |
| A16 | **a** | Event, no server work, no idle bill: Lambda. A chosen OS and a firewall is EC2. A broker is IoT Core. A 3D scene is TwinMaker. |
| A17 | **a** | A machine you launch from an AMI and protect with a virtual firewall is EC2. The other options are Lambda, the Device Shadow, and Logs Insights. |
| A18 | **a** | S3 is object storage, any amount, from anywhere on the Internet. |
| A19 | **a** | Strong consistency here means instant read-after-write. |
| A20 | **a** | Those three are the security tools. The other sets are Lambda, EC2 prices, and Greengrass. |
| A21 | **a** | Versioning, lifecycle rules, and object lock are the advanced options, listed apart from the security tools. |
| A22 | **a** | IoT Core connects devices to the cloud. Greengrass is the local processing runtime. |
| A23 | **a** | The gateway protocols in the notes are MQTT, HTTP, and WebSockets. |
| A24 | **a** | The Message Broker is the pub/sub path for a very large number of devices. |
| A25 | **a** | The Rules Engine filters with SQL-like syntax and routes to services such as Lambda or S3. |
| A26 | **a** | The shadow is the virtual JSON state for a device that is not online. The registry holds identity and metadata. |
| A27 | **a** | Registry: identities, attributes, metadata. It is not the function runtime, the delivery stream, or a web release. |
| A28 | **a** | IoT Core’s security bullet is encryption plus mutual authentication using X.509. The other locks belong to other services. |
| A29 | **a** | Greengrass is the edge runtime and cloud service for local processing, messaging, data management, sync, and ML inference. |
| A30 | **a** | The core device is the edge computer running the Greengrass software. The examples include an industrial PC, a Raspberry Pi, and x86 or ARM machines. |
| A31 | **a** | The notes: Linux and Windows, ARM and x86. The software runs on the device. |
| A32 | **a** | Those jobs are the component list: processing, filtering, aggregation, analytics, inference, transformation, communication, application logic. |
| A33 | **a** | Offline operation keeps local processing and storage, then syncs to IoT Core when the network returns. |
| A34 | **a** | Local compute is Lambda, Docker, or a native process, without a cloud round trip. |
| A35 | **a** | Lite is the C runtime for a constrained Linux device. The Java nucleus is the fuller runtime. |
| A36 | **a** | Nucleus manages deployments, process start and stop, and local IPC. |
| A37 | **a** | shadow-manager: local offline state. secret-manager: Secrets Manager credentials, encrypted, on the device. |
| A38 | **a** | The catalog is an index of components. The SDK builds your own small C, C++, or Rust components that use IPC. |
| A39 | **a** | Kinesis Data Streams is the scalable buffer: huge ingest, shards or on-demand capacity. |
| A40 | **a** | Firehose is the serverless delivery stream into a lake, warehouse, S3, or Redshift. |
| A41 | **a** | Continuous SQL or Flink is the Managed Service for Apache Flink, not the delivery stream and not the video store. |
| A42 | **a** | Kinesis Video Streams captures, processes, and stores video and audio for machine learning. |
| A43 | **a** | The benefit named is sub-second latency from ingestion to consumption. |
| A44 | **a** | Capacity adjusts without physical infrastructure, and the price follows throughput or volume. |
| A45 | **a** | Metrics are numbers, logs are text, an alarm is a rule on one metric, a dashboard is the combined view. |
| A46 | **a** | One metric, then a notification or an action. Auto Scaling is the example action. |
| A47 | **a** | Logs Insights queries logs. Anomaly Detection watches metrics. Cross-account observability spans accounts and regions. |
| A48 | **a** | Machine learning on metrics, versus one view across accounts and regions. |
| A49 | **a** | Sign-in is authentication. What you may do is authorization. |
| A50 | **a** | The default is deny until a policy allows the action. |
| A51 | **a** | A user has the long-term credentials: a password or a permanent access key. |
| A52 | **a** | A group is a collection of users that share permissions. It is not an identity you assume. |
| A53 | **a** | A role is assumed and yields temporary credentials. A permanent key inside code is the habit the notes are steering you away from. |
| A54 | **a** | The policy is the JSON allow/deny document, attached to an identity or a resource. |
| A55 | **a** | SiteWise collects, stores, organises, and monitors industrial equipment data. |
| A56 | **a** | OPC-UA, MQTT, and Modbus, through SiteWise Edge or IoT Core rules. |
| A57 | **a** | The asset model is the virtual equipment: hierarchy, measurements, computed metrics. |
| A58 | **a** | Edge processing keeps local pipelines and local visualisation during an outage. |
| A59 | **a** | SiteWise Monitor or Grafana supplies the no-code operational dashboard. |
| A60 | **a** | TwinMaker overlays data on a spatial scene and does not require that data to be moved or reingested. |
| A61 | **a** | The workspace holds the twin’s resources: models, connections, entities. |
| A62 | **a** | Model Builder creates the entities and relationships, and that becomes the twin graph. |
| A63 | **a** | Built-in connectors named in class: SiteWise and Kinesis Video Streams. |
| A64 | **a** | Timestream, Snowflake, and others are the further sources. They are not the built-in pair. |
| A65 | **a** | Scene Composer imports GLB, CAD, BIM, and point clouds. Grafana and the IoT App Kit are the view. |
| A66 | **a** | The sample list assigns CloudFront to content delivery. Greengrass, IoT Core, SiteWise, TwinMaker, and Lambda have the other jobs. |
| A67 | **a** | Immediate action is an edge job: latency, and reliability if the link is down. |
| A68 | **a** | Raw streams burn bandwidth. Filter and aggregate first. |
| A69 | **a** | Training on long, multi-site history is a cloud-scale job. Greengrass still lists ML inference as local work. |
| A70 | **a** | Edge: act now, send less, survive the outage. Cloud: keep history, compare sites, train, watch the estate. Those are the four justifications in the case study. |

---

# Answers — Chapter B

| Q | Answer | Why this is the best option |
|---|---|---|
| B1 | **a** | Azure is the platform. The field protocol, the AMI, and the App Engine sandbox are other chapters’ objects. |
| B2 | **a** | Virtual machines line up with EC2. |
| B3 | **a** | Functions line up with Lambda: event-driven, serverless. |
| B4 | **a** | Blob Storage is the object store, lining up with S3. |
| B5 | **a** | IoT Hub connects and manages devices, as IoT Core does. IoT Edge is the other IoT product. |
| B6 | **a** | IoT Edge runs workloads on the device, as Greengrass does. |
| B7 | **a** | Stream Analytics is the real-time processing match for Kinesis Data Analytics / Managed Flink. |
| B8 | **a** | Event Hubs is the large-scale ingest match for Kinesis Data Streams. The short class table writes “Kinesis” for this row; the detailed table says Kinesis Data Streams. |
| B9 | **a** | Azure Machine Learning lines up with SageMaker: develop, train, deploy. |
| B10 | **a** | Monitor lines up with CloudWatch: metrics, logs, alerts. |
| B11 | **c** | Hub is Core, Edge is Greengrass. Option c swaps them. The other rows match the table. |
| B12 | **a** | Ingest is Event Hubs. Processing the stream is Stream Analytics. Swapping them loses the mark. |
| B13 | **a** | That is the edge column: local processing through immediate response, including local AI inference. |
| B14 | **a** | Cross-site history is a cloud job. The other three must stay near the machine. |
| B15 | **a** | Latency, and reliability when the network is absent. |
| B16 | **a** | Bandwidth. Send the reduced result. |
| B17 | **a** | The slide puts training in the cloud and local AI inference at the edge. |
| B18 | **a** | The case-study sentence: connect and manage; process locally; store, analyse, and learn. |
| B19 | **a** | Hub is the cloud communication and management point, including both directions of messaging. |
| B20 | **a** | Both directions are listed under IoT Hub, not under storage or a dashboard. |
| B21 | **a** | Edge deploys and runs cloud workloads locally. The runtime manages them. |
| B22 | **a** | They divide one design. Hub does not execute the local module; Edge does not replace device management in the cloud. |
| B23 | **a** | Functions are the serverless, event-driven compute. |
| B24 | **a** | Those file examples are the Blob list: logs, CSV, images, machine records, historical IoT data. |
| B25 | **a** | Continuous generation is why a stream processor fits. |
| B26 | **a** | More devices, more places: health, performance, logs, metrics, and alerts still have to be seen. |

---

# Answers — Chapter C

| Q | Answer | Why this is the best option |
|---|---|---|
| C1 | **a** | App Engine is PaaS. Code is your job; much of the infrastructure is Google’s. |
| C2 | **a** | Scaling is the platform’s job. You are not asked to create servers by hand. |
| C3 | **a** | Application → Services → Versions → Instances. Reversing the chain is the usual miss. |
| C4 | **a** | One application resource in a Google Cloud project contains the rest. |
| C5 | **a** | A service is a logical part, a microservice, with its own function. |
| C6 | **a** | Login and catalogue are services. They are not “instances” and they are not “versions”. |
| C7 | **a** | A version is how you test, deploy, roll back, stage, and split traffic. |
| C8 | **a** | v1 stays. Traffic moves back to it. You do not destroy the application to abandon a bad release. |
| C9 | **a** | The instance is the running copy. Adding instances is the scaling mechanism. An old release kept for rollback is a version. |
| C10 | **a** | Traffic grows, instance count grows, and you do not create the servers yourself. |
| C11 | **a** | Standard: sandbox, supported runtimes. |
| C12 | **a** | Fast startup, rapid scale, isolation, scale-to-zero when it fits, and the named languages. Option b is Flexible. |
| C13 | **a** | Web apps and APIs, rapid scaling, low operational overhead, attention on code. |
| C14 | **a** | Flexible instances run on Compute Engine virtual machines. |
| C15 | **a** | CPU, memory, runtime, Docker, libraries, and networking are the Flexible control list. |
| C16 | **a** | Both can scale automatically. Standard is quicker and stricter. Flexible is slower to start and more open, including custom Docker. |
| C17 | **a** | Scale-to-zero is written for suitable Standard applications, not as Flexible’s headline. |
| C18 | **a** | Standard: mainly code. Flexible: code plus some environment configuration. |
| C19 | **a** | Cloud Storage is the file/object neighbour. App Engine does not replace it. |
| C20 | **a** | Cloud SQL and Firestore are the database neighbours named in class. |
| C21 | **a** | BigQuery analyses. Pub/Sub carries events. The comparison page pairs Pub/Sub with Dataflow for stream processing. |
| C22 | **a** | Cloud Monitoring and Cloud Logging are the watchers named beside App Engine. |
| C23 | **a** | Cloud Functions is the serverless neighbour. It is not the same row as App Engine. |
| C24 | **a** | Reduced infrastructure work, automatic scaling, versions, microservices, integration, monitoring, and several languages. |
| C25 | **a** | Application PaaS: App Engine, Elastic Beanstalk, App Service. Lambda is a different row. |
| C26 | **a** | Compute Engine, EC2, Azure Virtual Machines. |
| C27 | **a** | Cloud Functions, Lambda, Azure Functions. Do not put App Engine on this row. |
| C28 | **a** | Cloud Run, ECS/Fargate, Container Apps. That is the container row, not the PaaS row. |
| C29 | **a** | Cloud Storage, S3, Blob Storage. |
| C30 | **a** | BigQuery, Redshift, Synapse Analytics. A warehouse is not the object store. |
| C31 | **a** | Cloud SQL/Firestore, RDS/DynamoDB, Azure SQL/Cosmos DB. |
| C32 | **a** | Cloud Monitoring, CloudWatch, Azure Monitor. |
| C33 | **a** | Vertex AI, SageMaker, Azure Machine Learning. |
| C34 | **a** | The Google column is the IoT ecosystem and partner solutions, not a single product name. AWS is IoT Core. Azure is IoT Hub. |
| C35 | **a** | Google Distributed Cloud or Google’s edge solutions, Greengrass, IoT Edge. |
| C36 | **a** | Pub/Sub and Dataflow, Kinesis, Event Hubs and Stream Analytics. |
| C37 | **a** | They refuse to manage VMs and OS, they need automatic scale, and they need versions. That is the PaaS case. |
| C38 | **a** | The platform adds instances of the version. Staff do not place an order for servers. |
| C39 | **a** | The module is a service. The new edition is a version of that service. Traffic splitting keeps v1 in service. |
| C40 | **a** | A slice of traffic tries the new version. Failure sends traffic back. Videos are Cloud Storage’s job. |
| C41 | **a** | A normal web app that must scale fast with little operations work is the Standard case. |
| C42 | **a** | Flexible is for the custom runtime, the special library, or the Docker setup Standard will not give you. |
| C43 | **a** | Objects and files go to Cloud Storage. An instance disk is not the durable store in this design. |
| C44 | **a** | Tenfold traffic is more instances, plus the existing advantages: less infrastructure work and controlled versions. |
| C45 | **a** | Users, the application and its instances, storage, a database, and monitoring. That is the architecture the case study asks you to be able to draw. |

---

## If you only revise one page

| You are asked… | The best short answer |
|---|---|
| Rent a virtual machine | EC2, Azure Virtual Machines, Compute Engine |
| Run code on an event, no server to manage | Lambda, Azure Functions, Cloud Functions |
| Host the application and let the platform scale it | App Engine, Elastic Beanstalk, App Service |
| Store files and objects | S3, Blob Storage, Cloud Storage |
| Connect and manage devices in the cloud | IoT Core, IoT Hub |
| Process on the device, including an outage | Greengrass, IoT Edge |
| Take in a huge event stream | Kinesis Data Streams, Event Hubs |
| Analyse that stream continuously | Managed Flink / Kinesis analytics, Stream Analytics; on Google, Pub/Sub and Dataflow |
| Watch metrics, logs, and alerts | CloudWatch, Azure Monitor, Cloud Monitoring |
| Industrial plant data and asset models | AWS IoT SiteWise |
| 3D twin without copying the data out | AWS IoT TwinMaker |
| Web or API that must scale fast with little ops work | App Engine **Standard** |
| Custom runtime, Docker, or a say over CPU and memory | App Engine **Flexible** |
| Test a new release on a few users | a new **version**, then traffic splitting; the old version stays |
| Stop the machine now, or drop useless samples | **edge** (latency, bandwidth, reliability) |
| Train on a year of data from many sites | **cloud** (scale), then infer locally if the notes place inference at the edge |
