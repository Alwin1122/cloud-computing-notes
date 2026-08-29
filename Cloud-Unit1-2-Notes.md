# Cloud Computing — Unit 1 & Unit 2 Essential Notes

Exam-ready notes from the lecture PDFs. Every topic is explained: what it is, how it works, why it matters, plus one example.

---

## Table of Contents

**Unit 1**

1. [Roots of Cloud Computing](#1-roots-of-cloud-computing)
2. [Characteristics of Cloud Computing](#2-characteristics-of-cloud-computing)
3. [Service Models](#3-service-models)
4. [Deployment Models](#4-deployment-models)
5. [Challenges of Cloud Computing](#5-challenges-of-cloud-computing)
6. [Service Level Agreement (SLA)](#6-service-level-agreement-sla)
7. [Microservices](#7-microservices)

**Unit 2**

8. [Virtualization and Applications](#8-virtualization-and-applications)
9. [Types of Hypervisors](#9-types-of-hypervisors)
10. [Types of Virtualization](#10-types-of-virtualization)
11. [VM Provisioning and Manageability](#11-vm-provisioning-and-manageability)
12. [VM Migration](#12-vm-migration)

---

# UNIT 1

## 1. Roots of Cloud Computing

Cloud computing did not appear suddenly. It grew from older ways of sharing computers, paying only for use, and hiding hardware behind software.

**Traditional computing:** Each organization bought its own servers, storage, network gear, and software licenses. Problems: high cost, servers sitting idle most of the day, hard maintenance, and poor scalability. Classic question: why buy 100 servers if only 20 are busy?

### 1.1 Mainframe vs Client–Server

| Feature | Mainframe | Client–Server |
|---|---|---|
| Processing | All work on one central machine; terminals only display | Work is shared: clients handle UI, servers handle data and logic |
| User devices | Dumb terminals | PCs, laptops, phones |
| Scaling | Scale-up (make the central machine bigger) | Scale-out (add more servers) |
| Reliability | Extremely high; built for zero downtime | Depends on the network |
| Typical use | Banking, insurance, airlines | LANs, websites, enterprise email |
| Cost | Very high setup and maintenance | Cheaper commodity hardware |

### 1.2 Distributed Computing

Many computers work together on one problem. They share resources, talk over a network, and split the work. Example: a Google search uses thousands of machines, then combines the results.

### 1.3 Cluster Computing

A cluster is a set of **similar** machines (same hardware/OS), usually in one building or rack, managed as **one system** by a central cluster manager. Goal: high performance, parallel work, and failover (if one node dies, another takes over).

| | Cluster | Distributed |
|---|---|---|
| Architecture | Nodes act as one system | Nodes stay individual systems that cooperate |
| Hardware/OS | Homogeneous | Often heterogeneous |
| Location | Same building/rack | Can be worldwide |
| Goal | Speed and high availability | Resource sharing and large split tasks |
| Control | One central manager | Loose / no single controller |

### 1.4 Parallel Computing

Two or more processors (CPU cores, or GPUs) work on the **same** problem at the same time. A large job is split into smaller pieces that run together.

- **OpenMP** — shared-memory parallelism in C/C++/Fortran
- **CUDA** — NVIDIA GPU parallel computing

| | Parallel | Distributed |
|---|---|---|
| Structure | Tightly coupled processors in one machine | Separate machines on a network |
| Memory | Often shared memory | Each machine has its own memory; they pass messages |
| Goal | Speed | Scale + fault tolerance |
| Communication | Fast internal buses | Network protocols |
| Use | 3D rendering, weather models, AI | Google Search, blockchain, cloud |

### 1.5 Grid Computing

A special kind of distributed computing: **different organizations** share idle computers across administrative and geographic boundaries to solve a huge problem. All grid computing is distributed computing, but not all distributed computing is a grid.

Users typically do **not** pay per use; they collaborate and share unused capacity.

**Easy analogy**

- Same-class project team = cluster (same group, same place)
- Four campus PCs each processing 250,000 student records = distributed
- PSG + MIT + Oxford + Tokyo sharing idle CPUs for telescope data = grid

### 1.6 Utility Computing

Like electricity: you do not buy the power plant; you use power and pay for what you consume. You rent CPU, storage, software when needed.

Example: a company needs 100 GB + 4 CPUs for 10 days. It rents them instead of buying hardware.

Utility computing answered **“How do I pay?”** (pay-per-use). It lacked automation, elasticity, and a standard service catalog.

**Cloud ≈ utility computing + virtualization + internet access + automation + scalability.**

Cloud answers **“How do I get the service?”** (on-demand delivery), not only billing.

### 1.7 SOA, Web Services, Web 2.0, Mashups

These ideas taught the cloud to be built as reusable internet services.

**SOA (Service-Oriented Architecture):** Break a large app into independent, reusable services (auth, payment, email, inventory). Cloud platforms are SOA at scale: compute, storage, database as separate services.

**Web services:** Software published on the internet that talks through standard messages (historically XML).

**Web 2.0 (social web):** The internet became read–write. Users create and share content.

| | Web 1.0 | Web 2.0 |
|---|---|---|
| User | Passive viewer | Active creator |
| Content | Static pages | Dynamic, user-driven |
| Interaction | One-way | Two-way |
| Examples | Reading, basic email | Social media, streaming, blogs, wikis |

**Mashup:** One app built by combining other services. A food-delivery app = Google Maps + payment gateway + restaurant database.

Chain: SOA splits apps into services → web services let them talk → Web 2.0 creates huge demand → mashups combine online services.

### 1.8 Hardware Virtualization

One physical machine runs several isolated virtual computers (VMs). Each VM gets its own CPU, memory, and disk. A **hypervisor** (Virtual Machine Monitor) sits between hardware and VMs.

Without virtualization: one physical server → one OS → apps.  
With virtualization: one physical server → hypervisor → VM1 (Windows), VM2 (Linux), VM3 (Ubuntu).

**Three techniques**

1. **Full virtualization** — Hardware is fully simulated. Guest OS does not know it is virtual. No OS change needed. Example: early VMware Workstation. Performance: medium.
2. **Paravirtualization (PV)** — Guest OS is modified and talks to the hypervisor with **hypercalls** (`guest OS → hypercalls → hypervisor → hardware`). Guest knows it is virtual. Faster. Example: Xen.
3. **Hardware-assisted virtualization** — CPU has virtualization extensions (Intel VT-x, AMD-V). Little or no OS change, very high performance. Examples: KVM, modern VMware, Hyper-V.

| Feature | Full | Para | Hardware-assisted |
|---|---|---|---|
| OS modification | No | Yes | No |
| Guest aware it is a VM? | No | Yes | No |
| Extra CPU support | No | No | Yes (VT-x / AMD-V) |
| Performance | Medium | High | Very high |
| Example | Early VMware | Xen | KVM, modern VMware, Hyper-V |

**Type 1 hypervisor (bare-metal):** Installed directly on hardware. Examples: VMware ESXi, Microsoft Hyper-V, KVM.

**Type 2 hypervisor (hosted):** Installed on a host OS. Example: Oracle VirtualBox (Windows + VirtualBox + Ubuntu VM = Type 2).

**VMware ESXi:** Type-1, enterprise, live migration (vMotion), high availability. Easy and mature, but licensed.

**Xen:** Open-source Type-1. Uses a special control VM called **Domain-0 (Dom0)** to manage guests. Supports para and hardware-assisted virtualization. Efficient, but more complex.

**KVM (Kernel-based Virtual Machine):** A Linux-kernel module that turns Linux itself into a hypervisor. Open source, uses VT-x/AMD-V, common in clouds. Needs a Linux host.

| | ESXi | Xen | KVM |
|---|---|---|---|
| Type | Type-1 | Type-1 | Type-1 (Linux kernel) |
| Open source | No | Yes | Yes |
| Needs Linux host | No | No | Yes |
| Special control VM | No | Yes (Dom0) | No |
| Typical use | Enterprise data centers | Cloud and research | Cloud platforms |

**Virtual appliance:** A ready-made VM with OS + apps + settings already configured. Download → import into hypervisor → use. Saves install/config time.

**OVF (Open Virtualization Format):** Open DMTF standard for packaging VMs/appliances so they can move across hypervisors. Needed because formats differ (VMware `.vmdk`, VirtualBox `.vdi`, Hyper-V `.vhdx`). Benefits: vendor-independent, portable, interoperable.

### 1.9 Autonomic Computing

Systems that **manage themselves** with little human help (like a self-driving car for IT).

Traditional: problem → admin notices → admin fixes.  
Autonomic: problem → system detects → system fixes.

Cloud uses this constantly:

- **Auto scaling** — 100 users → 10,000 users → extra servers appear
- **Self-healing** — a VM dies → cloud starts a replacement
- **Load balancing** — high load → traffic is spread automatically

**Evolution toward cloud:** distributed → grid → utility → virtualization → autonomic → cloud.

---

## 2. Characteristics of Cloud Computing

NIST defines **five essential** characteristics. Lectures also mention related practical traits.

### 2.1 Resource Pooling (and multi-tenancy)

The provider pools CPU, RAM, storage, and network and serves many customers from the same pool (**multi-tenant**). Each customer is **logically isolated** even though the hardware is shared.

Example: thousands of AWS customers share the same data centers. Benefit: better utilization and lower cost.

### 2.2 On-Demand Self-Service

You get resources **when you ask**, **without calling an admin**.

Traditional IT: raise a ticket → wait for approval → wait days.  
Cloud: open a portal/API → launch a VM → ready in minutes.

Example: AWS EC2 — log in, pick OS, pick CPU/RAM, click Launch.

### 2.3 Broad Network Access (large network access)

Services are reached over the internet from many devices (laptop, tablet, phone, browser), from anywhere.

Example: a professor writes notes on a laptop, reviews them on a tablet, and opens them on a phone.

### 2.4 Rapid Elasticity

Capacity grows and shrinks automatically with demand. Scale **up** when busy, **down** when quiet. You do not keep paying for unused machines.

Example: an e-commerce site gets 20,000 festival visitors; extra VMs appear, then disappear after the sale.

### 2.5 Measured Service (and pay-as-you-go)

Usage is metered (CPU hours, storage, bandwidth) and billed. Pay only for what you used. This is also why cloud is economical: no huge unused hardware bill.

Example: Azure bills monthly by CPU hours, storage, and network.

### 2.6 Other lecture traits

- **Easy maintenance / high availability** — provider maintains servers; downtime is low
- **Automatic / self-managing** — metering, self-provisioning, reports for both host and customer
- **Security** — snapshots and protected storage so data is not lost if one server fails
- **Economical** — provider buys capacity once and shares it; customers pay monthly/yearly for use

### Quick map (exam)

| Clue | Characteristic |
|---|---|
| Launch a VM without calling support | On-demand self-service |
| Phone / laptop / anywhere / internet | Broad network access |
| Shared hardware, isolated tenants | Resource pooling |
| Auto add/remove VMs with traffic | Rapid elasticity |
| Bill by actual usage | Measured service |

---

## 3. Service Models

A **service model** says how much the provider manages and how much control you keep.

The three primary models: **IaaS, PaaS, SaaS**.

### 3.1 IaaS — Infrastructure as a Service

You rent **virtual machines, storage, and networks** over the internet.

- **Provider:** physical servers, storage, networking, virtualization
- **You:** OS, middleware, runtime, applications, data

Use when you need a VM and full OS control. Example: rent AWS EC2, install Ubuntu + Apache + MySQL + PHP yourself.

### 3.2 PaaS — Platform as a Service

You get a **ready platform** to build and deploy apps. You write code; the provider runs the platform.

- **Provider:** infrastructure, virtualization, OS, runtime, middleware
- **You:** application + data

Use when you want to deploy code quickly. Example: Google App Engine or Azure App Service for a placement portal — you write the app; they handle OS updates, web server, scaling.

### 3.3 SaaS — Software as a Service

Ready-to-use software over the internet. You just log in.

- **Provider:** everything
- **You:** usage, settings, and the data you enter

Use when you need the software, not a development platform. Example: Gmail, Google Docs, Google Meet (Google Workspace).

### Who manages what

CP = Cloud Provider, U = User

| Layer | SaaS | PaaS | IaaS |
|---|---|---|---|
| Application | CP | U | U |
| Data | CP / U (your data) | U | U |
| Runtime | CP | CP | U |
| Middleware | CP | CP | U |
| Operating system | CP | CP | U |
| Virtualization | CP | CP | CP |
| Servers | CP | CP | CP |
| Storage | CP | CP | CP |
| Networking | CP | CP | CP |

### Fast pick

| Need | Model |
|---|---|
| VM + full OS control | IaaS |
| Deploy my code, skip server admin | PaaS |
| Just use email / docs / ready software | SaaS |

---

## 4. Deployment Models

A **deployment model** says **where** the cloud lives and **who** can use it.

### 4.1 Public Cloud (Internet Cloud)

A third party (AWS, Azure, Google Cloud) owns and runs the hardware. Resources are shared among many tenants and delivered over the public internet.

**Advantages:** pay-as-you-go (no big hardware purchase), fast scale, no patching/maintenance for you.  
**Disadvantages:** shared hardware raises security questions; bills can explode if you do not watch usage.

**Best for:** websites with unpredictable traffic, Dev/Test, offsite backups, seasonal e-commerce. Typical users: startups, small companies, student projects.

### 4.2 Private Cloud (Enterprise Cloud)

Infrastructure is **dedicated to one organization**.

**Types**

1. **On-premises (internal) private cloud** — in your own data center. You own and manage everything. Max control and security; high capital cost; needs skilled admins. Example: a college cloud inside campus.
2. **Hosted (external) private cloud** — dedicated servers sit in a **provider** data center. You still do day-to-day app/OS work. Less physical control; you depend on the provider. Example: a bank rents dedicated servers.
3. **Managed private cloud** — dedicated/owned for you, but a third party handles monitoring, security, backup, updates, provisioning. You focus on the business.
4. **VPC (Virtual Private Cloud)** — a **logically isolated** slice of a **public** cloud. Hardware is still shared; your network (IPs, subnets, firewalls) looks private. Cheaper and easy to scale. Example: isolated AWS network with public/private subnets.

| Type | Location | Ownership | Management |
|---|---|---|---|
| On-premises | Org data center | Organization | Organization |
| Hosted | Provider data center | Dedicated to org | Organization (day-to-day) |
| Managed | Org or provider | Org or provider | Third party |
| VPC | Public cloud | Logically dedicated | Cloud provider + you (network rules) |

**Hosted vs managed (exam):** in hosted, you still do OS/app/day-to-day management; in managed, the provider does monitoring, OS updates, and daily cloud ops.

Private cloud typical users: banks, defense, healthcare (sensitive data).

### 4.3 Community Cloud

Shared by **several organizations with the same needs** (same laws, same mission). Cost is shared; policies are common. Less flexible than a private cloud. Example: hospitals sharing one cloud because of healthcare rules; several colleges under one university sharing exam/library systems.

### 4.4 Hybrid Cloud

**Two or more** models used together (usually private + public), connected so work can move.

Example: a bank keeps customer records on a private cloud, but **bursts** report generation to Azure at year-end.

**Advantages:** flexibility, extra scale, cost control (keep secrets private, rent extra capacity).  
**Disadvantage:** harder to manage.

Most enterprises use hybrid to balance security and scale.

### 4.5 Multi-Cloud

Using **two or more different providers** (not the same as hybrid). Hybrid = mix of *deployment types*. Multi-cloud = mix of *vendors*.

Example: AWS for VMs, Azure for AI, Google Cloud for analytics. Reasons: best tool for each job, less vendor lock-in, better reliability.

### Comparison

| Model | Ownership | Who can access | Cost | Security |
|---|---|---|---|---|
| Public | Cloud provider | Public internet | Low | Moderate |
| Private | One organization | Internal users | High | High |
| Community | Several orgs | That community | Medium | High |
| Hybrid | Mix | Mix | Medium | High |

### Scenario → model (exam)

| Scenario | Model |
|---|---|
| College builds campus cloud for staff/students only | Private (on-premises) |
| Netflix on AWS for millions of users | Public |
| Patient records private; Azure only at peak | Hybrid |
| Government departments share one secure cloud | Community |
| Uses AWS + Azure + GCP at once | Multi-cloud |
| Isolated AWS network, own IPs/subnets/firewalls | VPC |
| Dedicated servers at provider, hospital manages daily | Hosted private |
| Own private cloud, vendor does backups/patches | Managed private |

---

## 5. Challenges of Cloud Computing

### 5.1 Security and Privacy

Data sits on **someone else’s** servers. Questions: is it safe, who can see it, is sensitive data protected? Legal/regulatory rules also apply.

**Data breaches:** unauthorized people reach confidential cloud data. Consequences: money loss, reputation damage, lawsuits.

### 5.2 Vendor Lock-In (Data Lock-In)

You become so tied to one provider’s APIs, storage, and tools that moving is slow, expensive, and painful.

**How to reduce it**

- **Containers + Kubernetes** — pack apps so they run on many clouds
- **Open standards** — open-source DBs, common APIs and data formats
- **CCIF (Cloud Computing Interoperability Forum)** — vendor-neutral group (Intel, Sun, Cisco, etc.) for common frameworks
- **UCI (Unified Cloud Interface)** — one dashboard/abstraction to manage many clouds
- **OVF** — portable VM/appliance packaging across hypervisors

### 5.3 Availability and Downtime

No internet → no cloud. Outages stop work, lose revenue, and damage reputation. Cloud is **not** 100% uptime. Providers promise SLAs, typically **99.9% to 99.99%**.

### 5.4 Performance and Latency

Data must travel the network. Games and industrial control cannot tolerate delay. This is why **edge computing** exists: process data closer to the user/device.

### 5.5 Compliance and Legal Issues

Countries have different rules about where data may live and who may see it. Breaking them means fines.

### 5.6 Resource and Cost Management

Large orgs run thousands of VMs, containers, DBs, and networks. Unused resources still get billed (**cost management**). Managing all of this dynamically is hard.

### 5.7 Data Migration

Moving huge existing datasets to the cloud takes time, needs bandwidth, and risks data loss or downtime.

### Challenge summary

| Challenge | Meaning |
|---|---|
| Security & privacy | Protect data on third-party servers |
| Data breaches | Unauthorized access |
| Vendor lock-in | Hard to switch providers |
| Availability | Outages and failures |
| Internet dependency | Needs a reliable network |
| Latency | Network delay hurts real-time work |
| Compliance | Laws and industry rules |
| Cost management | Unused resources waste money |
| Resource management | Too many cloud objects to run well |
| Data migration | Hard to move existing data in |

### 5.8 Security Risks and Threats

1. **Data breaches** — stolen confidential data
2. **Data loss** — deletion, disk failure, or attack wipes data
3. **Account hijacking** — stolen user credentials
4. **Insecure APIs** — weak APIs that attackers exploit
5. **Insider threats** — staff/admins/contractors abuse access
6. **DoS / DDoS** — flood the service so real users cannot use it
7. **Multi-tenancy risks** — weak isolation leaks data to another tenant
8. **Misconfiguration** — wrong settings leave resources open
9. **Malware and ransomware** — malware on cloud systems
10. **Compliance violations** — fail legal/industry rules → fines

---

## 6. Service Level Agreement (SLA)

An **SLA** is a formal contract between provider and customer. It states the expected service: availability, performance, duties, and **penalties** if the provider fails.

### 6.1 Components of an SLA

1. **Service description** — what is being sold (VMs, storage, databases)
2. **Availability (uptime)** — how often it must be up (e.g. 99.9%)
3. **Performance metrics** — response time, latency, throughput
4. **Security requirements** — encryption, authentication, access control
5. **Support services** — hours, response time, resolution time (e.g. critical issues in 2 hours)
6. **Backup and disaster recovery** — backup frequency, how restore works, recovery time
7. **Responsibilities**
   - Provider: keep infrastructure up, meet availability, take backups
   - Customer: manage the app, protect passwords, follow security rules
8. **Penalties and compensation** — if target is missed (promised 99.99%, delivered 99.5%), customer may get **service credits**, refunds, or other compensation

### 6.2 Types of SLA

1. **Customer-based SLA** — written for **one** customer; customized to that business
2. **Service-based SLA** — one SLA for **one service**, same for every customer of that service
3. **Multi-level SLA** — stacked layers in one agreement:
   - **Corporate** — company-wide rules for all customers
   - **Customer** — that customer’s extra needs
   - **Service** — technical numbers for each service

### 6.3 OLA vs Underpinning Contract

These are **not** the customer-facing SLA, but they help the provider **meet** the SLA.

**OLA (Operational Level Agreement):** Internal deal **inside** the provider. Example: infra team promises server uptime; support team promises ticket times. OLAs make internal teams line up with the customer SLA.

**UC (Underpinning Contract):** Deal between the provider and an **external vendor** (network ISP, backup vendor). The vendor must hit numbers that support the main SLA. Example: hosting provider + network provider both have contracts so a weak third party does not break the customer promise.

```
Customer SLA
    ↑ supported by
Internal OLA (provider teams)
    ↑ supported by
Underpinning Contracts (third-party vendors)
```

### Exam sense

- Hospital / banking: pick the **highest availability + 24×7 support + backups + service credits** (e.g. 99.99% over 99.5% with email-only support).
- If outages exceed the promised monthly uptime, the **availability** clause is broken; claim **credits/compensation**.
- SLA matters for business-critical apps because downtime = money and safety risk.

---

## 7. Microservices

### 7.1 Monolithic Architecture

All features live in **one** codebase and are deployed as **one** unit.

Example e-commerce monolith: user + catalog + cart + payment + orders in one app.

**Benefits:** easier to start, faster first version, in-process calls (fast), simple to monitor.

**Problems:** cannot scale one piece alone; a small change forces a full redeploy; one bug can take down everything; one tech stack for all; teams step on each other; swapping a library can force a huge rewrite.

### 7.2 Microservices Architecture

The app is a set of **small, independent, loosely coupled** services. Each does **one** business job and talks to others through **APIs**.

Same e-commerce as separate services: User, Product, Cart, Payment, Order — each can run, deploy, and scale alone.

**Characteristics**

- Small and focused
- Independent deployment
- Loose coupling via APIs
- Per-service scaling
- Technology independence (different languages/DBs per service)

**Benefits:** scale only the busy service; pick the best stack per service; change one module without touching all; faults stay in one service; each service can have its own security.

**Drawbacks:** harder to manage many moving parts and data consistency; network calls add latency; higher design/DevOps cost; end-to-end testing is harder.

### 7.3 API Gateway

A **single front door** for clients. The client does not call every service; it calls the gateway, which routes the request.

**Jobs:** routing, auth, load balancing, rate limiting, logging, combining several service replies into one response.

**Examples:** Spring Cloud Gateway, Amazon API Gateway, Kong, NGINX.

### 7.4 Docker and Kubernetes

Typical cloud path:

Application → split into microservices → each packed in a **container** → **Docker** runs containers → **Kubernetes** deploys, scales, and heals them.

| Layer | Examples |
|---|---|
| Development | Spring Boot, Node.js, Flask, FastAPI |
| Containers | Docker, Podman |
| Runtime | Docker Engine, containerd |
| Registry | Docker Hub, Amazon ECR |
| API gateway | Kong, NGINX |
| Orchestration | Kubernetes, Docker Swarm |
| Cloud | AWS, Azure, GCP |

**Orchestration** automatically deploys, scales, networks, and recovers services so the whole app stays up.

### Monolith vs microservices

| | Monolith | Microservices |
|---|---|---|
| Shape | One application | Many small services |
| Deploy | One deploy | Independent deploys |
| Scale | Scale the whole app | Scale one service |
| Coupling | Tight | Loose (APIs) |
| Tech | One stack | Mix of stacks |

### SOA vs microservices (exam)

SOA also splits an app into services, but those services are often **larger, shared enterprise services** (sometimes SOAP/XML, shared databases). **Microservices** are smaller, independently deployable, usually REST/HTTP, and each service typically **owns its own data**. Cloud-native apps lean microservices + containers.

---

# UNIT 2

## 8. Virtualization and Applications

### 8.1 Need for Virtualization

Old rule: **one application per physical server**. Result: CPU often only 10–20% used, high hardware/power/space cost, more maintenance.

Example: web server, database, and mail each on their own box.

### 8.2 What Virtualization Is

Virtualization lets **one physical computer act as many independent computers**.

Key terms:

- **Host** — the physical server running a hypervisor
- **Host OS** — OS on the physical machine (Type 2 only)
- **Guest OS** — OS inside a VM
- **VM** — a software computer that behaves like a real one

Each VM has: **vCPU, virtual RAM, virtual disk, virtual NIC, guest OS, applications**.

Stack: App → Guest OS → Virtual hardware → **Hypervisor** → Physical hardware.

**VM traits:** own OS, isolated from other VMs, behaves like a PC, can be created/copied/deleted/migrated, shares real hardware through the hypervisor.

### 8.3 How It Works

The hypervisor splits real CPU, RAM, disk, and network among VMs.

**Before:** 3 apps → 3 physical servers.  
**After:** 1 physical server → hypervisor → VM1, VM2, VM3.

### 8.4 Advantages

Better hardware use, lower cost and power, faster deploy, easier scale, better disaster recovery, isolation (one crashed VM does not kill the others).

### 8.5 Applications of VMs

- **Server consolidation** — many VMs on fewer boxes
- **Cloud computing** — providers create VMs on demand for tenants
- **Dev/Test** — run Windows and Linux on one laptop
- **Multiple OSes** — run Linux on Windows without rebooting
- **Disaster recovery** — back up, clone, restore VMs quickly

**Virtualization vs VM:** virtualization is the *technique* (needs a hypervisor). A VM is the *result* (a virtual computer).

---

## 9. Types of Hypervisors

A **hypervisor** (VMM) creates and runs VMs. It sits between hardware and VMs so several OSes can share one machine.

### 9.1 Responsibilities

| Duty | Meaning |
|---|---|
| CPU scheduling | Share CPU among VMs |
| Memory management | Allocate RAM |
| Storage management | Manage virtual disks |
| Network management | Create virtual networks |
| VM / fault isolation | One VM crash or malware should not hit others |
| Resource allocation | Give hardware dynamically |

**Cloud advantages of hypervisors:** isolation, and **portable VMs** that are not glued to one physical box (easy local or remote move).

### 9.2 Type 1 — Bare-Metal

Installed **directly on hardware**. No host OS. High performance and security. Used in data centers and public clouds.

**Examples:** VMware ESXi, Microsoft Hyper-V, Xen, KVM.

**Pros:** efficient, low overhead, secure, many VMs.  
**Cons:** harder to install; needs dedicated hardware and skill.

### 9.3 Type 2 — Hosted

Installed **on top of** Windows, Linux, or macOS. Extra OS layer → more overhead, less performance. Fine for laptops, learning, and testing — **not** large data centers. A host-OS security hole can threaten every VM.

**Examples:** Oracle VirtualBox, VMware Workstation, VMware Fusion.

**Pros:** easy, no special hardware, great for students.  
**Cons:** slower, depends on host OS, not for production clouds.

### Comparison

| Feature | Type 1 | Type 2 |
|---|---|---|
| Install | On hardware | On a host OS |
| Host OS needed | No | Yes |
| Performance | High | Moderate |
| Security | Higher | Lower |
| Overhead | Low | Higher |
| Use | Data centers, cloud | PCs, testing, learning |
| Examples | ESXi, Hyper-V, Xen, KVM | VirtualBox, Workstation |

**Pick:** cloud provider installing ESXi on bare servers → Type 1. Developer installing VirtualBox on a Windows laptop → Type 2.

---

## 10. Types of Virtualization

Virtualization is not only servers. You can virtualize apps, networks, desktops, storage, and even data access.

### 10.1 Application Virtualization

The app runs in an isolated environment (often from a central server) and is **not installed** on each PC.

Without it: install MATLAB on 500 lab PCs; every update is 500 updates.  
With it: install once on a central server; students launch it from any lab PC.

**Advantages:** one deploy, fewer version conflicts (two Javas can coexist), central updates, better security (isolated), old apps can run on new OSes, less disk waste, faster onboarding, remote access, lower maintenance.

**Software:** Microsoft App-V, VMware ThinApp, Citrix Virtual Apps.

### 10.2 Network Virtualization

Create **many logical networks** on **one physical network**. Software makes vSwitches, virtual routers, virtual firewalls, virtual networks (e.g. VMware NSX, Open vSwitch).

Example: HR, Finance, R&D each get their own virtual network on the same cables — isolation, less traffic collision.

**Components**

- **vSwitch** — software switch connecting VMs
- **Virtual router** — routes between virtual networks
- **Virtual firewall** — blocks unwanted access
- **VLAN** — logically separate LANs on one physical net

**Advantages:** better use of links, isolation/security, faster setup, cloud-friendly. Traditional nets are hardware-bound and expensive to grow; virtual nets are software and easy to scale.

### 10.3 Desktop Virtualization (VDI)

The **whole desktop OS** lives on a central server. The user device only sends keyboard/mouse and shows the screen (thin client, laptop, tablet).

**Components:** host server, hypervisor, virtual desktop, client device.  
**Software:** Citrix Virtual Desktops, VMware Horizon.

**Pros:** install once, remote access, data stays on the server, backup the server only, any device.  
**Cons:** needs a good network and a strong server; setup cost is higher.

| | Desktop virtualization | Application virtualization |
|---|---|---|
| What is virtual | Whole desktop | One application |
| User gets | Full Windows/Linux desktop | Only that app |
| Runs | OS + apps | Just the app |

### 10.4 Storage Virtualization

Many physical disks are merged into **one logical pool**. Users see one volume, not Disk1/Disk2/Disk3.

Example: 2 TB + 3 TB + 5 TB → one 10 TB pool. Software (VMware vSAN, Ceph) places data and hides which disk it is on.

**Advantages:** use leftover space, manage one pool, add a disk and grow, stripe for speed, survive a disk with RAID/replication, central backup.

### 10.5 Server Virtualization

Split one physical server into many VMs, each with vCPU, RAM, disk, NIC, guest OS. This is the classic type used in clouds. Software: ESXi, Xen, KVM, Hyper-V.

| | Server virt. | Storage virt. |
|---|---|---|
| Virtualizes | Servers | Disks/arrays |
| Result | VMs | One logical storage pool |
| Uses | CPU and memory | Disks |

### 10.6 Data Virtualization

A **logical layer** lets you query many databases **without copying** the data. The data stays where it is; the layer combines results in real time.

Example: student + library + exam + placement DBs. Principal asks “full student details”; one query hits the virtual layer; it fetches from all four. Tools: Denodo, IBM Cloud Pak for Data.

**Advantages:** one view, no duplicate copies, live data, faster app development.

| | Storage virtualization | Data virtualization |
|---|---|---|
| Data stays in place? | Yes (on disks) | Yes (in original DBs) |
| Copied? | No | No |
| What is virtual | Storage devices | Data access |
| User sees | One volume | One logical database view |

### Quick software list

| Type | Common software |
|---|---|
| Application | App-V, ThinApp, Citrix Virtual Apps |
| Network | VMware NSX, Open vSwitch |
| Server | ESXi, Xen, KVM, Hyper-V |
| Desktop | Citrix Virtual Desktops, VMware Horizon |
| Storage | VMware vSAN, Ceph |
| Data | Denodo, IBM Cloud Pak for Data |

### Requirement → type (exam)

| Need | Type |
|---|---|
| MATLAB/AutoCAD from any PC, no local install | Application |
| Faculty desktop from home | Desktop |
| Fewer physical servers, many OSes | Server |
| One view of many DBs, no copy | Data |
| Combine department disks into one pool | Storage |
| Isolate student/faculty/admin traffic on one campus net | Network |

---

## 11. VM Provisioning and Manageability

### 11.1 What Provisioning Is

**VM provisioning** = create, configure, and hand over a VM with the right CPU, RAM, disk, network, OS, and apps.

Example: new developer needs Ubuntu, 4 GB RAM, 2 CPUs, 50 GB, Python → admin (or automation) builds that VM.

### 11.2 Provisioning steps

1. User request (OS + sizes)
2. Hypervisor allocates CPU, RAM, storage, network
3. Create the VM (VMware, Hyper-V, KVM, VirtualBox)
4. Install OS (Ubuntu, Windows Server, CentOS)
5. Configure IP, hostname, firewall, users
6. Install apps (Apache, MySQL, Java, Python)
7. VM ready

### 11.3 Provisioning methodologies (scaling)

- **Horizontal** — add **more VM instances** when load crosses a threshold (extra web servers for a busy site)
- **Vertical** — give the **same VM more** CPU/RAM/disk (often needs a reboot)
- **Hybrid** — e.g. scale web tier out (horizontal) and grow the database VM (vertical)

### 11.4 Types of provisioning

1. **Manual** — admin clicks through every step. Full control; slow, error-prone, does not scale. Good for 1–2 VMs, one-off student projects, or a highly custom research box (CUDA + TensorFlow + MATLAB).
2. **Automated** — tools/scripts build VMs on request. Fast, consistent, scalable. Needs upfront automation work. Used by clouds, large companies, VDI, disaster recovery.
3. **Template / clone (golden image)** — copy a master VM that already has OS + software. Example: 50 new engineers — first year 1 hour per VM by hand; next year clone a golden image in ~5 minutes.

| | Manual | Automated |
|---|---|---|
| Human effort | High | Low |
| Speed | Slow | Fast |
| Errors | More | Fewer |
| Scalability | Low | High |
| Best for | Small / custom | Cloud and data centers |

### 11.5 VM Manageability and Lifecycle

**Manageability** = monitor, secure, update, and optimize VMs for their whole life.

Lifecycle: **Create → Configure → Deploy → Monitor → Update → Backup → Migrate → Delete**

**Activities**

1. **Monitoring** — CPU, RAM, disk, network
2. **Resource management** — grow RAM 4→8 GB, CPU 2→4 cores when the VM is slow
3. **Security** — patches, OS updates, firewall, antivirus
4. **Backup** — regular copies of VM, apps, config
5. **Snapshots** — freeze state before a risky upgrade; roll back if it fails
6. **Migration** — move VM for maintenance, load balance, or disaster recovery
7. **Performance optimization** — tune CPU, memory, storage, network

Snapshot vs backup (exam): snapshot is a fast restore point (often on the same storage); backup is a durable copy for disasters.

### 11.6 Choosing virtualization software

| Software | Type | Notes |
|---|---|---|
| **Xen** | Type-1 | Open source; Dom0; para + hardware-assisted; live migration; public-cloud / research |
| **KVM** | Type-1 | Built into Linux; open source; pairs with OpenStack; private Linux clouds |
| **Hyper-V** | Type-1 | Microsoft; Active Directory / Windows Server shops |
| **VirtualBox** | Type-2 | Free, easy, snapshots; learning/testing; slower than Type-1 |
| **ESXi** | Type-1 | Enterprise data centers; vMotion, HA; licensed |

Team mapping from lectures: public-cloud Linux infra → **Xen**; Ubuntu + OpenStack private cloud → **KVM**; Windows enterprise → **Hyper-V**; students on laptops → **VirtualBox**.

---

## 12. VM Migration

**VM migration** moves a VM from a **source** physical host to a **destination** host **without changing** the guest OS, apps, or data.

### 12.1 Why migrate

Hardware maintenance without long outages, load balancing, better utilization, power saving (pack VMs onto fewer boxes), recover from failure, disaster recovery / business continuity.

Used in: cloud DCs, maintenance windows, load balance, DR, DC consolidation, greener computing.

Two main kinds: **cold** and **live**.

### 12.2 Cold Migration (Offline)

The VM is **powered off**, files are copied, then it is started on the new host.

Steps: running VM → shutdown (RAM and CPU state gone) → copy virtual disk + config → start on destination (OS boots again, apps restart).

**Copies:** virtual disk (OS + apps + data) and config. **Does not copy** RAM or CPU state (they are empty after shutdown). Shared storage is **not** required.

**Pros:** simple, no memory sync, lower failure risk.  
**Cons:** downtime; bad for 24×7 systems.

Example: migrate university ERP at midnight.

### 12.3 Live Migration (Online)

The VM stays **running**. Users see almost no pause (milliseconds to a few seconds). Typical in clouds (VMware vMotion, AWS/Azure maintenance).

Usually both hosts see the **same disk on shared storage (SAN/NAS)**, so only **RAM + CPU state** move, not the whole disk.

**Pros:** near-zero downtime, high availability, no user interrupt.  
**Cons:** more complex, needs a fast network, uses extra bandwidth.

| | Cold | Live |
|---|---|---|
| VM state | Powered off | Running |
| Downtime | High | Very low |
| Virtual disk | Copied | Usually stays on shared storage |
| Memory / CPU state | Not copied | Copied |
| Processes | Lost; restart | Preserved |
| Shared storage | Not required | Typically required |
| Complexity | Simple | Higher |
| Best for | Tests, planned night work | Production / cloud |

### 12.4 Dirty pages

While you copy RAM, the still-running VM keeps changing memory (logins, DB writes). Changed pages are **dirty pages**. If you copy RAM only once, the destination is stale. Pre-copy and post-copy solve this differently.

### 12.5 Pre-Copy

Copy **memory first**, while the VM still runs on the source. Recopy dirty pages in rounds. When few dirty pages remain: **pause briefly**, copy leftovers + CPU state, **resume on destination**.

**Pros:** tiny downtime; destination already has almost all RAM (safer if the network dies); default in VMware, KVM, Hyper-V, Xen.  
**Cons:** a write-heavy VM creates endless dirty pages → long migrate, more network use.

### 12.6 Post-Copy

**Pause first**, send **CPU state**, **start the VM on the destination immediately**, then pull RAM **on demand** when the VM page-faults.

**Pros:** each page sent once; less traffic; better when there are many dirty pages.  
**Cons:** if the network dies before all pages arrive, the VM can **crash** (some RAM still only on the source).

| | Pre-copy | Post-copy |
|---|---|---|
| Memory move | Before switch | After switch |
| VM starts on dest | After most RAM copied | Right after CPU state |
| Dirty pages | Recopied many times | Not recopied |
| Downtime | Very low | Very low |
| Network-fail risk | Low | High |
| Typical use | Most products | Research / special cases |

### 12.7 Hybrid

**Pre-copy** the hot/frequently used pages, transfer CPU state, start on destination, **post-copy** the rest on demand. Tries to get pre-copy reliability with post-copy speed.

Industry default is **pre-copy** because it is safer.

### 12.8 Live Migration over WAN

Inside one data center, live migrate uses a fast LAN. Clouds also move VMs **between cities** (Chennai → US) over a WAN for disaster or maintenance.

**Harder because:** limited bandwidth, high latency, must keep memory consistent while the VM still runs.

**Helps:** compress pages, **deduplicate** repeated blocks, **delta migration** (send only changes).

**Why do it:** disaster recovery, follow-the-sun (move the VM near active users — India launch, later shift toward Europe), business continuity, balance load across sites, pack servers at night to save power.

| | Local | WAN |
|---|---|---|
| Distance | Same DC | Different sites |
| Network | Fast LAN | WAN |
| Bandwidth | Very high | Limited |
| Latency | Low | High |
| Time | Short | Longer |
| Main pain | Resource placement | Bandwidth and delay |

**Exam pick:** cyclone warning, ERP must keep running across Chennai → Singapore, users still writing data, slow WAN → **live** (not cold); **hybrid** is often best (pre-copy hot pages, avoid post-copy crash if WAN drops). Never run the **same** VM on both hosts at once after a file copy — split-brain / data corruption.

---

## One-page exam checklist

**Unit 1**

- Evolution: traditional → mainframe / client–server → distributed → cluster → parallel → grid → utility → virtualization + autonomic → **cloud**
- Cloud ≈ utility + virtualization + internet + automation + scale
- NIST 5: on-demand self-service, broad network access, resource pooling, rapid elasticity, measured service
- IaaS / PaaS / SaaS = who manages the stack
- Deploy: public, private (on-prem / hosted / managed / VPC), community, hybrid, multi-cloud
- Challenges + 10 threats; lock-in fixes: containers, open APIs, OVF, UCI
- SLA 8 parts; customer / service / multi-level; OLA internal; UC with vendors
- Monolith vs microservices; API gateway; Docker + Kubernetes

**Unit 2**

- Virtualization: one box, many isolated VMs via hypervisor
- Type 1 on metal (ESXi, Hyper-V, Xen, KVM) vs Type 2 on host OS (VirtualBox)
- Types: application, network, desktop, storage, server, data
- Provision: request → allocate → create → OS → config → apps; manual vs auto vs template
- Lifecycle: create → monitor → snapshot/backup → migrate → delete
- Cold = off, copy disk; live = running, copy RAM/CPU, shared disk
- Live techniques: pre-copy (default, safe), post-copy (once, riskier), hybrid
)
