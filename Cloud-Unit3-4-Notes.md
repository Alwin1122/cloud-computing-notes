# Cloud Computing — Unit 3 and Unit 4 Essential Notes

These are the two chapters inside the unzipped slide folders.

- **Unit 3 — Edge computing:** why it exists, the four layers, virtual machines and containers, SDN, CDN, mobile data centres, Docker and Kubernetes, protocols, and the difficulties.
- **Unit 4 — From parallel processing to industrial IoT:** parallel work, MapReduce, edge analytics, the sensor–gateway–server architecture, and IIoT.

Every topic is explained as: what it is, why it is used, and one example. The one-mark questions are in `Cloud-Unit3-4-1Mark.md`. Read this file first, then sit the questions.

---

## Table of Contents

**Unit 3**

1. [Why the cloud alone is not enough](#1-why-the-cloud-alone-is-not-enough)
2. [What edge computing does](#2-what-edge-computing-does)
3. [Edge and cloud together](#3-edge-and-cloud-together)
4. [The four layers](#4-the-four-layers)
5. [Reading a scenario into layers](#5-reading-a-scenario-into-layers)
6. [Five techniques that make the edge practical](#6-five-techniques-that-make-the-edge-practical)
7. [Virtual machines and containers](#7-virtual-machines-and-containers)
8. [Software-defined networking](#8-software-defined-networking)
9. [Content delivery and a data centre on a truck](#9-content-delivery-and-a-data-centre-on-a-truck)
10. [Docker and Kubernetes](#10-docker-and-kubernetes)
11. [Edge, fog, and cloud on one comparison](#11-edge-fog-and-cloud-on-one-comparison)
12. [How messages travel](#12-how-messages-travel)
13. [What makes edge computing hard](#13-what-makes-edge-computing-hard)

**Unit 4**

14. [Parallel processing](#14-parallel-processing)
15. [MapReduce](#15-mapreduce)
16. [Edge analytics](#16-edge-analytics)
17. [Sensors, gateways, and servers](#17-sensors-gateways-and-servers)
18. [Looking after the devices](#18-looking-after-the-devices)
19. [Industrial IoT](#19-industrial-iot)
20. [Protocols, the PLC, and maintenance](#20-protocols-the-plc-and-maintenance)

---

# UNIT 3

## 1. Why the cloud alone is not enough

In ordinary cloud computing, the data is processed in a **remote data centre**. That is the right place for a large archive. It is the wrong place when the answer is needed immediately, or when the raw data is enormous.

Two pictures from the slides make the point.

**Example — the car.** A self-driving car asks a distant server whether to brake. The delay can be long enough for an accident. The decision has to be made in the car.

**Example — the cameras.** A smart signal sends every frame to the cloud. Each camera produces about 100 MB a minute, and there are 500 cameras. The result is a huge transfer, a slow response, and a high network bill.

Those stories produce the four problems that open the chapter:

- high latency
- network congestion
- high bandwidth use
- dependence on the internet

Edge computing is the response: do the urgent work near the device, and send the cloud only what is worth keeping.

## 2. What edge computing does

Edge computing is a distributed way of working in which **processing and storage happen close to the source** — a user, a sensor, or an IoT device — instead of sending everything to one central cloud.

The move is simple: bring the computation to the device, rather than bringing every reading to the data centre.

### What you gain

| Role | What it means | Example from class |
|---|---|---|
| Less latency | The answer is computed near the user | A car detects an obstacle locally |
| Less bandwidth | Only the useful result travels | A camera sends “intrusion”, not the whole video |
| Real-time applications | An immediate decision is possible | Cars, factory machines, patient monitors |
| Reliability | Work continues if the cloud link drops | A factory keeps watching machines during an outage |
| Privacy | Sensitive data can stay on site | Face recognition runs inside the hospital |
| A lighter cloud | The cloud receives a summary | Less storage, less compute, less traffic |

Edge computing also supports IoT applications and real-time analytics. The limit is physical: an edge box has **limited computing power and limited storage**. It cannot hold ten years of video or train a huge model.

### Where it shows up

| Place | What the edge does there |
|---|---|
| Smart city | Traffic-signal control |
| Healthcare | Patient monitoring |
| Autonomous vehicle | Obstacle detection |
| Smart agriculture | Irrigation control |
| Smart factory | Machine monitoring |
| Video surveillance | Local object detection |
| Retail | Smart checkout |

**Example.** A hospital wearable reads heart rate, oxygen, and blood pressure. The emergency alert is an edge job, because the doctor needs it now. The ten-year record is a cloud job. In that one scenario the edge is doing three things at once: acting in real time, filtering so only the summary leaves the ward, and keeping the alarm alive if the internet fails. The practical difficulties are the wearable’s battery, the risk that a small device is lost or attacked, and the cost of many devices.

## 3. Edge and cloud together

Edge computing **does not replace** the cloud. They are stacked.

```text
Sensors / users
        │
        ▼
Edge device  — local processing
        │
        ▼
Cloud        — storage, analytics, backup
```

A factory with 500 sensors, each producing 1 GB a day, should not ship all of that raw data. Most of it should be handled by an edge server. The cloud still receives the part that must be stored or studied later.

From the smart-city answer in class:

- **Do it locally:** traffic-signal control, emergency alerts, accident detection.
- **Still send it to the cloud:** historical data, reports, analytics, long-term storage.

| | Cloud | Edge |
|---|---|---|
| Where the work runs | Remote data centre | Near the data source |
| Latency | Higher | Lower |
| Bandwidth use | Higher | Lower |
| Dependence on the internet | High | Lower |
| Response | Slower | Faster |
| Best for | Storage and analytics | Real-time processing |
| Example | Google Drive | An autonomous vehicle |

**Example.** Google Drive is a cloud example because the point is to keep files and open them later. The car is an edge example because the point is to brake now.

## 4. The four layers

Data climbs from the device toward the cloud. Control instructions may come back down.

| Layer | Also called | Main job | Typical data | Delay | Power and storage |
|---|---|---|---|---|---|
| 1. Device | Edge devices | Generate data, sense, do a little processing, send it upward | Raw sensor data | Very low | Very limited CPU, memory, often a battery |
| 2. Edge | Edge server, edge gateway, MEC server | Filter, aggregate, detect events, decide now | Filtered data | Low | Moderate |
| 3. Regional | Cloudlet, fog node, regional data centre | Combine several edge servers, store briefly, balance load, analyse a region | Aggregated data | Medium | High |
| 4. Cloud | AWS, Azure, Google Cloud | Store for the long term, train models, analyse at large scale, back up, recover from disaster, manage globally | Historical data | High | Very high |

The class calls layer 2 **the heart of edge computing**, because this is where a camera’s thousand images become one event: “person detected”. Only that event continues upward.

**MEC** means Multi-access Edge Computing. On the slide it is one of the computers that can sit in layer 2, close to the devices, together with an edge gateway, an edge server, or a router that can compute.

Layer 3 has three names for one idea. **Cloudlet, fog node, and regional data centre** are the intermediate tier between the local edge and the central cloud. All the hospitals in one city can send summaries to one regional medical cloudlet. One gateway cannot see that whole city.

**Example — the power grid.**

| What you see in the story | Layer |
|---|---|
| Home meters measuring consumption every second | Device |
| The substation server that sees a bad line and disconnects it immediately | Edge |
| The regional centre that collects many substations and reroutes power at peak time | Fog / cloudlet |
| The national platform that stores years of use, forecasts demand, and prints the bill | Cloud |

Fault detection stays at the substation because it must happen in milliseconds. A trip to the national cloud would be too slow. The regional centre is still necessary: a substation can save its own line, but only the region can balance many substations. The cloud is for the long record, the forecast, and the bill. A cloud-only grid would detect faults late, burn bandwidth, depend on the internet, and overload the data centre.

## 5. Reading a scenario into layers

The exam gives a story and asks you to place each sentence. Use the job, not the word “server”.

**Cameras in a city.** The camera notices motion (device). A nearby server decides the activity is suspicious and tells the police (edge). A regional server watches congestion across the city (cloudlet). The centre stores the important events and trains the next model (cloud).

**Hospital, as labelled on the slide.**

```text
Wearable device
      ↓
Edge: detect the abnormal heartbeat
      ↓
Hospital fog: alert the doctor
      ↓
Cloud: store the patient history
```

The fuller hospital notes add what the fog and the cloud are for. The edge server detects the bad beat, raises the alarm, and notifies the doctor. The fog layer combines departments, allocates ICU beds, and manages emergency services. The cloud stores the electronic health record, trains models, writes the monthly report, and keeps the backup.

**Traffic.**

```text
Camera
  → edge server detects the vehicle
  → cloudlet optimises city traffic
  → cloud stores the traffic history
```

**Car.**

```text
Vehicle sensors
  → the car’s own computer brakes immediately
  → a roadside fog server coordinates traffic
  → the cloud sends a later software update
```

The brake is not a cloud job. The software update is not a brake job.

A hierarchy is worth building because it cuts delay and bandwidth, scales by adding local sites, keeps working through an outage, decides locally, protects some data, and lightens the cloud. The price is the number of devices to manage, weak hardware at the bottom, deployment cost, harder security, the need to synchronise edge and cloud, and a mixture of different machines.

## 6. Five techniques that make the edge practical

A city with 10,000 cameras, traffic sensors, parking systems, and vehicles cannot be processed instantly by one data centre. The three pressures are the volume of data, network delay, and limited bandwidth.

Once the computers are spread out, they must be packaged, connected, and sometimes carried to the site. The five techniques are:

| Technique | The job | Example |
|---|---|---|
| Virtual machine | Run several isolated operating systems on one edge server | A hospital server with separate machines for monitoring, imaging, and the database |
| Container | Deploy a light application without a second operating system | Docker on a Raspberry Pi |
| SDN | Control the network from one programmable place | A smart-city network |
| CDN | Keep popular content near the user | Netflix, YouTube |
| Mobile data centre | Bring computers to a temporary or cut-off place | Flood relief |

**Example — one city system using all five.** Containers run the accident-detection model on nearby servers. Virtual machines hold the police database and other applications that need strong isolation. SDN steers traffic toward an edge server that is not overloaded. A CDN serves live traffic updates to phones. During a festival or a disaster, a mobile data centre arrives with extra computers.

The manufacturing version of the same question: lightweight analytics deployed quickly are **containers**; steering data to the nearest node is **SDN**; training videos delivered to many sites are a **CDN**; a portable server rolled out to a remote plant during a shutdown is a **mobile data centre**.

## 7. Virtual machines and containers

An edge server may host traffic monitoring, camera analysis, IoT monitoring, and an AI application at the same time. Installing all of them straight onto one operating system makes them hard to separate. Virtual machines and containers are two ways to package them.

A **virtual machine** is a software computer on shared physical hardware. It has a virtual CPU, virtual memory, virtual storage, a **guest operating system**, and the applications. A hypervisor sits on the physical server and runs the virtual machines.

Why use one at the edge:

- several applications on one server
- isolation, so one application’s failure does not have to sink the others
- live migration
- fuller use of the hardware

The cost is the guest operating system. Each virtual machine carries an operating system, libraries, and applications, so it uses more memory and starts more slowly. Snapshots make backup easier, and the isolation is strong.

**Example.** One hospital edge server runs three virtual machines: patient monitoring, medical imaging, and the hospital database. They can use different lives even if the hardware is the same box. If the imaging machine is snapshotted, that copy is a backup of that machine, not of the other two.

Now the question on the slide: if both applications need Ubuntu, do you need two full operating systems? **No.** They can share the host operating system. That shared form is a **container**.

A container packages the application and everything it needs — libraries, runtime, configuration — and **shares the host kernel**. It does not contain a complete guest operating system. A container engine on the host runs many containers.

Containers suit the edge because the machine is small. They are lightweight, fast to start, easy to copy, easy to deploy, and sparing of memory.

| | Virtual machine | Container |
|---|---|---|
| Operating system | Its own guest operating system | Shares the host operating system |
| Startup | Slow | Fast |
| Memory | High | Low |
| Isolation | Strong | Moderate |
| Best use | Enterprise applications that need a full private system | Edge applications and microservices |

**Example.** The accident model should start quickly on a small roadside computer, so it is a container. The police database should be strongly isolated and may need its own operating system, so it is a virtual machine. “Stronger isolation” is not automatically “better at the edge”. On a small machine, the lighter option is usually the right one.

## 8. Software-defined networking

An edge estate may contain hundreds of servers, thousands of devices, several networks, moving users, and different kinds of traffic. Configuring each switch by hand does not keep up.

**Software-defined networking (SDN)** controls that network from software. The central idea is a split:

- **Control plane** — decides where traffic should go.
- **Data plane** — forwards the packets.

In a traditional network, every switch and router contains both planes. In SDN, the decision sits in a **controller**. The switches forward.

| | Traditional | SDN |
|---|---|---|
| Where the decision lives | Inside each device, together with forwarding | In a central controller |
| How you configure it | Device by device, often with a slow, error-prone command line | Through APIs, centrally |
| After a failure | Each device recovers as it can, which can be slow | The controller can see the failure and reroute |
| Different vendors | They may not work together | Vendor-neutral protocols are meant to let them |
| A new behaviour | Often new hardware | Software |

The data plane works mainly at **OSI layers 2 and 3**. The control plane works at **layer 3 and above**, using topology, policy, and routing protocols. The controller programs the forwarding devices, and it can reprogram them as the traffic changes.

The architecture has three layers, top to bottom:

1. **Application layer** — network services for users. These applications talk to the controller.
2. **Control layer** — the controller. It programs the devices.
3. **Infrastructure layer** — the data plane: physical and virtual switches, routers, and firewalls.

What SDN is used for in the notes: traffic that changes in real time, large data-centre networks, one view of the whole network, a policy for one application, and **network slicing**.

Network slicing means several logical networks on one physical network, each with its own policy.

**Example — the campus.** Students, faculty, and administration share the cables, but each group has its own logical network, so their traffic stays separate. During an exam, the exam servers get priority over student downloads. That second sentence is fine-grained control, not slicing. Both are SDN jobs. In the smart-city example, the controller redirects traffic to an edge server that is not already overloaded. That is dynamic routing and load balancing.

Other reasons the slides give for SDN: an online shop whose traffic changes constantly, and an insurer whose HR, finance, and customer applications sit on different clouds.

Advantages: one place to manage the network, live reconfiguration, lower day-to-day operating cost because less is done by hand, a central security policy, and automated provisioning.

Disadvantages, and these are exam favourites:

- joining SDN to an old network takes planning
- the staff need new skills
- the controller is a **single point of failure** — if it dies, the network can go down — so it needs a high-availability design
- the starting cost of hardware, software, and training is high
- there is no single universal SDN standard, so vendors may still fail to interoperate

**Example.** A city deploys one controller and enjoys fast rerouting. They still keep a second controller ready. Otherwise the design that was meant to make the network easier has created one box whose death stops the city.

## 9. Content delivery and a data centre on a truck

A **content delivery network (CDN)** is a set of servers that store copies of popular content near users. The user is served by the nearby copy, not by a server on another continent.

```text
First request
User → nearby CDN server → not there → origin server
     → content comes back → CDN stores a copy

Later request
User → nearby CDN server → cached content
```

The later request is a **cache hit**.

**Example.** A film kept only in America plays slowly in Coimbatore, because every viewing crosses to India. A CDN copy in Chennai removes that trip. Netflix, YouTube, Prime Video, software downloads, and online games are the applications named in class. The gains are faster delivery, less congestion, better availability, and easier growth.

A **mobile data centre** is a portable set of servers, storage, network equipment, and power. It is used where a permanent data centre cannot be reached: a disaster, a military operation, a remote village, a large public event. It can be deployed quickly, process data locally, cut delay, and keep working in an emergency. The slides also list healthcare camps, smart agriculture, and sports events.

**Example.** A flood has broken the path to the cloud. A truck with servers reaches the area within hours. Rescue teams process drone pictures beside the site. They have not replaced the cloud forever. They have brought a small one to the only place the work can be done.

## 10. Docker and Kubernetes

Resource management means **allocating, scheduling, and watching** the limited CPU, memory, storage, and network of many edge nodes. Without it, some containers eat the CPU, some crash, some must move, and a sudden crowd of users has nowhere to go.

A **container** is a lightweight, isolated environment: the application, its libraries, and its dependencies, on the host operating system, started by a container runtime.

**Docker** is the platform that builds and runs those containers. With it you create an image, build a container, run it, stop it, remove it, and share the image.

| Word | Meaning |
|---|---|
| Image | The template. A blueprint |
| Container | A running instance of that image |
| Dockerfile | The instructions for building the image |
| Registry (Docker Hub) | The store of images |
| Engine | The runtime that builds and runs containers |

The order is: **Dockerfile → image → container → application**.

Docker is enough for one machine. It is not enough for a hundred containers across several nodes. A person cannot restart container 12, notice that node 2 is overloaded, and start twenty new copies by hand when traffic jumps.

**Container orchestration** does that life cycle automatically:

- deploy containers across a group of servers
- add copies when traffic rises and remove them when it falls
- spread requests
- restart or replace a container that dies
- let containers talk to each other

**Kubernetes** (also written **K8s**) is the orchestrator. It does not replace Docker. Docker runs the container. Kubernetes manages many containers as one system: deployment, scaling, self-healing, load distribution, how much CPU and memory a workload may take, scheduling, service discovery, and recovery.

| | Docker | Kubernetes |
|---|---|---|
| Main job | Build and run containers | Orchestrate them |
| Scope | One host, one container at a time | A cluster |
| Scaling | More manual | Automatic |
| If something dies | Limited | Built in: restart or replace |
| Where work is placed | Basic | Scheduled across nodes |

A Kubernetes **cluster** has two sides.

- **Control plane** — the manager. It accepts requests, remembers the desired state, decides where work should run, watches the cluster, and reacts to failure. It does **not** normally run the application itself.
- **Worker nodes** — the machines that do run the applications. A node runs **pods**. A pod holds containers. A container holds the application.

The control-plane pieces named on the slide are the **kube-API server**, the **kube-scheduler**, the **controller manager**, and **etcd** (the cluster’s database).

**Example.** An edge server has 8 GB of RAM. Three applications ask for 3 GB, 4 GB, and 3 GB. That is 10 GB. They cannot all receive the full request. Kubernetes is the place those limits are stated and the work is placed, moved, or refused. If one container then crashes, self-healing restarts it. You do not SSH in and start it by hand.

## 11. Edge, fog, and cloud on one comparison

The hierarchy already placed fog as the regional layer. A later slide compares the three styles directly. Read it as a description of where the processing sits, not as a second, conflicting stack.

| | Edge | Fog | Cloud |
|---|---|---|---|
| Processing | On the local device, for a specific real-time action | On nearby network resources, such as a router or a roadside server. More room than the device, less than the cloud | In a data centre, for heavy processing and large analytics |
| Money | You may upgrade devices, but you save transmission and cloud storage | You pay for local network equipment, then save on cloud fees | Cheap to start, but the ongoing bill grows with use |
| The network | Can keep working when the network is poor | Better with a bad link than the cloud is, but it still needs the local network | Needs a stable internet connection |
| Security | Every device is its own target | The same, plus the nodes the data passes through | Central controls, but a breach can expose a great deal |

**Example.** A watch detects a fall on the wrist. That is edge. A roadside server watches several cameras, detects a crash, and sends the alert rather than the film. That is fog. The data centre trains next month’s detector on the stored alerts. That is cloud.

Cloud IoT platforms named in this deck are **AWS IoT Core, Azure IoT Hub, Google Cloud IoT Core, IBM Watson IoT, and Oracle IoT Cloud**. The features expected of such a platform are: add and retire devices, stream data, dashboards, alerts and predictive maintenance, firmware updates over the air, and security. The cloud is still worth connecting, because it can hold a huge number of devices, talk to business systems such as ERP and CRM, automate actions, fail over, and learn from the history.

## 12. How messages travel

An edge system contains unlike devices. A temperature sensor, a vibration sensor, a camera, and a phone do not naturally speak one language. A **protocol** is the agreement: how the data is formatted, how the parties talk, how errors are handled, and how the exchange is secured.

The stack in the diagram is:

```text
Cloud
  ↑  HTTP / HTTPS
Edge / fog node
  ↑  MQTT / HTTP / AMQP
Edge gateway
  ↑  MQTT / CoAP
Sensors
```

There is **no single best protocol**. The choice depends on message size, bandwidth, delay, power, reliability, the pattern of conversation, the number of devices, security, and what the device can manage.

### MQTT

MQTT (Message Queuing Telemetry Transport) is a light **publish/subscribe** protocol for small devices and small messages. It sits at the application layer. A publisher and a subscriber never talk directly.

- **Publisher** sends to a topic.
- **Subscriber** listens to a topic.
- **Broker** receives every publication and routes it.
- **Topic** is the address, a text path such as `factory/machine1/temperature`.

**Example.** A thousand factory sensors publish temperatures. The edge gateway subscribes, ignores the long run of 31°C and 32°C, and forwards one alert: machine 1 is at 91°C. That is the bandwidth saving. The sensor did not open a private conversation with the cloud.

### CoAP

CoAP (Constrained Application Protocol) is for devices that are short of memory, CPU, bandwidth, and power. It is **request/response**, in the same spirit as HTTP, but it commonly runs over **UDP**. HTTP commonly runs over **TCP**.

Choose CoAP when the device itself is severely constrained and the link is poor, as with a battery sensor in a forest. Choose MQTT when many small readings should be published to listeners, as with the factory sensors.

### HTTP and HTTPS

HTTP is everywhere, easy to call from a web application, and suitable for REST APIs. **HTTPS is HTTP plus TLS.** Use it when the hop from the edge to the cloud carries something sensitive.

The factory case in the notes is: sensors to the edge with **MQTT**, edge to the cloud with **HTTPS**.

### AMQP

AMQP (Advanced Message Queuing Protocol) is for reliable enterprise messaging: queues, delivery, routing, and acknowledgements.

```text
Producer → broker → exchange → queue → consumer
```

A **binding** is the rule that connects an exchange to a queue. How the exchange fans the message out:

| Exchange | What it does |
|---|---|
| Direct | Forwards only when the routing key matches exactly |
| Fanout | Sends the message to every bound queue |
| Topic | Uses wildcards, so a pattern can match many keys |
| Headers | Routes on fields in the header, not on the routing key |

### WebSocket

Ordinary HTTP waits for the client to ask. A **WebSocket** stays open, and either side may speak, with very little delay. Use it for a live dashboard, live monitoring, remote control, or a stream of notifications.

**Example.** A screen on the factory wall must show machine state continuously. WebSocket fits. A battery sensor in the forest does not. That sensor fits CoAP. A cloud REST API fits HTTPS. A bank of enterprise systems that need a queue and an acknowledgement fits AMQP.

## 13. What makes edge computing hard

| Challenge | The issue | A remedy from the mining answer |
|---|---|---|
| Resource limits | The edge node is small. The slide contrasts 64 cores and 256 GB in the cloud with 4 cores, 8 GB, and 128 GB on the device | Run only what is needed, in light containers, and place work carefully |
| Security | More places, some of them physically exposed: tampering, theft, stolen credentials, bad software | Authentication, authorization, encryption, secure boot, updates, intrusion detection |
| Privacy | Location, video, industrial data, personal data. Keeping it local helps, but the device itself must be secured | Encrypt, control access, and process sensitive data locally when you can |
| Distributed management | One cloud, 10 regional nodes, 100 edge servers, 10,000 devices | Containers and Kubernetes help. A widely scattered edge is still harder than one data centre |
| Connectivity | Low bandwidth, high delay, congestion, links that drop | Keep working locally. Store the result. Synchronise when the link returns |
| Scalability | 100 sensors become 100,000, and 10 nodes become 5,000 | Design so you can add devices, applications, and sites. That is horizontal scale |
| Heterogeneity | x86, ARM, a Raspberry Pi, a GPU server, Linux and Windows | Containers make the application easier to carry. They do not erase every hardware difference |
| Data management | 100 cameras at 10 MB/s is about 1 GB/s | Filter, aggregate, compress, drop duplicates, store briefly, analyse locally, forward events |
| Reliability | Hardware, power, software, or weather can kill a node | A backup node, failover, local redundancy, recovery |
| Workload placement | Device, edge, or cloud? | Device: fastest and most private, poorest in resources. Edge: low delay and less traffic. Cloud: heavy analytics, at the cost of delay and bandwidth |
| Cost | Servers, gateways, sensors, power, cooling, security, people, in many places | This is an operations problem, not only a software problem |
| Edge–cloud coordination | What stays, what goes, when to sync, what happens in an outage, when a workload should move | Time-critical work at the edge. Selected and aggregated data to the cloud |

**Example — the mine.** Autonomous vehicles at a remote pit generate camera, GPS, and sensor data. An on-site server does obstacle detection. Selected data goes to the cloud. The server is small, the internet comes and goes, the vehicles are different machines, the operational data is sensitive, and the fleet is growing. Those sentences are resource limits, connectivity, heterogeneity, security, and distributed management.

If the cloud disappears for 30 minutes:

- **Continue on site:** camera processing, obstacle detection, collision avoidance, local sensor analysis, immediate alerts, the driving decision. A delay here is a safety problem.
- **Wait:** uploading non-critical data, long-term storage, large-scale analysis, historical reports, a model update that is not needed for the next second.
- **When the link returns:** send the buffer.

---

# UNIT 4

## 14. Parallel processing

Parallel processing divides a large job into smaller pieces and runs those pieces **at the same time** on several processors. The aim is a shorter run.

One processor doing the whole job from start to finish is sequential. Parallel work uses several processors or nodes.

The four steps, in order:

1. **Divide** the problem.
2. **Distribute** the pieces to different processors.
3. **Execute** them at the same time.
4. **Combine** the partial results.

| | Sequential | Parallel |
|---|---|---|
| At one moment | One piece | Many pieces |
| Hardware | Usually one main processor | Several processors or nodes |
| A large job | Takes longer | Can finish sooner |
| Building it | Simpler | More complex |
| Growth | Limited | Better, by adding processors |
| Talking between parts | Little | Often required |

### Same operation, or different tasks

**Data parallelism** is the same operation on different blocks of the data.

**Example.** One million temperature readings are split into four blocks of 250,000. Each processor computes the average of its own block. The four averages are combined. Same operation, different data.

**Task parallelism** is different operations at the same time.

**Example.** One machine’s data is analysed for temperature, vibration, and faults by three processors at once. Different tasks, one moment.

| | Data parallelism | Task parallelism |
|---|---|---|
| What is split | The data set | The tasks |
| The operation | The same one, repeated | Different ones |
| Example | Average of each block | Temperature, vibration, and fault detection together |

### What you gain, and what you pay

You gain a shorter run, a way to handle a set that will not fit one machine, the ability to add nodes, the use of machines that would otherwise sit idle, and more data finished per unit of time. Parallel work is the base of many large distributed systems.

You pay for it in six ways:

1. **Communication overhead.** Processors spend time talking. That time is not useful computation.
2. **Synchronisation.** The combine step cannot start until the pieces it needs have finished. The slow piece holds the others.
3. **Load imbalance.** If one node receives 70% and the others receive 10% each, the job runs at the speed of the overloaded node. A fair split is 25% each.
4. **Data dependency.** If task B needs task A’s output, they cannot simply run side by side.
5. **Fault tolerance.** A node can die. The lost piece must be recovered or recomputed.
6. **Coordination.** Many nodes are harder to manage than one processor.

### Speedup

Do not expect 4 processors to give exactly 4 times the speed.

\[
\text{Speedup} = \frac{\text{sequential time}}{\text{parallel time}}
\]

**Example.** Sequential time is 100 seconds. Parallel time is 30 seconds. Speedup is \(100 / 30 \approx 3.33\), not 4. The missing speed is communication, synchronisation, imbalance, dependencies, data transfer, and coordination. If you invert the fraction you get 0.30, which is not the speedup.

**Example.** A billion sensor records take 10 hours on one machine. Four nodes can each take about 250 million. That is data parallelism. If node 4 is much slower, the problem is load imbalance. If node 2 dies, the problem is fault tolerance. The model that organises this kind of large batch is MapReduce.

## 15. MapReduce

MapReduce is a programming model for processing a large data set in parallel across many nodes. You write two functions. The framework distributes the work.

- **Map**
- **Reduce**

Between them, the system **shuffles and sorts**.

```text
Input
  → Map
  → intermediate key-value pairs
  → Shuffle and Sort
  → Reduce
  → final output
```

Everything moves as a **key-value pair**, written `(key, value)`.

**Example — counting machine status.** The input is Machine A normal, B fault, C normal, D normal, E fault.

Map emits one pair per machine:

```text
(Normal, 1)
(Fault, 1)
(Normal, 1)
(Normal, 1)
(Fault, 1)
```

Shuffle and sort **group by key**. The values are kept. They are not deleted:

```text
Normal → [1, 1, 1]
Fault  → [1, 1]
```

Reduce adds each list: **Normal → 3**, **Fault → 2**.

### The phases

The notes list three main phases and one optional phase.

| Phase | What happens |
|---|---|
| Map | Takes `(k, v)`. The key addresses the record. The value is the record. Emits `(k', v')`. Many maps run at once on different splits |
| Shuffle and sort | Groups the map output by key and sorts it. The reducer receives `(k, v[])`, a key and a list of values |
| Reduce | Runs the reducer on each group and writes the final result. Different keys can be reduced in parallel |
| Combine | **Optional.** It makes the shuffle quicker by reducing intermediate data. The answer is still correct if you omit it |

The flow drawn on the component slide is: **input → split → mapper → shuffle → sort → reducer → output**.

| | Mapper | Reducer |
|---|---|---|
| Reads | Input records | Grouped intermediate data |
| Writes | Key-value pairs | The final aggregate |
| When | Before the shuffle | After the shuffle and sort |
| Parallelism | Across partitions of the input | Across different keys |
| Example | `(Fault, 1)` | `Fault → 25` |

**Example — word count.** The two lines are “Cloud computing is useful” and “Cloud computing is scalable”.

Map emits `(Cloud, 1)`, `(computing, 1)`, `(is, 1)`, `(useful, 1)`, and the same for the second line with `scalable` instead of `useful`.

After grouping:

```text
Cloud → [1, 1]        → 2
computing → [1, 1]    → 2
is → [1, 1]           → 2
useful → [1]          → 1
scalable → [1]        → 1
```

Other uses named in class: log analysis, indexing web pages, ETL (extract, transform, load), recommendation systems, and data mining. Another counting picture on the slides is “how many movies are associated with each user”, which is the same shape: map to `(user, 1)`, group by user, reduce to a count.

### Why it is used, and when it is the wrong tool

Advantages: very large data, parallel processing, more nodes when the work grows, fault tolerance by running the failed piece again, a simpler job for the programmer (write Map and Reduce, not the whole distributed engine), and a good fit for **batch** work. **Data locality** helps because the computation stays near the data, so less data crosses the network.

Limits:

- Traditional MapReduce is for batch work. It is a poor fit for a millisecond response.
- The shuffle moves and groups data, which costs network time.
- Intermediate results often hit the disk.
- Algorithms that loop over the same data many times, including some machine-learning training, are inefficient.
- It is not the tool for a low-latency interactive session.

**Batch** means the data is collected and then processed as a job. A **stream** is processed as it arrives. MapReduce belongs to the batch side.

**Example.** Counting a billion stored sensor records overnight is MapReduce. Stopping a motor because vibration crossed a limit this second is not. That second decision is edge analytics.

## 16. Edge analytics

Edge analytics means analysing data **close to where it is produced**, so a useful decision does not wait for every raw reading to reach a central cloud.

```text
Cloud path:   sensors → network → cloud → analytics → decision
Edge path:    sensors → edge → local analytics → decision now
                              → summary → cloud
```

It is needed when the volume is huge, the cloud bill and the transmission bill matter, the decision has a tight deadline, the link is narrow or intermittent, the data should not all leave the site, or the site needs its own intelligence, such as anomaly detection.

| | Edge analytics | Cloud analytics |
|---|---|---|
| Location | Near the source | Central data centre |
| Latency | Very low | Usually higher |
| Processing and storage | Limited or moderate | Very high |
| Real-time decisions | Excellent | Weak when the deadline is strict |
| Long history and model training | Limited | Excellent |
| Bandwidth | Lower, because raw data stays home | Higher if raw data is shipped |
| Dependence on the link | Lower for a local decision | Higher |
| Privacy | Raw data need not travel | The archive is central |
| Best for | An immediate local decision | Large-scale and historical analysis |

**On the edge:** filtering, preprocessing, aggregation, event detection, anomaly detection, real-time analytics, local inference, immediate control.

**In the cloud:** long-term storage, historical analysis, large-scale analytics, model training, enterprise reports, cross-site analysis, central management.

### Methods

| Method | What it does | Example |
|---|---|---|
| Filtering | Drops what is not needed | Send only temperatures above 80°C |
| Aggregation | Many readings become one summary | The average temperature each minute |
| Threshold / event | A known limit fires immediately | Vibration above the line raises an alert |
| Statistics | Mean, minimum, maximum, variance | Spot an abnormal machine temperature |
| Anomaly detection | An unusual pattern, not only a fixed limit | Vibration that does not match this motor’s normal behaviour |
| Local inference | A trained model runs at the edge | A camera marks a defective product |
| Stream processing | The data is handled as it arrives | Sensor readings analysed continuously |
| Preprocessing | Clean and reshape before the cloud | Remove noise, normalise |
| Local decision | Act without the cloud | Stop the machine |
| Compression | Shrink the upload | 10,000 readings become an hourly statistic |

A threshold is a number you wrote down in advance. Anomaly detection is “this pattern is not normal”, which is the step that leads to predictive maintenance.

### Tools, and which layer they belong on

| Tool | What it is for |
|---|---|
| Python, with NumPy and Pandas | Numbers and tables |
| scikit-learn | Machine-learning inference |
| OpenCV | Images and video |
| TensorFlow Lite / LiteRT, or PyTorch | A model on an edge device |
| PySpark | Stream processing, distributed analytics, and MapReduce-style work **on an edge server that is big enough**. It is too heavy for a tiny sensor |
| Node-RED | A browser flow editor for wiring an IoT path. It is not a protocol |
| MQTT | The messenger. It is not the analytics. The edge server does the threshold check after the message arrives |

| Layer | Tools and methods |
|---|---|
| Sensor | A threshold, simple filtering |
| Edge device | Python, NumPy, OpenCV, LiteRT |
| Gateway | MQTT, Node-RED, filtering, aggregation, protocol handling |
| Edge server | Python, PySpark, inference, a local database, containers |
| Cloud | Large analytics, a warehouse, training, history |

**Example.** Two hundred machines emit temperature, vibration, and pressure every second. Shipping all of it makes the network busy and the fault late. An edge server filters, aggregates, and runs a threshold or an anomaly check. Abnormal vibration raises an alert on site. The cloud receives the summary and the fault, not every sample. If the link drops, detection continues and the buffer is sent later. Compared with a cloud-only design, the edge design wins on latency, bandwidth, local privacy, and survival of an outage. The cloud remains the better place for a huge history.

Applications named in class follow the same pattern. An ATM recognises tampering in the camera and shuts down locally, then alerts the bank. A drone looks at leaf colour on the farm. A shop camera watches stock. A car brakes itself. An ambulance analyses a critical patient on the way, because there is no time to upload first. Predictive maintenance estimates a failure before it happens, so the repair can be booked first.

## 17. Sensors, gateways, and servers

Data is not a pipe that only flows upward. At each stage it can be filtered, aggregated, analysed, and stored.

```text
Physical world
  → sensors / endpoints
  → edge devices
  → edge gateways
  → edge servers
  → cloud
```

| Piece | What it is | How heavy the work is |
|---|---|---|
| Sensor | Measures a physical quantity and turns it into data. Temperature, pressure, humidity, vibration, light, gas, motion, GPS, current | Very light |
| Endpoint | Any device at the edge that generates, receives, or exchanges data. A camera, a vehicle, a wearable, a machine. A sensor can be an endpoint. Not every endpoint is only a sensor | Varies |
| Edge device | A computer near the source: an industrial PC, a Raspberry Pi, a Jetson, a smart camera, a vehicle computer. It collects, filters, preprocesses, detects, alerts, stores briefly, and forwards a selection | Low to moderate |
| Edge gateway | The bridge. It connects, translates protocols, aggregates, filters, secures, forwards, and may analyse | Moderate |
| Edge server | A stronger computer near the site: an industrial server, a local rack, a GPU server | Moderate to high |
| Cloud | Central processing and storage | Very high |

The verb chain on the slide is the same stack: **sense → collect and process → connect and aggregate → analyse and compute → store and analyse at large scale**.

### The gateway is the translator

Devices do not share one network. The slide’s example is Bluetooth, Zigbee, Modbus, and Wi-Fi arriving at one gateway and leaving as one stream toward the edge server or the cloud.

The gateway also aggregates. One hundred sensors do not need one hundred uploads. The gateway can forward an average, a minimum, a maximum, and the important events. It can filter. It can authenticate, authorise, encrypt, control access, and filter traffic.

A **traditional IoT gateway** mostly connects. The analytics happen later in the cloud. An **edge gateway** can find the meaningful event before transmission: a fault, a maintenance alert, a quality result, a production figure, an energy saving. That is why it uses less bandwidth and answers faster. It can also sit in front of thousands of devices as the site grows.

### The edge server is the heavy local machine

A small device cannot host computer vision, many applications, a local database, and containers together. The edge server can.

It can join temperature, vibration, pressure, and power into one view of a machine, compare vibration with the normal pattern, run a trained model, look at how a signal changes over time, keep recent history, raise an alert without the cloud, and send upward only the summary, the anomaly, and the fault.

| | Edge device | Edge gateway | Edge server |
|---|---|---|---|
| Collect | Yes | Yes | Sometimes |
| Filter | Yes | Yes | Yes |
| Translate protocols | Sometimes | Yes | Sometimes |
| Aggregate | A little | Yes | Yes |
| Heavy analytics and inference | Limited | Limited or moderate | Yes |
| Storage and CPU | Low to moderate | Moderate | High |

**Example — readings 72, 73, 74, 75, and 92, with a fault line at 80°C.** The edge device can see that four readings are normal and 92 is a fault. It should not fire all five raw values upward as emergencies. It sends the 92°C event at once, and it can send a summary (machine, average, maximum, fault, time). If the application truly needs every sample for the historical record, those samples can sit locally and upload later. The point is not “never send data”. The point is “do not send five urgent raw samples when one event and a summary will do”.

**Example — mixed machines.** Machine A speaks Modbus, machine B speaks OPC UA, machine C speaks MQTT. The gateway translates them into one message format before the edge server sees them.

**Example — one hundred sensors every second.** Without the gateway, the cloud receives 100 readings a second. With it, the cloud or the edge server receives a zone average, a minimum, a maximum, and a fault count, plus any abnormal event forwarded immediately.

**Example — machine M205’s odd vibration.** The edge server, not the tiny sensor, joins temperature and vibration, runs the heavier model, and raises the local alert. The sensor does not have the CPU, memory, storage, or energy for that. The cloud still does the long-term training.

What the cloud should receive:

| Situation | Send |
|---|---|
| Normal operation | Periodic summaries: averages and statistics |
| Abnormal temperature | Machine, value, threshold, time, the event |
| A fault | The fault detail, the relevant recent history, the alert |
| Network down | Nothing yet. Store locally and synchronise later |

During a 30-minute outage the sensors keep measuring, the edge devices keep filtering and controlling, the gateway keeps translating and buffering, and the edge server keeps making safety decisions. When the link returns, the buffer is synchronised. A safety decision does not sit in that buffer waiting for the cloud.

## 18. Looking after the devices

Edge device management is how you deploy, configure, monitor, secure, update, repair, and retire devices you cannot visit one by one.

| Function | What you actually do |
|---|---|
| Registration | Record the new device’s identity, place, type, version, and what it can do |
| Configuration | Sampling rate, network, thresholds, application settings, security settings |
| Monitoring | CPU, memory, storage, network, temperature, battery, health, whether the application is up. A device at 92% CPU, 88% memory, and 95% disk is a warning |
| Updates | Push software or firmware remotely. Keep versions, roll out in stages, be able to roll back, and check that the update landed |
| Security | Authentication, certificates and keys, access control, secure communication, patches, watching for intrusion |
| Faults | Detect silence, alert, restart, recover, or replace |
| Resources | If CPU is too high, move the workload, slow the processing, restart the application, or alert |
| Life cycle | Deploy, register, configure, operate, monitor, update, maintain, retire |

**Example — three broken devices in a factory of 500.**

- **High CPU.** The management system notices, alerts, finds the workload, moves or reduces it, and keeps watching.
- **Old software.** It detects the old version, checks the new one, updates the device remotely, verifies the install, and returns the device to service. Nobody walks to all 500 boxes.
- **No answer.** Health check, retry, restart. If it stays dead, alert a technician and repair or replace it. Record the fault.

## 19. Industrial IoT

The **Industrial Internet of Things (IIoT)** is connected sensors, machines, controllers, networks, analytics, and software in industry: plants, power, oil and gas, mining, chemical works, water treatment, renewable energy, transport, smart factories.

The difference from ordinary IoT is the setting. These are industrial processes, so **reliability, safety, a real-time response, and continuous operation** matter. A failed consumer gadget is annoying. A failed industrial system can stop production, damage equipment, or hurt people.

IoT or IIoT is decided by the **purpose**, not by the brand of sensor and not by the radio.

| | IoT | IIoT |
|---|---|---|
| Devices | General connected devices | Industrial machines and systems |
| Examples | Home, wearables, a garden | Manufacturing, power, mining |
| If it fails | Often a moderate inconvenience | Safety, production, equipment |
| How it connects | General connectivity | Industrial protocols and operational technology |
| The work | Monitoring and automation | Monitoring, control, optimisation, predictive maintenance |

**Example.** A camera in the factory cafeteria that watches people is IoT. The same kind of camera on the production line, rejecting a bad product, is IIoT. A home garden that waters itself is IoT. A municipal water plant watching pressure and flow is IIoT. A car that tells the driver the tyre is soft is IoT. A wind turbine watched so that maintenance can be predicted is IIoT.

Classifications that match the answer slides:

| IoT | IIoT |
|---|---|
| Smart refrigerator, smartwatch, streetlights, washing machine, fitness band | Motor temperature in a plant, bearing vibration, refinery pressure, a camera that rejects bad products, humidity in a pharmaceutical plant |
| Phone-controlled door lock, home irrigation, tyre-pressure alert to the driver, a house CCTV alert, a house thermostat | A PLC controlling an industrial motor, a water-treatment plant, a wind turbine, production-line inspection, steam in a power plant |

Industrial sensors are read for a reason. Temperature suggests overheating, a bearing problem, or a cooling fault. Vibration suggests bearing failure, imbalance, misalignment, or wear. Pressure is read on pumps, compressors, pipelines, and hydraulic and chemical equipment. Motor current suggests overload, mechanical resistance, a motor fault, or abnormal energy use.

In ordinary IoT a sensor may talk fairly directly to a gateway or the cloud. In IIoT a sensor often talks **first to a PLC** or another industrial controller.

## 20. Protocols, the PLC, and maintenance

A **PLC (Programmable Logic Controller)** monitors inputs and controls a process.

**Example.** A temperature sensor reports to the PLC. The PLC asks whether the temperature is above 90°C. If it is, the PLC turns the cooling system on. That is control. Edge computing **analyses** the process: is this motor drifting toward a failure? The PLC and the edge are complementary. A plant does not choose one and throw the other away.

The **industrial edge gateway** stands between the equipment and the edge server. It converts protocols, collects, filters, aggregates, routes, secures, buffers, and manages the connection. The picture in class is OPC UA or Modbus from the PLC into the gateway, and MQTT from the gateway to the edge server.

**OPC UA** (Open Platform Communications Unified Architecture) is a platform-independent industrial standard.

- It runs on Windows, Linux, Android, or a small controller. It does not depend on an old Microsoft technology.
- It encrypts, signs messages, and authenticates users.
- It models data as a hierarchy of nodes, objects, and methods, not as a flat list of tags.
- It supports client-server communication and publish/subscribe.
- It joins the machines (operational technology) to IT and the cloud.

**Modbus** is a widely used industrial protocol, especially on older equipment. A **master** (a gateway or a PLC) starts every request. A **slave** (a meter, a drive, a sensor) answers only when asked. That is request/response. The master can read a temperature or a tank level, or write a command such as “turn on”. Modbus is not a publish/subscribe broker. That pattern belongs to MQTT, and OPC UA can do publish/subscribe as well as client-server.

The closing notes pair ordinary IoT with MQTT, HTTP/HTTPS, CoAP, and WebSocket, and IIoT with OPC UA and Modbus.

### From a threshold to a prediction

On the edge, IIoT work starts with the same methods as Unit 4’s analytics chapter.

1. **Filter** invalid readings, duplicates, noise, and irrelevant measurements.
2. **Aggregate** to an average, a maximum, or a minimum.
3. **Apply a threshold.** Below 80°C is normal, 80 to 90°C is a warning, above 90°C is critical. The alert is local.
4. **Detect an anomaly:** a sudden change, an odd pattern, an odd combination, a drift away from normal behaviour.

That fourth step is the door to **predictive maintenance**.

**Preventive maintenance** services the machine on a fixed calendar, for example every three months. A healthy machine may be opened unnecessarily. A failing machine may break before the scheduled day.

**Predictive maintenance** watches temperature, vibration, current, and pressure continuously, judges the condition, and raises a maintenance alert before the failure.

### Where the model is trained

```text
Historical data in the cloud
  → prepare it
  → train
  → send the trained model to the edge server
  → the edge server runs inference on live sensor data
  → if the result is bad, raise “maintenance required” immediately
  → the event returns to the cloud for history and for the next training run
```

**Example.** The cloud trains on five years of turbine vibration. The edge server on the turbine runs that model every minute. When the pattern matches an approaching bearing failure, the alert is local and immediate. The cloud hears about the event afterwards and can retrain. The PLC, meanwhile, is still the controller that can open a breaker or start a cooler. The model does not replace that ladder. It warns that the ladder’s machine is getting sick.

Security on this path is authentication of devices, gateways, applications, and users; authorization of who may read or change machine data; encryption in transit; controlled software and firmware updates; and monitoring for strange access, strange traffic, failed devices, and suspicious behaviour. Device management is the same life cycle as section 18: deploy, register, configure, operate, monitor, update, maintain, retire, with remote troubleshooting added for a plant you do not want to walk.

---

## One page before the exam

| Sentence you hear | What it is |
|---|---|
| Brake now, or the car hits something | Edge. Not the cloud |
| A summary of the day, a ten-year record, a trained model | Cloud |
| Meters, substation, regional centre, national bill | Device, edge, fog/cloudlet, cloud |
| Cloudlet, fog node, regional data centre | Three names for the layer between the edge and the cloud |
| Two Ubuntu applications, and you refuse a second operating system | A container. A virtual machine would carry the second operating system |
| One controller decides the path. Switches only forward | SDN. If that controller dies, the network can die with it |
| The first viewer fetches the film from America. The second gets it from Chennai | CDN cache miss, then cache hit |
| The internet is down at a flood | Mobile data centre |
| Image, container, Dockerfile | Template, running copy, build instructions. Kubernetes manages many of them. Docker does not get replaced |
| 3 GB + 4 GB + 3 GB on an 8 GB edge server | They do not all fit. Something must allocate |
| `factory/machine1/temperature` | An MQTT topic. The broker delivers it. The clients do not talk directly |
| A battery sensor on a bad forest link | CoAP, commonly over UDP |
| Sensors in the factory, then a secure call to a cloud API | MQTT, then HTTPS |
| A live wall display | WebSocket |
| 100 seconds becomes 30 seconds on several processors | Speedup about 3.33, not 4 |
| Same average on four blocks of the data | Data parallelism |
| Temperature and vibration analysed together | Task parallelism |
| `(Normal, 1)` grouped into `[1, 1, 1]` and added | Map, shuffle, reduce. The combiner is optional |
| Stop the motor this second | Edge analytics. Not MapReduce |
| 72, 73, 74, 75, 92, and the line is 80 | 92 is the fault event. Do not upload five raw emergencies |
| Modbus, OPC UA, and MQTT on one site | The gateway translates |
| A home garden, or a water-treatment plant | IoT, then IIoT. The purpose decides |
| The PLC turns the cooler on. The edge warns that the bearing is dying | Control, then analysis. Keep both |
| Every three months, or when the vibration pattern goes bad | Preventive maintenance, then predictive maintenance |
| Train on the history, infer beside the machine | Cloud, then edge |
