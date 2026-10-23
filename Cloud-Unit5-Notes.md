# Cloud Computing — Unit 5 Essential Notes

Edge Cloud Services. Three chapters from the lecture PDF: **Amazon Web Services**, **Microsoft Azure**, and **Google App Engine**.

Every topic is explained as: what it is, why it is used, and one example. The one-mark questions are in `Cloud-Unit5-1Mark.md`. Read this file first, then sit the questions.

---

## Table of Contents

**Chapter 1 — Amazon Web Services**

1. [What AWS is](#1-what-aws-is)
2. [EC2 — virtual machines](#2-ec2--virtual-machines)
3. [Lambda — run code when an event happens](#3-lambda--run-code-when-an-event-happens)
4. [S3 — object storage](#4-s3--object-storage)
5. [IoT Core — connect devices to the cloud](#5-iot-core--connect-devices-to-the-cloud)
6. [Greengrass — process on the device](#6-greengrass--process-on-the-device)
7. [Kinesis — live data streams](#7-kinesis--live-data-streams)
8. [CloudWatch — watch the cloud](#8-cloudwatch--watch-the-cloud)
9. [IAM — who may do what](#9-iam--who-may-do-what)
10. [SiteWise and TwinMaker — the plant and its twin](#10-sitewise-and-twinmaker--the-plant-and-its-twin)
11. [Where each job sits in a smart factory](#11-where-each-job-sits-in-a-smart-factory)

**Chapter 2 — Microsoft Azure**

12. [What Azure is, and the matching AWS service](#12-what-azure-is-and-the-matching-aws-service)
13. [IoT Hub and IoT Edge](#13-iot-hub-and-iot-edge)
14. [Functions, Blob, streams, and Monitor](#14-functions-blob-streams-and-monitor)
15. [The Azure smart-factory split](#15-the-azure-smart-factory-split)

**Chapter 3 — Google App Engine**

16. [App Engine is a platform, not a machine you patch](#16-app-engine-is-a-platform-not-a-machine-you-patch)
17. [Application, services, versions, instances](#17-application-services-versions-instances)
18. [Standard and Flexible](#18-standard-and-flexible)
19. [The other Google Cloud services beside it](#19-the-other-google-cloud-services-beside-it)
20. [The same job on three clouds](#20-the-same-job-on-three-clouds)
21. [The university case](#21-the-university-case)

---

# Chapter 1 — Amazon Web Services

## 1. What AWS is

Amazon Web Services is a cloud platform. You rent computing pieces instead of buying a data centre. The pieces used in this unit are compute, storage, networking, databases, IoT, analytics, machine learning, monitoring, security, and edge computing.

Two ideas run through the whole chapter.

- **Cloud** keeps what must last, be compared across sites, or be trained on a large history.
- **Edge** acts beside the machine, so a decision does not wait for a round trip, and the raw flood of sensor data does not have to travel.

| Job in this chapter | AWS service |
|---|---|
| Rent a virtual computer | Amazon EC2 |
| Run code when an event happens, with no server to manage | AWS Lambda |
| Store files and objects | Amazon S3 |
| Connect devices to the cloud | AWS IoT Core |
| Process on the device itself | AWS IoT Greengrass |
| Take in and analyse a live stream | Amazon Kinesis |
| Watch metrics, logs, and alarms | Amazon CloudWatch |
| Decide who may do what | AWS IAM |
| Industrial equipment data | AWS IoT SiteWise |
| A 3D working picture of the plant | AWS IoT TwinMaker |
| Deliver web content to viewers | Amazon CloudFront |

**Example.** A factory laptop reads vibration. Greengrass decides on the spot. IoT Core is how the device is known to AWS. S3 keeps the history. Lambda runs a short job when a new file lands. CloudWatch tells you if that job is failing.

## 2. EC2 — virtual machines

Amazon EC2 is Amazon Elastic Compute Cloud. It rents virtual computers, called **instances**, so you can run an application without buying the physical server.

**Elasticity** means the capacity can grow or shrink within minutes when traffic changes. You pay for the capacity you actually use.

Three pricing models are named in class:

- **On-Demand** — you pay for the instance while you use it, with no long commitment.
- **Spot Instances** — spare capacity at a lower price. It can be taken back, so it suits work that can stop and resume.
- **Savings Plans** — a commitment to a steady amount of use, in exchange for a lower price.

**Security** on the EC2 slide is a **virtual firewall** around the workload.

**Flexibility** comes from an **Amazon Machine Image (AMI)**. An AMI is a template. You pick Linux, Windows, or another operating system, and EC2 launches the instance from that template.

**Example.** A company needs a Linux server for a database that stays running all day. They choose an Ubuntu AMI, start an EC2 instance, and put a virtual firewall in front of it. When the festival sale starts, they add instances. When the sale ends, they remove them. They do not buy the hardware.

Choose EC2 when you need a machine you can log into, with an operating system you selected, that stays up while you are using it. Choose Lambda, next, when you only need a short piece of code after an event.

## 3. Lambda — run code when an event happens

AWS Lambda is event-driven and serverless. The service model is **Function as a Service (FaaS)**. You supply the code. AWS provisions the machine, patches it, scales it, and removes it. You do not launch an instance yourself.

Each run has three steps.

1. **Trigger.** Something happens. The notes use three examples: a file uploaded to S3, an HTTP request through API Gateway, or a new row in DynamoDB.
2. **Execution.** AWS starts an isolated, lightweight container using **Firecracker MicroVM** technology and runs your code inside it.
3. **Action.** The function does one job, such as reading the file, resizing an image, or updating a table, and then **shuts down**.

What you get from that design:

- No operating system to configure.
- Scale from one request a day to tens of thousands of requests a second without redesigning the application.
- The bill is the **number of requests** plus the **time in milliseconds**. If the code is not running, you pay nothing.
- Native languages: Python, Node.js, Java, Go, C#, and Ruby. Anything else uses the **Custom Runtime API**.

**Example.** A photo is dropped into an S3 bucket. That upload is the trigger. Lambda resizes the photo and writes the small copy back. The function exits. At 3 a.m., with no uploads, the bill for compute is zero. An EC2 instance left running at 3 a.m. would still be capacity you pay for.

## 4. S3 — object storage

Amazon S3 stores and retrieves any amount of data from anywhere on the internet. The unit of storage is an **object** (a file plus its metadata) kept in a **bucket**. It is not a virtual machine and it is not a database table.

**Strong consistency** means a read immediately after a write sees that write. You do not have to wait and hope the old copy disappears.

Security tools named together:

- **Block Public Access** — stop the bucket being opened to the world by mistake.
- **Bucket policies** — rules on the bucket itself.
- **IAM roles** — who is allowed to touch the objects.

Advanced options named beside those, not instead of them:

- **Versioning** — keep earlier copies when an object is overwritten.
- **Lifecycle rules** — move or expire objects as they age.
- **Object lock** — hold an object so it cannot be changed or deleted for a set period.

**Example.** A sensor summary is written to `factory-archive/line-2/today.csv`. The program reads it back at once and sees the new file. Block Public Access keeps the bucket private. A lifecycle rule can move files older than a year to cheaper storage. Versioning means yesterday’s overwritten report is still there if someone needs it.

## 5. IoT Core — connect devices to the cloud

AWS IoT Core is the managed front door between devices and AWS. It does not, by itself, run the factory’s local analytics. That is Greengrass. IoT Core connects, identifies, and carries messages.

What it provides: device connectivity, messaging, device identity, authentication and authorization, a message broker, rules, a device shadow, and device management.

| Piece | What it does | Example |
|---|---|---|
| Device Gateway | The entry. Devices connect with MQTT, HTTP, or WebSockets | A meter opens an MQTT session |
| Message Broker | Publish/subscribe for a very large number of devices, at high throughput and low delay | A thousand machines publish; only the subscribers of that topic receive the message |
| Rules Engine | Filters messages with SQL-like syntax and routes them | “If temperature > 90, send the message to Lambda or S3” |
| Device Shadow | A JSON copy of the device’s state, readable and writable even while the device is offline | The app sets “fan: on” at night. The device applies it when it reconnects |
| Registry | Identities, attributes, and metadata | “This is motor M205, line 2, installed in 2024” |
| Security | Encryption and mutual authentication with X.509 certificates | The device and the cloud each prove who they are |

Do not swap these. The broker moves messages. The shadow remembers desired state. The registry is the device’s identity card. The rules engine routes. The certificate proves identity.

**Example.** Motor M205 is powered off for maintenance. An engineer writes the desired speed into the shadow. The motor is off, so it cannot receive a live message. When it boots, it reads the shadow and applies the speed. The registry is only how AWS knows which motor this is. It is not the speed.

## 6. Greengrass — process on the device

AWS IoT Greengrass extends AWS onto the edge device. Work runs locally: processing, messaging, data management, synchronisation, and machine-learning inference. AWS describes it as an **edge runtime and a cloud service** together.

A **Greengrass core device** is the computer that runs the Greengrass software. Examples: an industrial PC, a Raspberry Pi, a Linux computer, an x86 machine, an ARM machine. The software runs on the device, on Linux or Windows, on ARM or x86. It is not “a virtual machine that exists only in the AWS region.”

**Components** are the programs on that device. They can filter, aggregate, run local analytics, run inference, transform data, communicate, and hold application logic.

Four capabilities to remember:

- **Local compute.** Lambda functions, Docker containers, or native processes act without waiting for a cloud round trip.
- **Offline operation.** During an outage the device keeps working and stores data. When the network returns, it synchronises with IoT Core.
- **Modular components.** Pre-built blocks such as a stream manager, an MQTT bridge, and a secret manager.
- **Two runtimes.** The usual **nucleus** is Java. It manages deployments, starts and stops applications, and provides local interprocess communication. **aws-greengrass-lite** is C, for a small Linux device, using small daemons on a system bus.

Other building blocks in the Greengrass GitHub organisation:

| Block | Job |
|---|---|
| aws-greengrass-nucleus | The Java runtime |
| aws-greengrass-lite | The small C runtime |
| software catalog | An index of ready-made components |
| component SDK | C, C++, and Rust tools for writing your own small components |
| shadow-manager | Keeps device state locally while offline |
| secret-manager | Keeps encrypted Secrets Manager credentials on the device |

**Example.** A press on the shop floor must stop if vibration spikes. The Greengrass core on the industrial PC sees the spike and opens the stop circuit. The cloud is not in that loop. If the factory link dies at the same moment, the PC still stops the press, stores the event, and sends it to IoT Core later. A tiny Linux board that cannot carry the Java nucleus uses greengrass-lite instead.

## 7. Kinesis — live data streams

Amazon Kinesis collects, processes, and analyses streaming data as it arrives. It is not object storage (that is S3) and it is not “is the server’s CPU high?” (that is CloudWatch).

| Piece | Job | Example |
|---|---|---|
| Kinesis Data Streams | A buffer. Ingests a very large flow, using shards or on-demand capacity | Thousands of machines publish readings continuously |
| Amazon Data Firehose | A delivery stream. Loads the flow into S3, Redshift, or another store, without you running the delivery servers | The stream lands in a data lake every minute |
| Managed Service for Apache Flink | Continuous analysis with SQL or Apache Flink | A running query: “count faults per line, right now” |
| Kinesis Video Streams | Video and audio from devices, for later machine learning | Cameras on the line, kept for a defect model |

Benefits named in class: sub-second delay from ingest to consumer, capacity that grows without a physical redesign, and pay-as-you-go on throughput or volume.

**Example.** Vibration readings enter Data Streams. Flink flags lines that look abnormal this minute. Firehose writes the hour’s data into S3 for the archive. The camera above the line goes to Video Streams, not into the temperature stream. CloudWatch is still there, but it is watching whether the Kinesis service itself is healthy, not replacing the stream.

## 8. CloudWatch — watch the cloud

Amazon CloudWatch monitors resources and applications. It collects numbers, text, and events.

| Piece | What it is | Example |
|---|---|---|
| Metric | A number over time | CPU percent, bytes on the network |
| Log | Text about what happened | An error line from Lambda |
| Alarm | A rule on **one** metric. It can notify someone or take an action such as Auto Scaling | “If CPU stays above 80%, add instances” |
| Dashboard | One screen for many resources | CPU, faults, and Lambda errors together |

Further features:

- **Logs Insights** — ask questions of the log text.
- **Anomaly Detection** — machine learning on metrics, to point at behaviour that is unusual rather than merely past a fixed line.
- **Cross-account observability** — one view across several AWS accounts and regions.

**Example.** Lambda errors spike after a bad deploy. Logs Insights finds the repeated message. An alarm on the error metric pages the on-call engineer. The dashboard is only the picture. The alarm is the rule that acts.

## 9. IAM — who may do what

AWS IAM is the free security service for identity. **Authentication** is who can sign in. **Authorization** is what they may do. Until a policy allows an action, the action is **denied**.

| Piece | What it is | How long the secret lives | Example |
|---|---|---|---|
| User | A person or an application | Long-term: a password or a permanent access key | Ada signs in to the console |
| Group | A set of users who share permissions | The users’ own credentials | “Factory-operators” all get the same read rights |
| Role | An identity that is assumed | Temporary | Lambda assumes a role that may write to one bucket |
| Policy | A JSON document attached to an identity or a resource | Not a login. It is the permission text | “Allow s3:GetObject on this bucket” |

A group is not something an application logs in as. A policy is not an identity. A role is what a service should use, so a permanent key is not pasted into source code.

**Example.** The resize function must write the small photo to S3. You do not put Ada’s access key in the code. You let the function assume a role whose policy allows that one write. Ada’s user account is for Ada. The group “photo-admins” is only a way to give several people the same rights.

This is a different lock from the others in the chapter. EC2 uses a virtual firewall. S3 uses bucket controls. IoT Core uses X.509 certificates. IAM uses users, groups, roles, and policies, and it starts from deny.

## 10. SiteWise and TwinMaker — the plant and its twin

These two are easy to merge, and the exam separates them.

**AWS IoT SiteWise** collects, stores, organises, and monitors industrial equipment data.

- **Collection.** Sensors and older systems, over OPC-UA, MQTT, and Modbus, through SiteWise Edge or IoT Core rules.
- **Asset modeling.** A virtual stand-in for a real machine: its place in the hierarchy, its measurements, and values computed from those measurements.
- **Edge processing.** Local pipelines and local screens keep going if the cloud link drops.
- **Pictures.** SiteWise Monitor, or a tool such as Grafana, for a dashboard without writing a front end.

**AWS IoT TwinMaker** builds an operational digital twin of a factory, a building, or a machine. It lays live data, video, and business data onto a 3D scene. The important design point: it does **not** have to copy that data out of the system that already stores it.

| TwinMaker piece | Job |
|---|---|
| Workspace | The container for the twin’s models, connections, and entities |
| Model Builder | Entities and relationships, which become a graph of the twin |
| Data connectors | Built in for SiteWise and Kinesis Video Streams. Others, such as Timestream and Snowflake, can be connected too |
| Scene Composer | Imports GLB, CAD, BIM, and point clouds |
| Views | Grafana, or a web app through the IoT App Kit |

**Example.** SiteWise knows that pump P3 sits under line 2 and that its pressure is 6 bar. TwinMaker places that pump on the CAD model of the hall and colours it when the pressure is wrong. The pressure number stays in SiteWise. TwinMaker points at it. CloudFront, in the sample architecture, is the extra piece that delivers content to browsers. It is not the twin and it is not the sensor path.

The sample design lines the services up like this: Greengrass on the site, IoT Core for the connection, SiteWise for the industrial data, TwinMaker for the 3D twin, Lambda for event-driven code, CloudFront for content delivery.

## 11. Where each job sits in a smart factory

Temperature and vibration sensors run continuously. The case study asks which work stays on the edge laptop and which work goes to AWS, using four tests.

| Test | What it asks | Where the work goes |
|---|---|---|
| Latency | Will a round trip be too slow? | Edge. Stopping the machine is local |
| Bandwidth | Must every raw sample cross the network? | Edge filters and aggregates. The cloud receives the useful result |
| Reliability | What if the link is down? | Edge keeps the safety loop. It syncs later |
| Scale | Is this a year of data from many plants? | Cloud. Storage, cross-site analytics, training, central monitoring |

Greengrass can run **inference** locally after a model exists. **Training** on a long history from many sites is a cloud job, because that is where the history and the scale are.

**Example.** Vibration crosses the limit. The edge PC stops the press (latency and reliability). It does not upload 1,000 raw samples a second (bandwidth). Once a day it uploads the summary and the fault events. A data scientist trains next quarter’s model in the cloud on every plant’s year of summaries, then sends the finished model back to Greengrass for local inference.

---

# Chapter 2 — Microsoft Azure

## 12. What Azure is, and the matching AWS service

Microsoft Azure is Microsoft’s cloud platform. It covers the same ground as AWS in this unit: compute, storage, networking, databases, AI and machine learning, analytics, IoT, monitoring, security, and edge computing.

The exam question is almost always “which Azure service does the job of this AWS service?” Learn the row, not the logo.

| Job | Azure | AWS |
|---|---|---|
| Virtual machine | Azure Virtual Machines | Amazon EC2 |
| Serverless, event-driven code | Azure Functions | AWS Lambda |
| Object / file storage | Azure Blob Storage | Amazon S3 |
| Connect and manage devices | Azure IoT Hub | AWS IoT Core |
| Run workloads on the device | Azure IoT Edge | AWS IoT Greengrass |
| Analyse a live stream | Azure Stream Analytics | Kinesis Data Analytics / Managed Flink |
| Ingest a large event or telemetry stream | Azure Event Hubs | Kinesis Data Streams |
| Metrics, logs, alerts | Azure Monitor | Amazon CloudWatch |
| Build, train, and deploy models | Azure Machine Learning | Amazon SageMaker |

The easy swap, and the one that loses the mark: **Event Hubs takes the stream in. Stream Analytics processes it.** Ingest is not analysis. IoT Hub is not IoT Edge.

**Example.** A new machine must be registered and must send telemetry. That is IoT Hub, matching IoT Core. The program that watches vibration on the factory PC is IoT Edge, matching Greengrass. The millions of events per minute enter through Event Hubs. The “count faults this minute” query is Stream Analytics. The CSV archive of last year is Blob Storage, not Event Hubs.

## 13. IoT Hub and IoT Edge

**Azure IoT Hub** is the managed cloud point between devices and Azure. It provides device connectivity, device identity, device management, telemetry, **cloud-to-device** messages, and **device-to-cloud** messages. Both directions are Hub’s job. Hub does not execute the local analytics module.

**Azure IoT Edge** takes a cloud workload and runs it on the edge device. The **IoT Edge runtime** manages the workloads on that device.

They are a pair, not substitutes. Hub remains the place that knows the devices. Edge is the place that runs the code beside the machine.

**Example.** The plant adds 40 pumps. Each pump’s identity is created in IoT Hub, and Hub can send a configuration down to the pump (cloud to device) as well as receive its telemetry (device to cloud). The anomaly program is deployed as an IoT Edge workload onto the industrial PC. If someone says “we installed IoT Edge, so we can delete IoT Hub,” they have removed the cloud connection and the device directory.

## 14. Functions, Blob, streams, and Monitor

**Azure Functions** is serverless. Code runs because an event happened. You do not provision the server. Same idea as Lambda.

**Azure Blob Storage** holds large unstructured data. The examples in class are sensor logs, CSV files, images, machine records, and historical IoT data. It is a store, not a stream processor.

**Azure Stream Analytics** fits because IoT data is produced continuously. Processing it as a stream is the natural shape. Same idea as a continuous Flink or Kinesis analytics job.

**Azure Event Hubs** is the large front door for events and telemetry. Same idea as Kinesis Data Streams. Remember the split from section 12: Hubs ingests, Stream Analytics processes.

**Azure Monitor** watches resource health, application performance, logs, metrics, and alerts. It matters more in an edge-cloud system, not less, because the devices are many and they are spread out. You cannot walk the factory and look at every PC.

**Example.** A file of the day’s CSV lands in Blob Storage. A Function starts because that file arrived, and it checks the file. The live vibration feed is a different path: Event Hubs receives it, Stream Analytics computes the one-minute maximum, and Monitor raises an alert if the Function or the hub starts failing. Machine-learning **training** on the year’s CSV is Azure Machine Learning, matching SageMaker. The fast local guess can still run on IoT Edge.

## 15. The Azure smart-factory split

The slide gives the two lists explicitly. Use them.

**On the edge**

- Local processing
- Filtering
- Aggregation
- Anomaly detection
- Local AI inference
- Immediate response

**In the cloud**

- Long-term storage
- Historical analytics
- Machine-learning training
- Centralised monitoring
- Cross-site analysis
- Device management

The case-study sentence is the whole design:

**IoT Hub connects and manages. IoT Edge processes locally. The Azure cloud stores, analyses, and learns.**

Justify with the same four tests as AWS.

| If the sentence is… | Put it… | Because… |
|---|---|---|
| Stop the machine the moment the limit is crossed | Edge | Latency, and the link may be down |
| Drop useless samples before they are transmitted | Edge | Bandwidth |
| Keep a safety decision alive during an outage | Edge | Reliability |
| Train on a year of data from every plant, and watch all of the sites from one place | Cloud | Scale, history, and one management point |

**Example.** Line 2’s PC filters vibration, detects the anomaly, and stops the motor. That is IoT Edge. The motor’s identity and the command channel live in IoT Hub. Overnight, Blob Storage holds the summaries, Azure Machine Learning trains on all four factories, and Azure Monitor shows which edge PCs are unhealthy. The trained model can be sent back for local inference. Training and inference are not the same box.

---

# Chapter 3 — Google App Engine

## 16. App Engine is a platform, not a machine you patch

Google App Engine is **Platform as a Service** on Google Cloud. You write the application. Google manages a large part of the infrastructure underneath it. Scaling is the platform’s job. You do not create servers by hand when traffic grows.

That is the contrast with a virtual machine. Compute Engine, EC2, and Azure Virtual Machines are machines you choose and operate. App Engine is the layer above that, for the application itself.

App Engine is also not the same row as Lambda. Lambda, Azure Functions, and Cloud Functions are short pieces of code on an event. App Engine hosts the application and scales it. The three-cloud table in section 20 keeps those rows apart.

**Example.** The university will not patch Linux and will not guess how many servers exam week needs. They deploy the learning site to App Engine. A quiet Tuesday and the morning results are published are the same application. The platform changes the number of running copies.

## 17. Application, services, versions, instances

An App Engine application is organised from the top down:

**Application → Services → Versions → Instances**

| Level | What it is | Example |
|---|---|---|
| Application | The top-level container, created in a Google Cloud project. It holds the services, versions, and instances | The university learning site |
| Service | One logical part, a microservice, with its own job | User service for login. Product service for the catalogue. Assignment service for submissions |
| Version | A release of that service. Used for testing, deployment, rollback, staging, and traffic splitting | v1 is production. v2 is under test. v3 is an experiment |
| Instance | A running copy of a version. More traffic means more instances. That growth is automatic scaling | Exam morning starts more copies of v1 |

If v2 misbehaves, traffic is sent back to v1. You do not delete the application to abandon a bad release.

**Traffic splitting** sends a fraction of users to the new version while everyone else stays on the old one.

**Example.** Assignment submission is its own service. The new edition is v2 of that service, not a new Google Cloud project. Ten percent of students try v2. If uploads fail, one hundred percent return to v1. The login service is untouched throughout. The extra students at 9 a.m. are extra **instances** of whichever version is live. They are not extra services.

## 18. Standard and Flexible

App Engine has two environments. Both can scale automatically. They are not “the one that scales” and “the one that does not.”

| | Standard | Flexible |
|---|---|---|
| Idea | Fully managed, sandboxed | Managed, but running on Compute Engine virtual machines |
| Startup | Very fast | Slower |
| Scaling | Very rapid, and suitable apps can scale to zero | Automatic |
| Runtime | The supported languages: Python, Java, Go, Node.js, PHP, Ruby | Custom runtimes, including Docker |
| How much you control | More restricted: CPU and memory come from predefined choices | More: CPU, memory, runtime, libraries, networking |
| Developer’s attention | Mainly the application code | The code, plus some environment configuration |
| Best for | Web apps and APIs that must scale quickly with little operations work | An application that needs a special library or a runtime the sandbox will not allow |

**Scale to zero** is stated for suitable applications on Standard. It is not Flexible’s headline. Flexible’s headline is control.

**Example.** The learning site is ordinary Python pages and APIs. Standard is the right first choice: fast start, rapid scale, and the team stays on the code. One video-processing module needs a native library the sandbox cannot host. That module is the reason to use Flexible, not a reason to put the whole site there.

## 19. The other Google Cloud services beside it

App Engine does not do every job. The application calls its neighbours.

| Need | Service |
|---|---|
| Files, videos, downloads | Cloud Storage |
| Structured records | Cloud SQL or Firestore |
| Events between parts of the system | Pub/Sub |
| “Is the app healthy?” | Cloud Monitoring and Cloud Logging |
| A warehouse for large analysis | BigQuery |
| A small extra function on an event | Cloud Functions |

**Example.** Students stream lecture videos from Cloud Storage. Marks live in Cloud SQL or Firestore. When a submission is accepted, Pub/Sub can carry that event to another part of the system. Cloud Monitoring shows the error rate on exam morning. BigQuery is where a later report asks “which courses had the most late submissions this year?” Cloud Functions might resize a thumbnail. None of those is a reason to abandon App Engine as the place the site itself runs.

Advantages named in class, in one list: less infrastructure to manage, automatic scaling, versions and traffic control, services as microservices, integration with the rest of Google Cloud, monitoring and logging, and several languages.

## 20. The same job on three clouds

This table is the join of all three chapters. If you can say the job, you can name the column.

| Job | Google Cloud | AWS | Azure |
|---|---|---|---|
| Application platform (PaaS) | App Engine | Elastic Beanstalk | App Service |
| Virtual machine | Compute Engine | EC2 | Virtual Machines |
| Serverless function | Cloud Functions | Lambda | Functions |
| Container application platform | Cloud Run | ECS / Fargate | Container Apps |
| Object storage | Cloud Storage | S3 | Blob Storage |
| Data warehouse | BigQuery | Redshift | Synapse Analytics |
| Cloud database | Cloud SQL / Firestore | RDS / DynamoDB | Azure SQL / Cosmos DB |
| IoT connectivity | IoT ecosystem and partner solutions | IoT Core | IoT Hub |
| Edge runtime | Distributed Cloud / edge solutions | IoT Greengrass | IoT Edge |
| Streaming and events | Pub/Sub / Dataflow | Kinesis | Event Hubs / Stream Analytics |
| Monitoring | Cloud Monitoring | CloudWatch | Monitor |
| Machine learning platform | Vertex AI | SageMaker | Machine Learning |

Three swaps that cost the mark:

- App Engine is **not** Lambda. The function row is Cloud Functions, Lambda, Azure Functions.
- BigQuery is **not** Cloud Storage. One is a warehouse. The other is files.
- Cloud Run is **not** App Engine. Cloud Run is the container row.

**Example.** “Store the lecture video” is Cloud Storage, S3, or Blob. “Host the website and let the platform scale it” is App Engine, Elastic Beanstalk, or App Service. “Run this 200-millisecond resize when a file arrives” is Cloud Functions, Lambda, or Azure Functions. Three sentences, three rows.

## 21. The university case

The site has about 2,000 requests an hour on a normal day and about 20,000 in exam week. Staff will not manage virtual machines, operating systems, or capacity. They also want a safe way to try a new release.

Walk the questions in the notes.

1. **Why App Engine.** It is PaaS. They write the site. The platform scales it and manages the infrastructure they refused to manage.
2. **The jump to 20,000.** App Engine adds instances of the live version. Staff do not order servers that week.
3. **Services, versions, instances.** The assignment module is a service. The new edition is a version of that service. The running copies are instances.
4. **Trying the new edition.** Deploy v2, send a fraction of traffic to it, and send traffic back to v1 if it fails.
5. **Standard or Flexible.** Standard, because this is a web application that must scale quickly with little operations work. Flexible only if a module needs a custom runtime, a special library, or Docker that the sandbox will not allow.
6. **A picture of the system.** Users reach the App Engine application. Services and versions run on instances. Cloud Storage holds videos and files. Cloud SQL or Firestore holds records. Cloud Monitoring and Cloud Logging watch the app.
7. **A tenfold spike, compared with managing machines yourself.** Instances follow demand, versions stay under traffic control, and nobody is patching servers or guessing capacity the night before results.

**Example.** Results morning is ten times a normal hour. Standard App Engine starts more instances of v1. Videos still come from Cloud Storage, not from the instance disk. A new results page is v2 of that service, shown first to a small share of students. The instance disk is not the archive. If the link between “I must patch Linux” and “I want App Engine” is still fuzzy, re-read section 16: the platform owns that work.

---

## One page before the exam

| Sentence you hear | What it is |
|---|---|
| A Linux machine I can log into, from a template | EC2, Azure Virtual Machines, or Compute Engine. The template on AWS is an AMI |
| Code runs for an event and then exits. Idle costs nothing | Lambda or Azure Functions. On Google, Cloud Functions, not App Engine |
| The website scales, and I will not create the servers | App Engine. Versions and traffic splitting are how a new release is tried |
| A file, any size, from anywhere | S3, Blob Storage, or Cloud Storage. On S3, a read after a write sees the write |
| The device is offline, but I can still set its desired state | IoT Core Device Shadow |
| Stop the press without a round trip, and keep going if the link dies | Greengrass or IoT Edge |
| Prove the device, with a certificate | IoT Core, X.509. Not the EC2 firewall, and not an IAM user password |
| A person signs in. A service gets a temporary right | IAM user, then IAM role. Default is deny |
| Industrial readings over OPC-UA, MQTT, or Modbus | SiteWise |
| The same readings, drawn on the CAD model, without copying them out | TwinMaker |
| A huge live feed, then a continuous query, then a file in the lake | Kinesis Data Streams, then Managed Flink, then Firehose into S3 |
| CPU crossed a line, so add instances | A CloudWatch alarm on one metric, or the same idea in Azure Monitor |
| Hub or Edge? | Hub connects and manages. Edge processes locally. The cloud stores, analyses, and learns |
| Service, version, or instance? | Part of the app, a release of that part, a running copy |
| Standard or Flexible? | Ordinary fast web app, or a custom runtime and Docker |
