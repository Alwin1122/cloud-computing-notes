# Unit 3 and Unit 4 — 1-mark MCQ bank

Two chapters from the remaining decks in the Unit 5 pack.

- **Unit 3 — Edge computing:** why it exists, the four-layer hierarchy, virtual machines and containers, SDN, CDN, mobile data centers, Docker and Kubernetes, edge-to-cloud protocols, and the challenges.
- **Unit 4 — Parallel processing through IIoT:** parallel processing, MapReduce, edge analytics, the sensor–gateway–server architecture, and industrial IoT.

Unit 5 (AWS, Azure, and App Engine) is the separate bank in `Cloud-Unit5-1Mark.md`.

**How to sit this.** Cover the answer pages. Choose the **best** option. Then read the one-line reason. A 1-mark paper gives the mark for the right layer, the right technique, or the right protocol. If you can say the reason aloud, a reworded question still falls the same way.

There is **no negative marking** assumed. One question, one mark.

Eight ideas unlock almost every question:

1. **Closer means faster, and less data leaves the site.** The cloud keeps the history and trains the model.
2. **Four layers, bottom to top.** Device generates. Edge decides now. Fog / cloudlet coordinates a region. Cloud remembers. Data climbs. Control can come back down.
3. **A container shares the operating system. A virtual machine carries its own.** Docker runs containers. Kubernetes runs many of them across machines. Docker is not replaced by Kubernetes.
4. **The control plane chooses the path. The data plane forwards the packet.** In SDN that choice sits in one controller, so the controller must not be a single unprotected brain.
5. **MQTT publishes small readings. CoAP is for the most constrained device, over UDP. HTTPS carries the result to a cloud API. WebSocket stays open both ways. AMQP queues enterprise messages.**
6. **MapReduce is a huge batch:** split, map to key-value pairs, group by key, reduce. It is not how you stop a machine in the next millisecond.
7. **The gateway translates protocols. The edge server does the heavy local analysis. The PLC controls the machine. The edge predicts the failure.**
8. **IIoT is decided by the job, not by the sensor.** A factory, a plant, or a safety-critical machine is IIoT. A home, a watch, or a personal alert is IoT.

---

# Unit 3 — Edge computing

### A1
Edge computing, as defined in class, is

a) a rule that every reading must be stored in a remote data centre before it may be used  
b) processing and storage performed closer to the source, instead of sending all data to a central cloud  
c) a replacement that removes any need for cloud storage  
d) a protocol for downloading films

### A2
A self-driving car that waits for a distant cloud server before it brakes is a lesson in

a) strong S3 consistency  
b) delay, and the accident that delay can cause  
c) why virtual machines need a guest operating system  
d) cache hits

### A3
Five hundred traffic cameras each send every frame to the cloud, at about 100 MB a minute. The problems named in class are

a) a huge transfer, a slow response, and a high network cost  
b) too much privacy, because the pictures never leave the camera  
c) the cloud having too little disk for a single JPEG  
d) MapReduce being unable to count words

### A4
The four cloud problems that motivate edge computing are

a) high latency, network congestion, high bandwidth use, and dependence on the internet  
b) too little long-term storage, too few programming languages, and no backup  
c) containers starting too quickly  
d) sensors that cannot measure temperature

### A5
Which item is a **limitation** of edge computing, not an advantage?

a) lower latency and a faster response  
b) less bandwidth use, better privacy, and work that continues through an outage  
c) limited computing resources and limited storage  
d) support for real-time IoT analytics

### A6
A CCTV system uses the edge properly when it

a) uploads the continuous video and lets the cloud decide later  
b) sends the intrusion event, not the uninterrupted video  
c) stores ten years of video only on the camera battery  
d) trains the recognition model on the camera and never uses a server

### A7
A factory keeps monitoring its machines during an internet outage. The role on display is

a) reliability: local operation does not require the cloud link at that moment  
b) CDN cache replacement  
c) a MapReduce shuffle  
d) network slicing for students and faculty

### A8
Facial recognition runs inside the hospital, and the patient images are not sent to a public cloud. The role on display is

a) live migration of a virtual machine  
b) privacy: sensitive data can stay local  
c) a mobile data centre  
d) fanout exchange

### A9
“Reduces cloud workload” means the cloud receives

a) summarised or relevant results, so storage, compute, and network traffic all drop  
b) every raw sample, so the cloud bill stays the same  
c) only IAM policies  
d) a full guest operating system from each sensor

### A10
On the comparison in class, cloud computing is the better fit for storage and large analytics, and edge computing is the better fit for real-time processing. The examples paired with them are

a) an autonomous vehicle for the cloud, and Google Drive for the edge  
b) Google Drive for the cloud, and an autonomous vehicle for the edge  
c) both for a single MQTT topic  
d) both for a Dockerfile

### A11
The relationship taught between edge and cloud is that

a) they work together: devices, then local processing, then the cloud for storage, analytics, and backup  
b) edge computing deletes the cloud  
c) the cloud is only a CDN  
d) sensors must talk to the cloud with no device in between

### A12
In the smart-city answer, which data should **still** go to the cloud?

a) the brake decision of a car that is about to hit an obstacle  
b) historical data, reports, analytics, and long-term storage  
c) every camera frame, as the preferred design  
d) the guest operating system of each traffic light

### A13
Which applications are named as needing immediate local processing?

a) traffic-signal control, emergency alerts, and accident detection  
b) a ten-year billing archive  
c) training a model on a national history  
d) a monthly report

### A14
Wearables watch heart rate, oxygen, and blood pressure. Doctors need an alert at once, and the hospital needs years of records. The split is

a) alerts, anomaly detection, and the local alarm at the edge; long history, heavy trend analysis, and cross-hospital sharing in the cloud  
b) the emergency alarm only in the cloud; the ten-year record only on the wearable battery  
c) both jobs inside one MQTT broker  
d) both jobs inside a combiner

### A15
Three roles of edge computing in that hospital case are real-time processing, filtering, and local autonomy. A deployment difficulty the notes add is

a) the cloud having no disk  
b) battery drain, a device that can be lost or attacked, and the cost of many devices  
c) MapReduce being too interactive  
d) CDN cache hits being too fast

### A16
From the device upward, the hierarchy is

a) edge devices, then edge server or gateway, then regional edge (cloudlet / fog), then the cloud  
b) cloud, then fog, then the sensor, then the gateway  
c) mapper, shuffle, reducer, combiner  
d) application layer, control layer, infrastructure layer

### A17
In this hierarchy, the usual directions are

a) data and control both stay inside one sensor  
b) data flows upward toward the cloud; control instructions may flow downward toward the devices  
c) control flows up and data is forbidden to move  
d) only the fog layer is allowed to store anything

### A18
The device layer is where data is generated. A typical device is

a) limited in CPU and memory, often on a battery, and able to generate a very large volume of raw data  
b) the national archive of ten years of records  
c) the Kubernetes control plane  
d) a regional cloudlet that balances load across cities

### A19
The edge server or edge gateway is called the heart of edge computing because it

a) filters, aggregates, runs local analytics, detects events, and can decide in real time, close to the devices  
b) is the only place a model may be trained on a national history  
c) replaces every protocol with a guest operating system  
d) stores the etcd database

### A20
A camera captures 1,000 images. The edge server finds a person. What should be sent onward?

a) all 1,000 images, because the cloud must see every pixel before the word “person” is allowed  
b) the event “person detected”  
c) the camera’s battery status only  
d) a new virtual machine for each image

### A21
Cloudlet, fog node, and regional data centre, in this hierarchy, are

a) three names for the intermediate layer between edge nodes and the central cloud  
b) three names for the sensor itself  
c) the three MapReduce functions  
d) Docker Hub, the Dockerfile, and the image

### A22
The fog / cloudlet layer is required when

a) one gateway’s local view is not enough, and several edge servers must be coordinated, balanced, and analysed as a region  
b) a single temperature sample must be printed  
c) the only job is to issue a long-term IAM key  
d) a container must share the host kernel

### A23
The cloud layer is the right place for

a) long-term storage, model training, big-data analytics, backup, disaster recovery, and global management  
b) isolating a faulty power line within milliseconds  
c) the publish step of a single MQTT sensor  
d) packaging one Python library into an image

### A24
The kind of data each layer is described as processing is

a) device historical, edge raw, fog filtered, cloud empty  
b) device raw, edge filtered, fog aggregated, cloud historical  
c) all four layers raw video  
d) only the cloud filtered, and the edge historical

### A25
Moving from the device, to the edge, to the cloudlet, to the cloud, latency and computing power generally

a) latency rises and computing power rises  
b) latency falls and computing power falls  
c) both stay identical at every layer  
d) latency rises and computing power falls to zero

### A26
In the power-grid story, smart meters, the substation server, the regional control centre, and the national platform are

a) device, edge, fog, and cloud  
b) cloud, fog, edge, and device  
c) mapper, reducer, combiner, and shuffle  
d) CDN, SDN, VM, and container

### A27
The faulty line is disconnected by the local server, not by the national cloud, because

a) national disks are smaller than a meter  
b) the disconnection must happen in milliseconds, and a trip to the cloud adds too much delay  
c) fog nodes are forbidden to see electricity data  
d) Modbus cannot leave a building

### A28
The regional control centre is still needed even though each substation can trip its own line, because

a) it coordinates many substations and balances demand across them; one gateway sees only its own area  
b) it replaces the meters  
c) it is the MQTT topic string  
d) it builds Docker images

### A29
A grid that used only the distant cloud would suffer

a) slower fault detection, more bandwidth, a late emergency response, dependence on the internet, and a heavier cloud  
b) too much privacy and no history  
c) an inability to store a monthly bill  
d) containers that cannot start

### A30
Five thousand cameras detect motion themselves. Nearby servers flag suspicious activity and call the police. A regional server watches congestion across the city. The centre stores the important events and trains the next model. Those four steps are

a) cloud, cloudlet, edge, device  
b) device, edge, cloudlet, cloud  
c) reducer, mapper, shuffle, split  
d) infrastructure, control, application, and etcd

### A31
On the labelled hospital chain, the wearable, the detection of the abnormal beat, the alert to the doctor, and the stored history sit at

a) device, edge, fog, cloud  
b) cloud, fog, edge, device  
c) gateway, CDN, SDN, MDC  
d) map, shuffle, reduce, combine

### A32
On the traffic chain, the camera, “vehicle detected”, city-wide optimisation, and stored traffic history sit at

a) device, edge, cloudlet, cloud  
b) cloudlet, cloud, device, edge  
c) PLC, Modbus, OPC UA, MQTT  
d) image, container, pod, node

### A33
On the vehicle chain, the sensors, the immediate brake, roadside traffic coordination, and the later software update sit at

a) device, vehicle edge computer, roadside fog, cloud  
b) cloud, fog, edge, device  
c) CDN origin, cache hit, cache miss, broker  
d) control plane, data plane, application plane, etcd

### A34
A hierarchical edge design is used because it

a) cuts latency and bandwidth use, scales better, stays up locally, keeps some data private, and lightens the cloud  
b) forces every decision through one national server  
c) removes the need to manage devices  
d) guarantees that four processors give exactly four times the speed

### A35
A limit of that same hierarchy is

a) an absence of any devices  
b) many devices to manage, modest edge hardware, higher deployment cost, harder security, edge–cloud synchronisation, and mixed hardware  
c) the cloud being unable to store history  
d) MQTT having no broker

### A36
The five key techniques named for edge computing are

a) virtual machines, containers, SDN, CDN, and mobile data centres  
b) map, shuffle, reduce, combine, and split  
c) MQTT, CoAP, HTTP, AMQP, and WebSocket  
d) sensor, endpoint, gateway, server, and PLC

### A37
A virtual machine, in this chapter, is

a) a picture of a film stored near the viewer  
b) a software computer, with virtual CPU, memory, and storage, that runs its own guest operating system on shared hardware  
c) a topic string such as `factory/machine1/temperature`  
d) the Kubernetes database

### A38
Virtual machines are placed on an edge server so that

a) several applications can run on one machine, isolated from each other, with a path to live migration and fuller use of the hardware  
b) every application is forced to share one kernel and nothing else  
c) the data plane can forward packets  
d) a cache hit can skip the origin server

### A39
The cost of that isolation is that each virtual machine

a) contains no operating system, so it cannot start  
b) carries an operating system, libraries, and applications, so it uses more memory and starts more slowly  
c) is unable to take a snapshot  
d) can run only on a phone battery

### A40
Two applications both need Ubuntu. The slides say a second full operating system is unnecessary because

a) they can share the host operating system, which is what a container does  
b) SDN will merge the two disks  
c) the fog layer deletes one of them  
d) CoAP does not use an operating system

### A41
A container packages the application and its libraries, and it

a) shares the host kernel and does not include a full guest operating system  
b) always includes a private guest operating system  
c) is a regional data centre  
d) is a publish/subscribe broker

### A42
Containers are preferred on a small edge server because they are

a) heavier than virtual machines and slower to start  
b) lightweight, quick to start, easy to copy, and sparing of memory  
c) unable to run more than one application in the whole city  
d) a replacement for HTTPS

### A43
Which comparison matches the table?

a) a virtual machine has its own operating system, starts slowly, uses more memory, and isolates strongly; a container shares the host operating system, starts quickly, uses less memory, and isolates more moderately  
b) the container has the stronger isolation and the slower start  
c) both include a full guest operating system  
d) virtual machines are only for microservices, and containers cannot run on the edge

### A44
SDN is introduced in an edge network because

a) hundreds of servers and thousands of devices are painful to configure one by one; SDN offers central, programmable control  
b) each sensor must carry a guest operating system  
c) films must be cached in Chennai  
d) a truck must reach a flood

### A45
In SDN the two planes are

a) the map plane and the reduce plane  
b) the control plane, which decides where traffic should go, and the data plane, which forwards the packets  
c) the device plane and the billing plane  
d) the image plane and the container plane

### A46
In traditional networking, as taught here,

a) each switch or router contains both the decision and the forwarding  
b) a single controller owns every decision, and the switch only forwards  
c) packets are stored as Docker images  
d) the data plane is prohibited

### A47
Which SDN statement matches the notes?

a) switches still choose their own routes with a slow manual CLI, and the controller only draws a picture  
b) the controller decides and programs the devices; configuration uses APIs; the controller can reroute when something fails; vendor-neutral protocols help different makers work together  
c) SDN combines both planes back inside every device  
d) SDN is a cache of films

### A48
One edge server in a smart city is overloaded. The SDN example says the controller should

a) redirect traffic toward a nearer or less-loaded edge server  
b) send every camera frame to another country  
c) turn the network back into per-device CLI configuration  
d) replace the controller with a CDN origin

### A49
A CDN is

a) a spread of servers that keep copies of popular content near users  
b) a guest operating system  
c) the optional MapReduce phase  
d) a battery-powered sensor protocol

### A50
A viewer in Coimbatore asks for a film that is not yet on the nearby CDN server. The sequence in class is

a) the CDN invents the film without an origin  
b) the first request is fetched from the origin, the CDN stores a copy, and a later request is a cache hit on the nearby server  
c) every later request still crosses from America, which is the definition of a cache hit  
d) the origin is deleted after the first request

### A51
A mobile data centre is

a) a portable set of servers, storage, network equipment, and power, brought to a place where the permanent cloud cannot be reached  
b) a topic on an MQTT broker  
c) a Kubernetes scheduler  
d) the guest operating system inside a virtual machine

### A52
During a flood the internet is down. Rescue teams still need to process drone pictures beside the site. The technique is

a) a distant origin server only  
b) a mobile data centre  
c) a combiner  
d) an etcd backup in another country, with no local machine

### A53
Match the technique with the job in the smart-city design.

a) containers run the accident-detection model; virtual machines isolate the police database; SDN sends load to a free edge server; a CDN serves live updates to phones; a mobile data centre adds computers for a public emergency  
b) the CDN isolates the police database; the virtual machine is the truck; SDN is the film cache  
c) all five jobs are done by the MQTT broker  
d) the mobile data centre is the control plane of a normal office switch

### A54
A factory deploys lightweight analytics quickly, steers data to the nearest edge node, delivers training videos to many sites, and rolls a portable server out to a remote plant during a shutdown. Those four techniques, in that order, are

a) virtual machine, CDN, SDN, container  
b) container, SDN, CDN, mobile data centre  
c) MapReduce, CoAP, fog, PLC  
d) etcd, scheduler, pod, image

### A55
Containers, rather than virtual machines, are the better default for those lightweight analytics applications because

a) the edge machine is limited, and a container does not carry a second operating system  
b) a container isolates more strongly and therefore should hold the police database  
c) containers cannot be copied  
d) virtual machines cannot run on a hospital server at all

### A56
Resource management in edge computing means

a) allocating, scheduling, and watching the limited compute, storage, and network of scattered nodes  
b) deleting the cloud layer  
c) counting words with a reducer  
d) choosing a film codec

### A57
A container, as used for that management, is

a) a lightweight isolated environment holding the application, its libraries, and its dependencies, on a shared host operating system  
b) a full guest operating system with no application  
c) a regional electricity control room  
d) an AMQP binding

### A58
Docker, in this chapter, is the platform used to

a) orchestrate a whole cluster, including self-healing across many nodes  
b) build images and create, run, stop, and share containers  
c) train a national demand model  
d) forward packets at layer 2

### A59
Which row is correct?

a) image = template; container = running instance; Dockerfile = build instructions; registry = stored images; engine = the runtime that builds and runs  
b) image = running instance; container = a text file of instructions; engine = a CDN  
c) Dockerfile = the broker; image = a topic  
d) registry = the data plane; engine = the fog layer

### A60
The build order in the notes is

a) running container, then a Dockerfile written afterwards, then the image  
b) Dockerfile, then image, then a running container, then the application  
c) shuffle, then map, then split  
d) cloud, then sensor, then gateway

### A61
Docker alone is not enough for 100 containers across several nodes because

a) Docker cannot start even one container  
b) crashes, overload, extra copies, and bursts of traffic are too much to handle by hand; an orchestrator automates the life cycle  
c) containers are forbidden at the edge  
d) the image cannot be stored

### A62
Container orchestration, as defined here, automatically

a) deploys containers across servers, scales them up and down, spreads traffic, restarts failures, and connects them  
b) replaces HTTPS with Modbus  
c) moves the national archive onto a wearable  
d) writes the Map function

### A63
Kubernetes is

a) a replacement that removes Docker  
b) the orchestrator that deploys, scales, heals, and places Docker containers across a cluster  
c) a publish/subscribe protocol  
d) a portable truck

### A64
Which comparison matches the table?

a) Docker is for building and running containers, with more manual scaling; Kubernetes is for a cluster, with automated scaling, self-healing, and scheduling onto nodes  
b) Kubernetes builds the image, and Docker is only the etcd database  
c) they are two names for a CDN  
d) Docker manages the cluster and Kubernetes manages one container on one laptop only

### A65
A Kubernetes cluster is split into

a) a control plane that manages, and worker nodes that run the applications; the control plane does not normally run those workloads itself  
b) a data plane that trains models, and a CDN that stores etcd  
c) mappers and reducers only  
d) sensors and PLCs only

### A66
The control-plane components named in class are

a) kube-API server, kube-scheduler, controller manager, and etcd  
b) MQTT broker, CoAP client, WebSocket, and AMQP queue  
c) map, shuffle, reduce, and combine  
d) camera, meter, drone, and robot

### A67
On a worker node the notes place

a) the national billing report  
b) pods, and inside them containers, and inside those the applications  
c) only the SDN application layer  
d) the origin copy of a film and nothing else

### A68
Self-healing, in the Kubernetes list, means

a) a failed container can be restarted or replaced  
b) the cluster refuses to notice a crash  
c) every node must be rebuilt by hand from a DVD  
d) the data plane chooses routes without a controller

### A69
An edge server has 8 GB of RAM. Three applications ask for 3 GB, 4 GB, and 3 GB. The lesson is

a) 10 is less than 8, so all three start at full size  
b) they ask for 10 GB and only 8 GB exist, so something must allocate, shrink, or refuse  
c) RAM is unlimited on every edge node  
d) the combiner will add the three sizes

### A70
On the edge / fog / cloud comparison, processing and connectivity are described as

a) edge on the device itself, able to keep going when the network is poor; fog on nearby network resources; cloud in a data centre that needs a stable internet  
b) edge only in a foreign data centre; fog only inside one sensor chip; cloud with no network at all  
c) all three identical  
d) fog as the MapReduce reducer

### A71
In the smart-traffic fog example, the roadside node

a) stores ten years of video and trains the model as its main job  
b) detects the accident from the local video, and sends a summary or an alert to the cloud  
c) is a mobile data centre parked in another country  
d) is the etcd database

### A72
The cloud IoT platforms named together are

a) AWS IoT Core, Azure IoT Hub, Google Cloud IoT Core, IBM Watson IoT, and Oracle IoT Cloud  
b) Docker Hub, Kubernetes, etcd, and a CDN  
c) Modbus, OPC UA, and a PLC only  
d) NumPy, Pandas, and OpenCV

### A73
A cloud IoT platform, in that list of features, is expected to

a) add and retire devices, stream data, show dashboards, raise alerts, push firmware, and provide security  
b) replace the edge layer entirely  
c) act as a guest operating system  
d) be the optional combiner

### A74
Cloud integration is called critical for an IoT estate because it gives

a) a reason to upload every camera frame  
b) scale to many devices, links to systems such as ERP and CRM, automation, failover, and learning from the data  
c) a second guest operating system on each sensor  
d) a ban on local processing

### A75
Students, faculty, and administration share one physical campus network, but each group has its own logical network. That SDN use is

a) network slicing  
b) a cache miss  
c) task parallelism  
d) predictive maintenance

### A76
During exams, the exam servers are given priority over student downloads. That requirement is

a) a mobile data centre  
b) fine-grained traffic control  
c) a Docker Hub repository  
d) word count

### A77
The data plane and the control plane, in the OSI terms used in class, are

a) forwarding, mainly at layers 2 and 3; decisions at layer 3 and above  
b) both at the application layer only, with no forwarding  
c) the sensor and the cloud bill  
d) the image and the Dockerfile

### A78
Top to bottom, the SDN architecture in the notes is

a) application layer, control layer, infrastructure layer  
b) infrastructure layer, then the film cache, then etcd  
c) device, fog, cloud, with no controller  
d) producer, queue, consumer, with no exchange

### A79
The infrastructure layer of SDN

a) is the data plane: switches, routers, and firewalls forward traffic as the controller instructed  
b) trains the machine-learning model  
c) is the optional MapReduce phase  
d) is a wearable sensor

### A80
A serious disadvantage of putting control in one SDN controller is

a) containers start too quickly  
b) the controller is a single point of failure, so a dead controller can take the network down unless it is made highly available  
c) the data plane becomes unable to forward even when it has instructions  
d) network slicing becomes impossible

### A81
Other SDN disadvantages named in class are

a) a difficult join to old networks, staff who need new skills, a high starting cost, and standards that are not universal  
b) an inability to set a security policy  
c) a ban on automation  
d) faster manual CLI as the recommended method

### A82
SDN’s advantages include central management, live reconfiguration, lower manual operating cost, central security policy, and automated provisioning. The item that is **not** one of those advantages is

a) programming many devices from the controller  
b) treating a controller outage as harmless because traditional networks never needed a backup plan  
c) adapting to traffic without visiting each switch  
d) deploying a new behaviour in software

### A83
On the protocol picture, sensors reach the gateway with MQTT or CoAP, and the edge or fog node reaches the cloud with

a) a guest operating system  
b) HTTP or HTTPS  
c) a Dockerfile  
d) etcd replication only

### A84
Protocols are required in an edge system because

a) unlike devices still need a shared way to format data, identify each other, handle errors, and secure the exchange  
b) every sensor already shares one proprietary language  
c) the cloud refuses encrypted traffic  
d) Kubernetes replaces communication

### A85
MQTT is a publish/subscribe protocol. The broker’s place in that design is

a) publishers and subscribers talk to each other directly, and the broker is optional decoration  
b) clients do not talk to each other; the broker receives publications and delivers them to subscribers of the topic  
c) the broker is a guest operating system  
d) the broker is the reducer

### A86
`factory/machine1/temperature` with a payload of 78°C is

a) a Dockerfile and a container  
b) a topic and a message  
c) a control plane and a data plane  
d) a cache hit and an origin

### A87
A thousand sensors publish frequent readings, including one 91°C spike among many values near 31°C. The edge use of MQTT in the notes is

a) forward every reading, including the normal ones, and do no filtering  
b) let the gateway take the messages, and send onward the alert rather than the whole normal series  
c) replace MQTT with a virtual machine  
d) store the topic inside etcd as the analytics result

### A88
CoAP differs from ordinary HTTP, as taught here, because CoAP

a) is publish/subscribe and always uses TCP  
b) is a request/response protocol for constrained devices, and it commonly runs over UDP, whereas HTTP commonly uses TCP  
c) is a 3D scene format  
d) is the Kubernetes scheduler

### A89
HTTPS, in the edge-to-cloud notes, is

a) HTTP protected with TLS, used when the information is sensitive  
b) HTTP with the security removed  
c) another name for Modbus  
d) a cache hit

### A90
The AMQP path described in class is

a) producer to broker, then exchange, then queue, then consumer; a binding is the rule that ties an exchange to a queue  
b) consumer directly to the sensor, with no queue  
c) map to reduce, with no keys  
d) origin to viewer, with no cache

### A91
Which exchange behaviour is correct?

a) fanout keeps the message on one queue and drops the rest; direct sends it to every queue  
b) direct needs the routing key to match; fanout delivers to all bound queues; topic uses wildcards; headers use header fields rather than the routing key  
c) all four types ignore bindings  
d) headers are the same thing as a CDN

### A92
WebSocket is the right choice when

a) both sides must be able to push messages on a connection that stays open, as on a live dashboard  
b) the client must open a fresh request for every single update, which is the point of WebSocket  
c) the device is a constrained sensor that should use UDP  
d) the only need is a one-off REST call

### A93
Thousands of small sensor readings, a call to a cloud REST API, and a live monitoring screen are matched with

a) MQTT, HTTP/HTTPS, and WebSocket  
b) AMQP, CoAP, and a virtual machine  
c) CDN, SDN, and MDC  
d) map, reduce, and combine

### A94
The notes choose CoAP rather than MQTT when the comparison is

a) a factory of small telemetry messages that should be published to many listeners  
b) a battery-powered sensor on a poor, intermittent link, where the device itself is severely constrained  
c) an enterprise system that needs queues and acknowledgements  
d) a web API

### A95
Enterprise messaging, with queues, routing, and acknowledgements, is

a) AMQP  
b) a Dockerfile  
c) speedup  
d) a cloudlet

### A96
Five hundred limited sensors in a factory send a continuous trickle of small readings to an on-site edge server, and the processed result must travel securely to the cloud. The pair recommended in the notes is

a) MQTT from the sensors to the edge, and HTTPS from the edge to the cloud  
b) HTTPS from every sensor, and CoAP from the edge to the cloud  
c) WebSocket for the sensors and a guest operating system for the cloud  
d) Modbus for the cloud REST API

### A97
The protocol chapter’s closing rule is

a) MQTT is always best, for video, for REST, and for a queue  
b) there is no single best protocol; size, bandwidth, delay, power, reliability, pattern, scale, security, and the device all matter  
c) the cloud accepts only CoAP  
d) WebSocket is the industrial master/slave protocol

### A98
A cloud server in the challenge notes has 64 cores, 256 GB of RAM, and terabytes of disk. An edge device has 4 cores, 8 GB, and 128 GB. The challenge is

a) the edge device is the place for every heavy job  
b) resource limits: some work does not fit on the edge node and must be placed carefully  
c) the cloud cannot store a backup  
d) RAM on the edge is larger than RAM in the cloud

### A99
Security gets harder at the edge because

a) there is only one locked data-centre room  
b) there are many places, some of them physically exposed, so a device can be tampered with, data stolen, or bad software installed  
c) encryption is illegal on sensors  
d) authentication is needed only in the cloud

### A100
The security requirements named for that exposed edge are

a) authentication, authorization, encryption, secure boot, regular updates, and intrusion detection  
b) a cache hit and a guest operating system  
c) only a topic string  
d) speedup and a combiner

### A101
Edge computing can improve privacy by keeping a sensitive video local. The challenge that remains is

a) the edge device itself still has to be secured  
b) privacy requires sending the video to every public cloud  
c) local processing increases exposure by definition  
d) hospitals are forbidden to process images on site

### A102
One cloud, ten regional nodes, a hundred edge servers, and ten thousand devices illustrate

a) a CDN cache hit  
b) distributed management: deploying, watching, updating, and healing that estate is hard, which is why containers and Kubernetes appear, even though a scattered edge is still harder than one data centre  
c) data parallelism on one processor  
d) a single PLC ladder

### A103
The internet between an edge server and the cloud drops. The design in the notes is

a) stop all local work until the cloud answers  
b) keep processing locally, keep the result, and synchronise when the link returns  
c) delete the local result so the cloud cannot be confused  
d) rebuild the SDN controller

### A104
A city grows from 100 sensors and 10 edge nodes to 100,000 sensors and 5,000 edge nodes. The design response named in class is

a) vertical scaling of one sensor until it holds the whole city  
b) horizontal scalability: the architecture must accept more devices, applications, users, data, and sites  
c) a ban on new sensors  
d) moving the brake decision to a yearly batch job

### A105
Edge nodes in one estate include x86, ARM, a Raspberry Pi, and a GPU server, on Linux and Windows. The honest conclusion is

a) containers make the same application easier to carry, but hardware and operating-system differences can still break compatibility  
b) containers erase every hardware difference  
c) heterogeneity is not a challenge  
d) only one architecture is allowed to join an edge system

### A106
One hundred cameras at 10 MB/s produce about 1 GB/s. Data management at the edge therefore means

a) uploading the 1 GB/s unchanged, because filtering is lossy and forbidden  
b) filter, aggregate, compress, drop duplicates, store briefly, and analyse locally, forwarding the important events  
c) counting the bytes with a reducer and taking no other action  
d) replacing the cameras with a CDN

### A107
An edge node can fail from hardware, power, software, or the weather. Reliability then requires

a) a backup node, failover, local redundancy, or a recovery path  
b) a promise that edge hardware never fails  
c) deletion of all neighbouring nodes  
d) a single controller with no high availability, used as the recovery plan

### A108
Putting a task on the device, on the edge, or in the cloud is a challenge because

a) the three places have the same CPU and the same delay  
b) the device is fastest and most private but poorest in resources; the edge adds power and cuts traffic; the cloud adds heavy analytics at the price of delay and bandwidth  
c) the cloud is always faster than the device  
d) privacy is highest when the raw video is public

### A109
Cost and maintenance of an edge estate include

a) only the cloud invoice  
b) hardware, power, cooling, physical security, updates, and technical support in many places  
c) a single snapshot of one virtual machine and nothing else  
d) the word-count reducer

### A110
A remote mine has a small edge server, a link that comes and goes, mixed vehicle hardware, sensitive operational data, and a growing fleet. Four of the challenges on display are

a) resource limits, connectivity, heterogeneity, and security or distributed management  
b) cache hits, guest operating systems, film encoding, and word count  
c) only a shortage of cloud disk  
d) only an SDN standard

### A111
The matching remedies in that mining answer are

a) ignore the limits and upload every camera frame  
b) lightweight containers and careful placement; local processing with a buffer; containers for portability; encryption and local handling of sensitive data; orchestration such as Kubernetes; time-critical work at the edge and selected data to the cloud  
c) one virtual machine in another country for the brake decision  
d) a fixed three-month service calendar and no sensing

### A112
If that mine loses the cloud for 30 minutes, the work that must continue on site is

a) obstacle detection, collision avoidance, and the immediate driving decision  
b) a national monthly report and a model retrain  
c) only the long-term archive  
d) nothing, because an edge server is defined to stop when the cloud stops

### A113
The work that can wait for the link to return is

a) the collision-avoidance decision  
b) uploading non-critical data, long-term storage, large-scale analysis, historical reports, and a model update that is not needed for the next second  
c) local sensing  
d) the driver’s immediate alert

---

# Unit 4 — Parallel processing, MapReduce, edge analytics, architecture, and IIoT

### B1
Parallel processing, as defined in class, is

a) one processor working through a large job from start to finish  
b) dividing a large job into smaller pieces and executing those pieces at the same time on several processors  
c) sending every sensor reading to a single cloud function  
d) storing a film on the nearest CDN server

### B2
The four steps, in order, are

a) Combine, Execute, Distribute, Divide  
b) Divide, Distribute, Execute simultaneously, Combine  
c) Map, Combine, Shuffle, Split  
d) Sense, Brake, Train, Retire

### B3
Sequential processing differs from parallel processing in that sequential processing

a) uses many processors and finishes a large job sooner by design  
b) does one piece at a time, usually on one main processor, and is simpler but less able to grow  
c) always requires a shuffle  
d) cannot produce a correct result

### B4
One million temperature readings are split into four blocks of 250,000, and each processor computes the same kind of average on its own block. This is

a) data parallelism: the same operation, different data  
b) task parallelism: different operations at the same time  
c) a CDN cache hit  
d) network slicing

### B5
Temperature analysis, vibration analysis, and fault detection run at the same time on different processors. This is

a) data parallelism  
b) task parallelism: different tasks, executed together  
c) a single sequential loop  
d) an AMQP header exchange

### B6
Which statement matches the comparison?

a) data parallelism splits the data and repeats one operation; task parallelism splits the tasks  
b) data parallelism always runs different algorithms; task parallelism always averages one array  
c) they are two names for a container  
d) both forbid communication between processors

### B7
Parallel processing is used because it can

a) shorten the run, handle a large set by splitting it, grow by adding nodes, use idle machines, and raise throughput  
b) remove communication and synchronisation  
c) guarantee a four-times speedup from four processors  
d) replace edge analytics for a millisecond brake

### B8
A result cannot be combined until the slow piece finishes. That challenge is

a) synchronisation  
b) a cache hit  
c) protocol translation  
d) secure boot

### B9
Processors spend time exchanging data before the final answer exists. That challenge is

a) communication overhead  
b) a guest operating system  
c) horizontal scalability of cameras  
d) predictive maintenance

### B10
Four nodes receive 10%, 10%, 10%, and 70% of the work. The defect is

a) perfect data parallelism  
b) load imbalance  
c) a cache hit  
d) an empty reducer input

### B11
One node cannot start until another node’s output exists. The challenge is

a) data dependency  
b) an SDN cache  
c) MQTT keep-alive  
d) a Docker registry

### B12
In a parallel job a node dies, and the lost piece must be recovered or recomputed. The challenge is

a) fault tolerance  
b) a CDN origin  
c) task parallelism’s definition  
d) the device layer generating raw data

### B13
Speedup is defined as

a) parallel time divided by sequential time  
b) sequential time divided by parallel time  
c) the number of processors multiplied by the sequential time  
d) the size of the dataset divided by the number of keys

### B14
A job takes 100 seconds on one processor and 30 seconds in parallel. The speedup is about

a) 4, because four processors were hoped for  
b) 3.33, and not 4, because of communication, synchronisation, imbalance, dependencies, transfer, and coordination  
c) 0.30  
d) 130

### B15
A billion sensor records take 10 hours on one machine. Splitting them across four nodes so that each node takes about 250 million is an example of

a) data parallelism, organised as a parallel divide-and-combine  
b) one MQTT publish  
c) a cache miss  
d) a PLC ladder that turns on a cooler

### B16
If node 4 is much slower than the others, and if node 2 dies, the two problems are

a) load imbalance, and fault tolerance  
b) a cache hit, and a guest operating system  
c) privacy, and a CDN  
d) CoAP, and WebSocket

### B17
The programming model that organises this large batch into Map and Reduce is

a) MQTT  
b) MapReduce  
c) OPC UA  
d) Node-RED

### B18
Between Map and Reduce, the system step named in class is

a) live migration  
b) shuffle and sort  
c) secure boot  
d) network slicing

### B19
The MapReduce pipeline in the notes is

a) input, map, intermediate key-value pairs, shuffle and sort, reduce, final output  
b) reduce, then map, then delete the keys  
c) container, image, Dockerfile  
d) device, fog, cloud, with no keys

### B20
`(MachineB, Fault)` is

a) a key-value pair, the basic record MapReduce passes between stages  
b) a Docker image  
c) an SDN controller  
d) a speedup ratio

### B21
Counting machine status, the Map step emits

a) `(Normal, 1)` or `(Fault, 1)` for each machine  
b) the final totals immediately, with no intermediate pairs  
c) a guest operating system  
d) a topic subscription

### B22
After shuffle and sort, the notes show

a) every repeated 1 deleted, so each status can only be 1  
b) `Normal → [1, 1, 1]` and `Fault → [1, 1]`, the values kept and grouped by key  
c) the original sentences, still unsorted  
d) a single list with the keys thrown away

### B23
The Reduce step on those lists produces

a) Normal 3 and Fault 2  
b) Normal 1 and Fault 1, because duplicates were deleted  
c) a cache hit  
d) five machines still uncounted

### B24
The phases named for MapReduce are mapping, shuffling and sorting, reducing, and

a) combining, which is optional and is there to make the shuffle quicker  
b) combining, which is mandatory or the totals are wrong  
c) braking, which is mandatory  
d) slicing, which replaces the reducer

### B25
Map’s input and output, as described in class, are

a) a key-value input record `(k, v)`, and a key-value output `(k', v')`  
b) a finished total in, and a raw file out  
c) a container in, and a virtual machine out  
d) a packet in, and a route out

### B26
Shuffle and sort hand the reducer

a) `(k, v[])`, a key and the list of values that shared it  
b) unrelated files in arrival order  
c) only the keys, with every value removed  
d) the original camera frames

### B27
Word count on “Cloud computing is useful” and “Cloud computing is scalable” reduces `Cloud` to

a) 1  
b) 2  
c) 8  
d) 0

### B28
In that same count, `useful` and `computing` reduce to

a) 1 and 2  
b) 2 and 1  
c) 2 and 2  
d) 0 and 0

### B29
The component order in the MapReduce flow diagram is

a) output, reducer, mapper, split  
b) input, split, mapper, shuffle, sort, reducer, output  
c) broker, exchange, queue, consumer  
d) sensor, PLC, cooler

### B30
A mapper differs from a reducer in that the mapper

a) processes input records and emits intermediate pairs, in parallel across splits  
b) receives the grouped lists and writes the final aggregate  
c) runs only after every reducer has finished  
d) is the optional phase

### B31
A reducer differs from a mapper in that the reducer

a) can run in parallel for different key groups, after shuffle and sort, and it produces the aggregated result  
b) emits `(Fault, 1)` from a raw record and then stops the cluster  
c) is forbidden to run in parallel  
d) replaces the input split

### B32
MapReduce is attractive for a huge dataset because

a) the programmer mainly writes Map and Reduce, while the framework handles distribution, and failed work can be run again  
b) it answers in a millisecond  
c) it refuses extra nodes  
d) it stores no intermediate data

### B33
Traditional MapReduce is a poor fit when

a) the job is a large batch, such as counting or an ETL pass over stored logs  
b) the job needs a millisecond response, repeats many iterations the way some learning algorithms do, or suffers from a heavy shuffle and heavy disk traffic  
c) the data set is too large for one machine  
d) the keys can be grouped

### B34
Batch processing and stream processing, as contrasted in the notes, are

a) batch collects work and processes it as a job; stream processes data as it arrives  
b) two names for the edge brake  
c) both defined as millisecond MapReduce  
d) CDN and SDN

### B35
Data locality helps MapReduce because

a) it reduces how far the data must move across the network  
b) it deletes duplicate keys before the mapper runs  
c) it replaces the reducer  
d) it is the same idea as a mobile data centre

### B36
Stopping a machine the moment vibration crosses a limit, and counting a billion stored records, belong respectively to

a) MapReduce, and edge analytics  
b) edge analytics or a local threshold, and MapReduce  
c) a CDN, and a PLC  
d) etcd, and a Dockerfile

### B37
Edge analytics means

a) analysis close to where the data is produced, so a useful decision does not wait for every raw reading to reach the central cloud  
b) analysis that starts only after the raw archive has crossed the country  
c) a programming model whose main stages are Map and Reduce  
d) a portable truck

### B38
Edge analytics is needed when there is

a) a huge volume, a tight delay, limited bandwidth, a link that may drop, a privacy constraint, or a decision that must be local  
b) a requirement that every raw sample be archived before any alert  
c) no sensor on site  
d) a single batch job with no deadline

### B39
On the comparison table, edge analytics and cloud analytics line up as

a) edge near the source, very low delay, limited storage, excellent immediate decisions; cloud in the data centre, much more capacity, excellent history and model training  
b) edge as the place for national training; cloud as the place for the emergency brake  
c) both unable to filter  
d) edge with higher bandwidth demand because it always ships raw data

### B40
The edge-task list and the cloud-task list are

a) edge: filter, preprocess, aggregate, detect events and anomalies, infer locally, and act at once; cloud: store, study history, train, report, and compare sites  
b) the reverse of that list  
c) both lists assigned to the mapper  
d) both lists assigned to the wearable battery

### B41
An ATM camera recognises tampering and shuts the machine down before anyone uploads the clip. The pattern is

a) local inference and local action, then an alert  
b) MapReduce word count  
c) a yearly preventive calendar with no sensing  
d) a cache of the film in another country

### B42
Predictive maintenance differs from waiting for the breakdown in that it

a) estimates the failure before it happens, so the repair can be scheduled first  
b) services every machine on a fixed date and ignores the sensor  
c) is a CDN function  
d) requires the raw video to reach a foreign data centre before the machine may stop

### B43
An ambulance cannot usefully upload a critical patient’s data before anyone acts. The lesson is

a) analyse on the spot  
b) wait for the cloud report  
c) use MapReduce on the journey  
d) store the vitals only as a monthly bill

### B44
Filtering, aggregation, and a threshold, with the examples from class, are

a) send only temperatures above 80°C; send a one-minute average; raise an alert when vibration crosses a set limit  
b) three names for model training in the cloud  
c) the SDN planes  
d) image, container, and pod

### B45
Anomaly detection differs from a plain threshold in that anomaly detection

a) looks for an unusual pattern, not only for a value that crossed a number written in advance  
b) is defined as the average of one minute  
c) can run only as a batch the next day  
d) is another name for HTTPS

### B46
Local decision making, in the methods table, is illustrated by

a) stopping the machine when a fault is detected, without waiting for the cloud  
b) training the model on a ten-year archive  
c) translating Modbus to MQTT  
d) writing a Dockerfile

### B47
Compression or summarisation at the edge is illustrated by

a) turning 10,000 readings into an hourly statistic before transmission  
b) sending all 10,000 readings because a summary is forbidden  
c) deleting the fault so the cloud stays small  
d) replacing the sensor with a reducer

### B48
NumPy, Pandas, scikit-learn, OpenCV, and TensorFlow Lite or LiteRT are grouped as

a) Python tools for numbers, tables, model inference, images, and on-device inference  
b) the five SDN layers  
c) industrial master/slave protocols  
d) the Kubernetes control plane

### B49
PySpark is recommended when

a) the node is a tiny constrained sensor  
b) the edge server has enough capacity for stream processing, distributed analytics, or MapReduce-style work  
c) the only need is a browser flow chart  
d) the job is a single threshold on a battery sensor

### B50
Node-RED, in these notes, is

a) a browser-based flow editor for showing and wiring an IoT path  
b) a messaging protocol  
c) a data warehouse  
d) the reducer

### B51
MQTT’s relationship to edge analytics is

a) MQTT is the analytics algorithm that detects the fault  
b) MQTT carries the message; the edge server does the threshold check and then acts  
c) MQTT trains the model  
d) MQTT is a guest operating system

### B52
A factory camera, an edge computer, OpenCV, and a defective product illustrate

a) image analytics at the edge  
b) a national ETL batch as the first and only step  
c) network slicing  
d) an AMQP header exchange

### B53
Tools placed at the sensor, the gateway, the edge server, and the cloud are, in that order,

a) a simple threshold; MQTT, Node-RED, and aggregation; Python or PySpark and inference; large analytics, a warehouse, and training  
b) training; a warehouse; a threshold; a PLC cooler  
c) etcd at the sensor and a camera at the control plane  
d) four copies of the same reducer

### B54
A machine’s vibration becomes abnormal. The edge system detects it without waiting for the cloud by

a) applying a threshold or an anomaly check locally and raising the alert on site  
b) opening a MapReduce job on the stored year of data before the machine may stop  
c) asking a CDN origin in another country  
d) waiting for the next preventive calendar date

### B55
What should be sent to the cloud instead of every raw reading?

a) summaries and the important events  
b) nothing, ever, including faults  
c) the guest operating system  
d) the SDN controller state only

### B56
The factory-to-cloud link drops. The edge system should

a) keep the local detection running, buffer what must be kept, and synchronise when the link returns  
b) stop the sensors until the cloud is back  
c) discard the buffer so synchronisation is unnecessary  
d) move the brake decision into tomorrow’s batch

### B57
Against a cloud-only design, the edge design in the traffic case improves

a) latency, bandwidth, local privacy, and operation during a lost link  
b) the need to ship every video frame  
c) millisecond MapReduce  
d) nothing, because the cloud is always nearer than the intersection

### B58
The IoT and edge architecture, from the physical world upward, is

a) cloud, then a reducer, then a sensor  
b) sensors or endpoints, edge devices, edge gateways, edge servers, cloud  
c) control plane, data plane, etcd  
d) map, shuffle, reduce

### B59
A sensor and an endpoint differ in that

a) a sensor measures a physical quantity; an endpoint is any edge party that generates, receives, or exchanges data. A sensor can be an endpoint, but not every endpoint is only a sensor  
b) they are synonyms, and a camera cannot be an endpoint  
c) an endpoint is always the cloud  
d) a sensor is always a PLC

### B60
An edge device, in this architecture, is

a) the national archive  
b) a computer near the source that can collect, filter, detect, alert, store for a while, and forward the selected result  
c) only a cable with no computation  
d) the place where the model must be trained

### B61
A reading of 95°C is critical and the normal readings are not. The edge device should

a) mark the critical alert and summarise the normal run, rather than treat every sample as equally urgent  
b) drop the 95°C reading because it is inconvenient  
c) train a new model before the alert  
d) translate the number into Modbus and stop

### B62
An edge gateway’s defining jobs include

a) connectivity, protocol translation, aggregation, filtering, security, and forwarding  
b) national model training as its only job  
c) being a tiny sensor with no network role  
d) replacing the PLC as the device that closes a relay

### B63
Bluetooth, Zigbee, Modbus, and Wi-Fi sensors are brought into one system by

a) the gateway, which translates and gathers them  
b) the cloud, which speaks all four with no gateway  
c) a reducer  
d) a CDN edge cache

### B64
A traditional IoT gateway and an edge gateway differ in that

a) the traditional gateway is mainly a connection, and the analytics happen later in the cloud; the edge gateway can also find events before it transmits  
b) the traditional gateway trains models and the edge gateway cannot aggregate  
c) they are the same object as a PLC  
d) neither is allowed to filter

### B65
An edge server is added when a small device cannot host

a) vision, several applications, a local database, containers, or a heavier inference  
b) a single threshold  
c) a topic string  
d) one temperature sample

### B66
The edge server’s extra contribution, beyond a small sensor, is

a) joining several signals, running inference, keeping recent history, and raising a local alert  
b) generating the raw voltage  
c) being the master in a Modbus exchange only  
d) replacing the cloud for a ten-year national archive

### B67
Edge device management is the work of

a) registering, configuring, monitoring, securing, updating, repairing, and retiring devices  
b) writing only the Map function  
c) caching films  
d) choosing Spot versus On-Demand

### B68
A remote update of a thousand devices should include

a) version control, a staged rollout, a way to roll back, and a check that the update landed  
b) a visit to each device as the preferred method  
c) deletion of the device identity  
d) a full guest operating system copied from a neighbour with no check

### B69
High CPU, old software, and a device that has stopped answering are handled by

a) moving or reducing the heavy workload; a checked remote update; a health check, a restart, and a technician if it stays dead  
b) ignoring all three until the next yearly report  
c) sending each problem to a word-count reducer  
d) turning the three devices into one CDN origin

### B70
The life cycle in the notes runs

a) retire, then deploy, with no monitoring in between  
b) deploy, register, configure, operate, monitor, update, maintain, retire  
c) map, reduce, brake  
d) slice, cache, train

### B71
On the role table, the gateway and the server are distinguished by

a) the gateway connecting, translating, and aggregating; the server doing the heavier local analytics and inference  
b) the gateway training the national model; the server only measuring temperature  
c) both being unable to filter  
d) the server being less powerful than the sensor

### B72
The verb chain sense, collect and process, connect and aggregate, analyse and compute, store and analyse at scale belongs to

a) sensors, edge devices, gateways, edge servers, and the cloud  
b) mapper, reducer, combiner, shuffle, and split  
c) five names for the PLC  
d) the SDN application layer repeated five times

### B73
Readings 72, 73, 74, 75, and 92 arrive, and the fault line is 80°C. The edge device should

a) upload all five raw values immediately and do nothing else  
b) treat 92 as the fault, send that event promptly, and send a summary rather than five urgent raw samples  
c) ignore 92 because four readings were normal  
d) start model training on the wearable before anyone is told

### B74
Machines speak Modbus, OPC UA, and MQTT. Before the edge server sees one stream, the gateway should

a) translate them into a common message  
b) refuse every protocol except the first  
c) send the three protocols to the cloud unaltered as the main design  
d) replace them with a reducer

### B75
One hundred sensors report every second. A useful gateway output is

a) all one hundred readings forwarded unchanged, as the preferred design  
b) a zone average, a minimum, a maximum, and the fault count  
c) a new virtual machine per reading  
d) the etcd dump

### B76
Under normal operation, under a fault, and during a network outage, the cloud should receive

a) a periodic summary; the machine, the value, the threshold, and the time; and, while the link is down, nothing until the local buffer is synchronised later  
b) every raw sample in all three cases  
c) nothing in the normal case and the entire raw video during the outage  
d) a model-training job from the sensor in all three cases

### B77
During a 30-minute cloud outage the layers should

a) stop sensing until the cloud returns  
b) keep sensing, filtering, translating, buffering, and making local safety decisions, then synchronise the buffer  
c) move safety decisions to the cloud queue and wait  
d) retire every device

### B78
The sentence that matches the notes is

a) edge analytics means the cloud is never sent any data  
b) edge analytics means the edge processes intelligently and the cloud still receives the appropriate information  
c) the edge server is only a cable  
d) the gateway is forbidden to aggregate

### B79
IIoT, as defined in class, is

a) any consumer gadget that happens to contain a sensor  
b) connected sensors, machines, controllers, and software in industry, where safety, a real-time response, and continuous operation matter  
c) a film-distribution network  
d) the MapReduce shuffle

### B80
IoT and IIoT are distinguished by

a) the brand of the temperature chip  
b) the purpose: a home or personal device is IoT; an industrial machine, a plant, or an operational-technology process is IIoT  
c) IIoT being unable to use a network  
d) IoT being unable to use MQTT

### B81
A failed industrial controller can stop production or create a safety incident. A failed consumer gadget usually cannot. That is why IIoT stresses

a) reliability, safety, real-time behaviour, and continuous operation  
b) a larger film cache  
c) word count  
d) scale-to-zero of a website

### B82
Vibration sensing on a rotating machine is used especially to notice

a) bearing trouble, imbalance, misalignment, or wear  
b) a user’s step count  
c) a cache miss  
d) an SDN controller election

### B83
In the IIoT path described in class, a sensor often

a) speaks first to a PLC or industrial controller, rather than opening a direct cloud session  
b) trains the model on the sensor die  
c) is the CDN origin  
d) is the Kubernetes API server

### B84
A PLC and edge computing are related as follows

a) the PLC closes the loop, for example turning cooling on above 90°C; edge computing analyses the process. They complement each other  
b) the PLC is a batch reducer, and edge computing is forbidden on a plant  
c) they are competitors, and a plant must choose only one  
d) the PLC delivers films

### B85
An industrial edge gateway in the notes sits between the PLC and the edge server, with

a) OPC UA or Modbus on the machine side, and MQTT toward the edge server  
b) a guest operating system as the only protocol  
c) WebSocket as a master/slave field bus  
d) etcd as the coolant controller

### B86
OPC UA is described as

a) a platform-independent industrial standard, with encryption and authentication, a hierarchical information model, both client-server and publish/subscribe, and a bridge from the machines to IT  
b) a master/slave bus on which only the master may speak, used mainly because the equipment is old  
c) a Python charting library  
d) the optional combiner

### B87
Modbus is described as

a) a common industrial protocol, often on older equipment, in which the master requests and the slave replies  
b) a publish/subscribe broker for millions of phones  
c) a CDN  
d) a Kubernetes pod

### B88
The temperature bands in the IIoT notes are

a) below 80°C normal, 80 to 90°C a warning, above 90°C critical, with the alert raised at the edge  
b) every value critical  
c) only values below 80 sent to a foreign data centre before anyone may act  
d) a yearly average with no bands

### B89
Anomaly detection on a plant leads toward predictive maintenance because it

a) notices a sudden change, an odd pattern, or an odd combination of signals, rather than waiting for a calendar date  
b) services the machine every three months whether or not it is healthy  
c) deletes the vibration channel  
d) replaces the PLC ladder with a film cache

### B90
Fixed-interval preventive maintenance can fail because

a) a healthy machine may be serviced too early, and a failing machine may break before the scheduled day  
b) it uses too many sensors by definition  
c) it is the same method as continuous condition monitoring  
d) it can run only on a CDN

### B91
Predictive maintenance through the edge watches condition continuously and then

a) raises a maintenance alert before the failure  
b) waits for the calendar regardless of the vibration  
c) ships every raw sample before the alert is allowed  
d) turns off the PLC permanently

### B92
The learning loop in the IIoT notes is

a) train on historical data in the cloud, deploy the model to the edge for local inference, and send events back so the model can be retrained  
b) train on the sensor, and forbid the cloud to see an event  
c) infer only in a yearly batch, with no local model  
d) replace inference with Modbus reads

### B93
Edge security in this IIoT chapter means

a) authentication, authorization, encryption, controlled software updates, and watching for strange access or traffic  
b) a public broker with no identity  
c) security only inside the film cache  
d) a decision to skip patches because the plant is air-gapped in spirit

### B94
Which classification matches the answer key in class?

a) a smart refrigerator, a smartwatch, a home washing machine, and a fitness band are IoT; motor temperature, bearing vibration, refinery pressure, and a production-line defect camera are IIoT  
b) the refrigerator is IIoT because it contains a sensor, and the refinery is IoT because pressure is a common measurement  
c) all eight are IIoT  
d) all eight are IoT

### B95
A home garden that waters itself, and a municipal water plant that watches pressure and flow, are

a) both IIoT, because both use water  
b) IoT, and IIoT  
c) IIoT, and IoT  
d) both a CDN

### B96
A camera in a factory cafeteria that watches people, and a camera on the production line that rejects a bad product, are

a) IoT, and IIoT  
b) both IIoT, because both are cameras  
c) both IoT, because both record video  
d) SDN, and a reducer

### B97
A phone-controlled door lock, a PLC driving an industrial motor, a car telling the driver about tyre pressure, and a wind turbine watched for maintenance are

a) IoT, IIoT, IoT, IIoT  
b) IIoT, IoT, IIoT, IoT  
c) all IIoT  
d) all IoT

### B98
A house thermostat, steam in a power plant, a streetlight that switches on at dusk, and humidity inside a pharmaceutical plant are

a) IoT, IIoT, IoT, IIoT  
b) IIoT, IoT, IIoT, IoT  
c) all decided by the protocol alone  
d) all MapReduce jobs

### B99
The protocol families paired with ordinary IoT and with IIoT in the closing notes are

a) MQTT, HTTP/HTTPS, CoAP, and WebSocket for IoT; OPC UA and Modbus for IIoT  
b) OPC UA for a fitness band, and CoAP as the only plant protocol  
c) Map and Reduce  
d) Dockerfile and image

### B100
A connected car that only warns the driver about tyre pressure is classified as IoT, while vibration and temperature on a wind turbine are IIoT, because

a) classification follows the operational purpose, not the mere presence of a sensor or a radio  
b) cars cannot contain sensors  
c) wind turbines are consumer appliances  
d) tyre pressure is an industrial field bus

---

# Answers — Unit 3

| Q | Answer | Why this is the best option |
|---|---|---|
| A1 | **b** | Processing and storage move closer to the sensors, the users, or the devices. |
| A2 | **b** | The car example is about delay, and the accident that delay can cause. |
| A3 | **a** | The camera story lists a huge transfer, a slow response, and a high network cost. |
| A4 | **a** | Latency, congestion, bandwidth, and internet dependence are the four problems on the opening slides. |
| A5 | **c** | Limited compute and limited storage are the stated limitations. The other items are advantages. |
| A6 | **b** | Bandwidth falls when the camera sends the intrusion event instead of the continuous video. |
| A7 | **a** | Continuing through an outage is the reliability role. |
| A8 | **b** | Keeping the face match inside the hospital is the privacy role. |
| A9 | **a** | The cloud works on a summary, so storage, compute, and traffic shrink. |
| A10 | **b** | Google Drive stands for cloud storage. The autonomous vehicle stands for a real-time edge decision. |
| A11 | **a** | The diagram is sensors, then the edge, then the cloud. Edge does not abolish the cloud. |
| A12 | **b** | History, reports, analytics, and long-term storage stay cloud jobs. |
| A13 | **a** | Signals, emergency alerts, and accident detection cannot wait. |
| A14 | **a** | The alert is local. The long record, the slow trend, and sharing across hospitals are cloud jobs. |
| A15 | **b** | The notes add battery life, a device that can be lost or attacked, and the cost of many devices. |
| A16 | **a** | Device, edge server or gateway, fog or cloudlet, cloud. |
| A17 | **b** | Data climbs. Control may come back down. |
| A18 | **a** | The device layer generates data and is short of CPU, memory, and often power. |
| A19 | **a** | Filtering, aggregation, local analytics, event detection, and a real-time decision are why this layer is called the heart of the design. |
| A20 | **b** | One thousand images become one event. |
| A21 | **a** | Cloudlet, fog node, and regional data centre are the names used for that one intermediate layer. |
| A22 | **a** | A region must coordinate many edge servers. One gateway sees only its own neighbourhood. The hospitals in one city are the example. |
| A23 | **a** | Years of records, training, big analytics, backup, and disaster recovery belong in the cloud. |
| A24 | **b** | Raw, filtered, aggregated, historical. |
| A25 | **a** | Delay increases as the processing moves away. Compute and storage increase as well. |
| A26 | **a** | Meters generate. The substation acts. The region balances. The nation stores, forecasts, and bills. |
| A27 | **b** | A fault must be isolated in milliseconds. The cloud trip is too slow. |
| A28 | **a** | Rerouting power across substations needs a regional view. |
| A29 | **a** | Those five are the stated costs of a cloud-only grid. |
| A30 | **b** | Motion on the camera, suspicion on the nearby server, congestion at the regional server, memory and training at the centre. |
| A31 | **a** | Wearable, detect the bad beat, alert the doctor, store the history. |
| A32 | **a** | Camera, detect the vehicle, optimise the city, store the history. |
| A33 | **a** | The brake is on the vehicle. Coordination is at the roadside fog. The software update comes from the cloud. |
| A34 | **a** | Latency, bandwidth, scale, reliability, local decisions, privacy, and a lighter cloud. |
| A35 | **b** | Management, weak edge hardware, cost, security, synchronisation, and mixed machines are the stated limits. |
| A36 | **a** | Virtual machines, containers, SDN, CDN, and mobile data centres. |
| A37 | **b** | A virtual machine is a software computer with its own guest operating system. |
| A38 | **a** | Isolation, several applications, live migration, and better use of one server. |
| A39 | **b** | The guest operating system is why memory is high and startup is slow. |
| A40 | **a** | Shared host operating system is the definition of the container in this lesson. |
| A41 | **a** | Dependencies travel with the application. The guest operating system does not. |
| A42 | **b** | Light, fast, easy to copy, and cheaper in memory: the reason they suit the edge. |
| A43 | **a** | That is the comparison table: strong and heavy versus moderate and light. |
| A44 | **a** | Central programmable control replaces box-by-box configuration. |
| A45 | **b** | Control decides. Data forwards. |
| A46 | **a** | Traditionally both planes sit inside each device. |
| A47 | **b** | Controller, APIs, fast reroute, and vendor-neutral behaviour are the SDN column. |
| A48 | **a** | The overloaded server is relieved by sending traffic to a less-loaded edge server. |
| A49 | **a** | Copies of popular content live near the user. |
| A50 | **b** | A miss goes to the origin, the copy is stored, and the next request is a hit. |
| A51 | **a** | Servers, storage, network, and power, moved to the site. |
| A52 | **b** | The flood has no path to the distant cloud, so the data centre comes to the flood. |
| A53 | **a** | Each technique is doing the job named for it in the combined city example. |
| A54 | **b** | Light analytics, dynamic path, videos near many sites, portable computers at a remote shutdown. |
| A55 | **a** | The analytics application does not need a second operating system on a small machine. |
| A56 | **a** | Allocate, schedule, and watch limited compute, storage, and network. |
| A57 | **a** | Application, libraries, and dependencies, isolated, on the host operating system. |
| A58 | **b** | Docker builds and runs containers. Orchestrating the cluster is the next tool. |
| A59 | **a** | Image, container, Dockerfile, registry, and engine are the five terms on the table. |
| A60 | **b** | Instructions, then the image, then the running container. |
| A61 | **b** | A hundred containers, crashes, and traffic spikes are an orchestration problem. |
| A62 | **a** | Deploy, scale, balance, heal, and connect. |
| A63 | **b** | Kubernetes manages containers at cluster scale. It works with Docker. |
| A64 | **a** | One host and a manual scale, versus a cluster and an automatic scale. |
| A65 | **a** | Control plane manages. Workers run the applications. |
| A66 | **a** | API server, scheduler, controller manager, and etcd. |
| A67 | **b** | Pods hold containers, and containers hold the applications. |
| A68 | **a** | A failed container is restarted or replaced. |
| A69 | **b** | 3 + 4 + 3 is 10, and the machine has 8. Allocation is required. |
| A70 | **a** | On-device edge, nearby fog, distant cloud that needs the internet. |
| A71 | **b** | The roadside fog node finds the accident and forwards the alert, not the whole film archive. |
| A72 | **a** | Those five are the platforms written on the slide. |
| A73 | **a** | Provisioning, streaming, dashboards, alerts, firmware, and security. |
| A74 | **b** | Scale, links to other business systems, automation, failover, and learning. |
| A75 | **a** | Several logical networks on one physical network. |
| A76 | **b** | Priority for the exam servers is fine-grained control. |
| A77 | **a** | Forwarding at layers 2 and 3. Decisions from layer 3 upward. |
| A78 | **a** | Application, control, infrastructure. |
| A79 | **a** | The infrastructure layer is the data plane. |
| A80 | **b** | One controller is a single point of failure unless it is highly available. |
| A81 | **a** | Legacy integration, skills, initial cost, and incomplete standards. |
| A82 | **b** | A controller outage is a disadvantage, not an advantage. The other items are the advantage list. |
| A83 | **b** | The top of the stack is HTTP or HTTPS into the cloud. |
| A84 | **a** | Unlike devices still need a common language. |
| A85 | **b** | The broker is the only party both clients must know. |
| A86 | **b** | The slashed string is the topic. 78°C is the message. |
| A87 | **b** | The gateway keeps the normal series and forwards the alert. |
| A88 | **b** | Constrained request/response, commonly over UDP. |
| A89 | **a** | TLS is what turns HTTP into HTTPS for the sensitive hop. |
| A90 | **a** | Producer, broker, exchange, queue, consumer. The binding joins exchange and queue. |
| A91 | **b** | Direct matches. Fanout floods. Topic uses wildcards. Headers use the header. |
| A92 | **a** | The connection stays up, and either side may speak. That is the dashboard case. |
| A93 | **a** | Small telemetry, a REST call, a live screen. |
| A94 | **b** | CoAP is the choice when the device and the network are both severely constrained. MQTT remains the factory telemetry choice when many small readings are published. |
| A95 | **a** | Queues, routing, and acknowledgements are the AMQP list. |
| A96 | **a** | The case-study notes use MQTT up to the edge and HTTPS onward. |
| A97 | **b** | The selection depends on the application. There is no universal winner. |
| A98 | **b** | The numbers show how small the edge node is, so placement matters. |
| A99 | **b** | More sites, some of them physically exposed, means a larger attack surface. |
| A100 | **a** | Those six are the security requirements on the slide. |
| A101 | **a** | Local processing helps privacy, and the device still has to be protected. |
| A102 | **b** | The counts are the distributed-management problem. Kubernetes helps, and a scattered edge remains harder than one room of servers. |
| A103 | **b** | Local work continues. The stored result moves when the link returns. |
| A104 | **b** | Growth by adding sites and devices is the horizontal-scale requirement. |
| A105 | **a** | Containers help portability. They do not abolish hardware differences. |
| A106 | **b** | About 1 GB/s cannot be the upload plan. Filter and forward events. |
| A107 | **a** | Backup, failover, redundancy, and recovery. |
| A108 | **b** | Each place trades delay, privacy, power, and bandwidth differently. |
| A109 | **b** | Many sites mean hardware, power, cooling, security, updates, and people. |
| A110 | **a** | The mine states those challenges almost sentence by sentence. |
| A111 | **b** | Each challenge is paired with the remedy in the published answer. |
| A112 | **a** | Safety and driving decisions cannot wait half an hour. |
| A113 | **b** | Archives, large analysis, reports, and a non-urgent model update can wait, then synchronise. |

---

# Answers — Unit 4

| Q | Answer | Why this is the best option |
|---|---|---|
| B1 | **b** | Split the job and run the pieces at the same time. The aim is a shorter run. |
| B2 | **b** | Divide, distribute, execute together, combine. |
| B3 | **b** | One piece at a time, simpler, and less able to grow. |
| B4 | **a** | Same operation, different blocks of the data set. |
| B5 | **b** | Different analyses at the same time. |
| B6 | **a** | Data is what gets split in data parallelism. Tasks are what get split in task parallelism. |
| B7 | **a** | Speed, large sets, extra nodes, idle machines, and throughput. Exact linear speedup is not promised. |
| B8 | **a** | The combine step waits. That wait is synchronisation. |
| B9 | **a** | Time spent talking between processors is communication overhead. |
| B10 | **b** | 70% on one node is the imbalance picture. The repaired picture is 25% each. |
| B11 | **a** | A task that needs another task’s output is a dependency, and it is harder to run side by side. |
| B12 | **a** | A dead node requires recovery or recomputation. |
| B13 | **b** | Sequential time over parallel time. |
| B14 | **b** | 100 / 30 is about 3.33. The missing 0.67 is overhead, not a rounding error to 4. Inverting the fraction gives 0.30. |
| B15 | **a** | Equal chunks of one large set are data parallelism. |
| B16 | **a** | A slow node is imbalance. A dead node is fault tolerance. The organising model for the whole job is MapReduce. |
| B17 | **b** | MapReduce is the model named for this batch. |
| B18 | **b** | Shuffle and sort sit between the two functions. |
| B19 | **a** | Input, map, pairs, group and sort, reduce, output. |
| B20 | **a** | Key and value are the record the stages exchange. |
| B21 | **a** | Each machine becomes a category and a count of one. |
| B22 | **b** | The example keeps every 1 and groups them. The reducer needs that list. |
| B23 | **a** | Three normal machines and two faults. |
| B24 | **a** | The combiner is optional. It speeds the shuffle. The result does not depend on it being present. |
| B25 | **a** | `(k, v)` in, `(k', v')` out. |
| B26 | **a** | The reducer receives the key and the array of values. |
| B27 | **b** | The word Cloud appears once in each sentence. |
| B28 | **a** | `useful` appears once. `computing` appears twice. |
| B29 | **b** | Input, split, mapper, shuffle, sort, reducer, output. |
| B30 | **a** | The mapper emits pairs from input splits, in parallel. |
| B31 | **a** | Different keys can be reduced in parallel after they have been grouped. |
| B32 | **a** | Large data, parallel nodes, and a programmer who writes Map and Reduce rather than the whole distributed engine. Failures can be re-executed. |
| B33 | **b** | Millisecond response, heavy shuffle and disk traffic, and repeated iterations are the stated limits. |
| B34 | **a** | Batch is a collected job. A stream is handled as it arrives. MapReduce belongs to the batch side. |
| B35 | **a** | Keeping the computation near the data avoids moving the data. |
| B36 | **b** | A millisecond stop is local analytics. A billion historical records are a MapReduce batch. |
| B37 | **a** | The decision is made near the source. The raw flood does not have to arrive first. |
| B38 | **a** | Volume, delay, bandwidth, a fragile link, privacy, and a local decision. |
| B39 | **a** | That is the completed comparison table. |
| B40 | **a** | Immediate and local on the edge. History, training, and cross-site work in the cloud. |
| B41 | **a** | The ATM acts on the image locally, then tells the bank. |
| B42 | **a** | The repair is prompted by the approaching failure, not by the breakdown itself. |
| B43 | **a** | There is no time to upload before acting. |
| B44 | **a** | Those three examples are the method table. |
| B45 | **a** | A threshold is a known limit. An anomaly is an unusual pattern. |
| B46 | **a** | Stop the machine locally. |
| B47 | **a** | Many readings become one summary. |
| B48 | **a** | The Python list on the tools slide. |
| B49 | **b** | Spark fits an edge server. It is too heavy for a tiny device. |
| B50 | **a** | A visual flow editor, not a protocol and not an analytics algorithm. |
| B51 | **b** | MQTT transports. The threshold is the analysis. |
| B52 | **a** | OpenCV on the edge computer is the image path. |
| B53 | **a** | The layer-to-tool table. |
| B54 | **a** | The check and the alert are local. |
| B55 | **a** | Summaries and events, not the raw stream. |
| B56 | **a** | Continue, buffer, synchronise. |
| B57 | **a** | Delay, bandwidth, privacy, and survival of a lost link. |
| B58 | **b** | Sensors and endpoints, devices, gateways, servers, cloud. |
| B59 | **a** | Measuring is the sensor. Participating in the exchange is the endpoint. A camera can be an endpoint. |
| B60 | **b** | Local compute beside the source. |
| B61 | **a** | The critical value is the event. The normal run can be summarised. |
| B62 | **a** | Connect, translate, aggregate, filter, secure, forward. |
| B63 | **a** | Those four networks meet at the gateway. |
| B64 | **a** | A plain IoT gateway connects. An edge gateway can also analyse before it sends. |
| B65 | **a** | Vision, many applications, a database, and containers need the larger machine. |
| B66 | **a** | Multi-signal analysis, inference, recent history, and a local alert. |
| B67 | **a** | The management list from registration through retirement. |
| B68 | **a** | Version, staged rollout, rollback, and a check. A tour of a thousand devices is what management avoids. |
| B69 | **a** | Three different faults, three different responses, all from the management slides. |
| B70 | **b** | Deploy through retire, in that order. |
| B71 | **a** | Translate and gather, versus heavy local analytics. |
| B72 | **a** | Each verb is the main job of the next box in the architecture. |
| B73 | **b** | Four readings are under 80. The 92 must be reported as a fault. The raw five are not five emergency uploads. |
| B74 | **a** | Protocol translation to one format is the gateway’s answer to mixed machines. |
| B75 | **b** | Average, minimum, maximum, and faults replace one hundred separate uploads. |
| B76 | **a** | Summary, fault record, and a later synchronisation. |
| B77 | **b** | Each lower layer keeps its own job. The cloud catches up afterwards. |
| B78 | **b** | Intelligent processing is not a ban on sending. |
| B79 | **b** | Industry, machines, and continuous safe operation. |
| B80 | **b** | Purpose decides. The sensor chip does not. |
| B81 | **a** | The consequence of failure is the difference the table stresses. |
| B82 | **a** | Bearing, imbalance, alignment, and wear are the vibration uses. |
| B83 | **a** | Industrial sensing often meets a PLC before it meets a cloud API. |
| B84 | **a** | The PLC controls. The edge analyses. |
| B85 | **a** | Field protocol in, MQTT out. |
| B86 | **a** | The OPC UA feature list. Modbus is the other description. |
| B87 | **a** | Master requests, slave replies, often on older equipment. |
| B88 | **a** | Normal, warning, critical, raised locally. |
| B89 | **a** | Odd behaviour is the clue that maintenance should happen before the break. |
| B90 | **a** | A calendar can be both too early and too late. |
| B91 | **a** | Continuous condition, then an alert before the failure. |
| B92 | **a** | Train in the cloud, infer at the edge, learn again from the events. |
| B93 | **a** | Identity, permission, encryption, updates, and monitoring. |
| B94 | **a** | Home and personal devices on one side. Plant and production on the other. |
| B95 | **b** | A home garden is IoT. A municipal treatment plant is IIoT. |
| B96 | **a** | Watching people in a cafeteria is IoT. Inspecting products on the line is IIoT. |
| B97 | **a** | Lock and driver alert are personal. A PLC and a turbine under maintenance are industrial. |
| B98 | **a** | House and streetlight are IoT. Power-plant steam and a pharmaceutical plant are IIoT. |
| B99 | **a** | The closing notes split the protocols that way. |
| B100 | **a** | Same idea of “a sensor on a network”, two different purposes. |

---

## If you only revise one page

| You are asked… | The best short answer |
|---|---|
| Why edge exists | Delay, congestion, bandwidth, and dependence on the internet |
| Who decides now | The edge, close to the device |
| Who coordinates a city or a region | Fog / cloudlet / regional centre |
| Who keeps ten years and trains the model | The cloud |
| Container or virtual machine on a small node | Container: shared operating system, fast, light |
| Docker or Kubernetes | Docker runs a container. Kubernetes runs many, across nodes |
| SDN planes | Control decides. Data forwards. The controller can be a single point of failure |
| Popular film near the user | CDN. First miss fills the cache. The next request hits |
| Cloud unreachable on a disaster site | Mobile data centre |
| Small factory readings | MQTT to the edge. HTTPS onward |
| Tiny battery sensor on a bad link | CoAP, over UDP |
| Live dashboard | WebSocket |
| Enterprise queue | AMQP |
| Four processors, 100 s down to 30 s | Speedup about 3.33, not 4 |
| Same average on different blocks | Data parallelism |
| Temperature and vibration at the same time | Task parallelism |
| Billion stored records | MapReduce: map to pairs, group by key, reduce. Combiner is optional |
| Stop the machine this instant | Edge threshold or local inference, not MapReduce |
| Mixed industrial protocols | Gateway translates. Edge server analyses. PLC controls |
| Home garden or water plant | IoT, then IIoT. The purpose decides |
