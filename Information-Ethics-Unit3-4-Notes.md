# Information Ethics (23I007) — Unit 3 & Unit 4 Exam Notes

Exam-ready notes for the two portions in the class sheet. Each portion is a **9-mark** answer. The notes follow the lecture decks (Unit III — Computer and Internet Crime; Unit IV — Professional Ethics in Computing), including the textbook tables and diagrams that were pasted into the slides as pictures.

Every heading on the portion sheet is covered. Key terms are in **bold**. Each topic has an explanation, a table or a worked example where that helps you write a full answer.

---

## Table of Contents

**Unit III — Computer and Internet Crime (9 marks)**

1. [IT security incidents](#1-it-security-incidents)
2. [Why incidents are so common](#2-why-incidents-are-so-common)
3. [Types of exploits](#3-types-of-exploits)
4. [Types of perpetrators](#4-types-of-perpetrators)
5. [Federal laws for prosecuting computer attacks](#5-federal-laws-for-prosecuting-computer-attacks)
6. [Trustworthy computing](#6-trustworthy-computing)
7. [Risk assessment](#7-risk-assessment)
8. [Establishing a security policy](#8-establishing-a-security-policy)
9. [Educating employees and contract workers](#9-educating-employees-and-contract-workers)
10. [Prevention](#10-prevention)
11. [Detection](#11-detection)
12. [Response](#12-response)
13. [Computer forensics](#13-computer-forensics)
14. [Ethical trade-offs and reasonable assurance](#14-ethical-trade-offs-and-reasonable-assurance)

**Unit IV — Professional Ethics in Computing (9 marks)**

15. [What professional ethics are](#15-what-professional-ethics-are)
16. [Why computing needs a code of ethics](#16-why-computing-needs-a-code-of-ethics)
17. [Scenarios](#17-scenarios)
18. [Sorting out computing as a profession](#18-sorting-out-computing-as-a-profession)
19. [Codes of ethics — the ACM Code](#19-codes-of-ethics--the-acm-code)
20. [Professional relationships](#20-professional-relationships)
21. [Conflicting responsibilities](#21-conflicting-responsibilities)
22. [A legal perspective: licensing and selling software](#22-a-legal-perspective-licensing-and-selling-software)
23. [Software licenses in detail](#23-software-licenses-in-detail)
24. [How to write the 9-mark answers](#24-how-to-write-the-9-mark-answers)

---

# UNIT III — Computer and Internet Crime

**Portion line:** IT security incidents. Types of exploits. Types of perpetrators. Federal laws for prosecuting computer attacks. Implementing trustworthy computing. Risk assessment. Establishing a security policy. Educating employees and contract workers. Prevention. Detection. Response.

## 1. IT security incidents

An **IT security incident** is any event in which a computer system, a network, or information is **accessed, damaged, stolen, or disrupted without proper authorization**.

Organizations protect IT because it holds:

- **Confidential business data** (plans, source code, accounts)
- **Private customer and employee data** (identity, health, pay)
- The ability to keep services running (a shop, a bank, a hospital)

A malicious act can be **theft** (data or money leaves) or **disruption** (the service stops even if nothing is copied).

**Example.** A company keeps customer records on its servers. A hacker copies those records, or knocks the server offline so customers cannot log in. Both events are IT security incidents. The first harms confidentiality. The second harms availability.

The number of such incidents has risen worldwide. Security is therefore a management duty, not only a technical one. Deciding **which** systems and data deserve the strongest protection is itself an ethical decision: money and effort are limited, and leaving customer data weakly protected can harm people who trusted the organization.

---

## 2. Why incidents are so common

Five pressures explain the rise. A full answer should name them and give one line of explanation each.

**1. Complexity creates more weaknesses.** Modern computing environments are huge and still growing. Every new server, laptop, phone, cloud account, and virtual machine is another **entry point**. Cloud computing and virtualization add layers that must each be configured correctly. A mistake in any layer can open the system.

**2. Users are under pressure, and shortcuts appear.** Help desks are pushed to solve problems fast. Staff may skip identity checks. Users share login IDs and passwords so work does not stop. Shared credentials destroy accountability: the log shows an account, not the person.

**3. Systems keep changing.** In the network era a PC is connected to millions of other machines that can exchange files and code. IT is **ubiquitous**: firms need it to meet their goals. Technology changes faster than security settings and staff training, so gaps stay open.

**4. Organizations depend on commercial software that already has known weaknesses.** An **exploit** is an attack that uses a **vulnerability** (a flaw from poor design or poor implementation). A **patch** is the vendor’s fix. Installing the patch is the user’s responsibility. Every day of delay is a day the flaw can be used.

**5. Zero-day attacks.** A **zero-day attack** exploits a serious weakness **before the vendor knows about it or before a fix exists**. There is no patch to apply yet. U.S. companies in the textbook discussion are described as heavily dependent on commercial software that still contains known, unpatched vulnerabilities — which is a wider problem than zero-days alone.

**Example.** A hospital uses a cloud billing system, a local network, staff phones, and a vendor application with a published flaw. A nurse shares a password with the night shift. An attacker uses the unpatched flaw, then the shared password. Complexity, shared credentials, and a delayed patch all played a part.

---

## 3. Types of exploits

An **exploit** is a method that takes advantage of a weakness in a computer, a phone, or software. The deck treats seven common types: virus, worm, Trojan horse, distributed denial of service, rootkit, spam, and phishing (including spear-phishing, smishing, and vishing).

### 3.1 Virus

A **virus** is malicious program code that **attaches itself to a file or program** and performs unwanted actions when that file is opened or run.

How it works:

1. It looks like an ordinary file, document, or program.
2. It attaches to a legitimate file.
3. The user opens or runs that file, and the virus becomes active.
4. It may delete or modify files, damage data, or disrupt the computer.

The harmful action is the **payload**. Example of a payload: deleting files.

A virus commonly spreads when a user opens an infected email attachment, downloads an infected program, or visits an infected website. **The user takes an action.** That is the main difference from a worm.

**Common virus types named in the lecture**

| Type | What it does |
|---|---|
| **Boot sector virus** | Infects the boot record. It can run when the machine starts, before normal programs load. |
| **Program / file infector virus** | Attaches to executable programs and runs when the user starts that program. |
| **Multipartite virus** | Uses more than one method, often both the boot sector and program files, so cleaning one place is not enough. |
| **Stealth virus** | Hides from detection. It can interfere with the operating system so scans see the original file instead of the infected one. |
| **Macro virus** | Lives in the macro language of a document (word processor or spreadsheet) and runs when the document is opened. |
| **Polymorphic virus** | Changes its own code each time it infects a file, so a scanner looking for one fixed pattern can miss it. |
| **ActiveX virus** | A harmful ActiveX control that a browser or Windows component may run. |
| **Browser hijacker** | Changes browser settings (home page, search, redirects) without genuine consent. |
| **Resident virus** | Stays in memory after the host program closes and can infect other files that are used later. |

### 3.2 Worm

A **worm** is a harmful program that **copies itself and spreads from computer to computer on its own**. It can reside in active memory while the system is running. **No human action is required** for it to move across a network. That automatic copying is its main characteristic.

**Impact of a worm**

- **Lost data and programs** — files or software damaged or deleted
- **Lost productivity** — machines and networks become slow or unavailable
- **Extra work for IT staff** — they must find, contain, and remove the worm

**Example.** One lab PC is infected. Overnight the worm copies itself to every machine that shares the network. Staff arrive to find computers unusable. Nobody had to open a file on those other machines.

### 3.3 Trojan horse

A **Trojan horse** is malicious code **hidden inside a program that looks harmless**. The user is tricked into installing it. Delivery can be an email attachment, a download from a website, or removable media (a USB drive).

Its main characteristic is **disguise**, not self-copying. It does not need to spread by itself. The user installs it because it appears to be a game, an update, a document, or a utility.

A **logic bomb** is code that stays quiet until a **trigger event** (a date, or a condition such as a particular employee’s account being removed) and then executes its payload. Logic bombs are often hidden inside programs the way a Trojan is hidden.

**Example.** A student downloads a “free PDF converter.” The converter works, so the student trusts it. Hidden code also installs a program that records keystrokes. The useful tool was the disguise.

### Virus vs worm vs Trojan horse

| Feature | Virus | Worm | Trojan horse |
|---|---|---|---|
| Meaning | Malicious code that usually attaches to a file | Harmful program that copies and spreads itself | Malicious code disguised as a harmless program |
| Needs user action | Yes | No — it can spread automatically | Yes — the user is tricked into installing it |
| How it spreads | Infected files and programs | Automatically through networks | Fake programs, email, websites, USB |
| Main characteristic | Attaches and infects | Replicates and spreads | Disguises and tricks |
| Example | User opens an infected document | One infected computer spreads to others by itself | User downloads a fake application |

### 3.4 Distributed denial-of-service (DDoS)

The attacker takes over many computers on the Internet and makes them **flood a target** with demands for data and other small tasks.

- The captured computers are **zombies**.
- A large group of zombies under one attacker’s control is a **botnet**.
- The attack **does not require a break-in at the target**. The target is simply too busy answering automated requests.
- **Legitimate users cannot get in.**

The harm is loss of **availability**. A shop loses sales. A government site loses public access. Hacktivists use DDoS to protest. Criminals use it to extort money: “pay, or the site stays down.”

**Example.** An online bookstore is flooded by thousands of zombie PCs on the morning of a sale. The site never loses its database, but customers see timeouts and buy elsewhere.

### 3.5 Rootkit

A **rootkit** is a set of programs that lets an attacker gain **administrator-level (highest) access** without the user’s knowledge. With that access the attacker has extensive control and can **hide the rootkit** so the user and ordinary security tools do not see it.

Detection is hard because a rootkit can **modify the operating system**. The operating system then returns **false information** when a scanner asks “what files are here?” The tool is asking a system that the attacker already controls.

**Example.** After a Trojan runs, a rootkit hides the Trojan’s files and processes. Antivirus that trusts the operating system’s file list reports “no infection.”

### 3.6 Spam

**Spam** is **unsolicited email** sent to many people who never asked for it. It is often cheap advertising. Some of it promotes fraudulent products.

Email marketing itself can be legitimate. A shop may mail customers who **agreed** to receive offers. The ethical and legal problem is **bulk mail the receiver did not request**, especially when the sender hides their identity.

**CAN-SPAM Act** (Controlling the Assault of Non-Solicited Pornography and Marketing) is the U.S. law that sets rules for commercial email. Commercial email can be legal if it follows the rules, including an **opt-out / unsubscribe** option and **accurate sender information**.

**CAPTCHA** (Completely Automated Public Turing test to tell Computers and Humans Apart) is a challenge that humans can usually pass and automated programs cannot. Sites use it so bots cannot create thousands of accounts or post thousands of spam messages.

### 3.7 Phishing

**Phishing** is a fraudulent attempt to **trick a person into revealing sensitive information**: passwords, bank details, card numbers. The email looks as if it came from a real bank or service. The link opens a **counterfeit website**. Whatever the user types is captured by the attacker.

**Example from the lecture (Figure 3-3).** An email pretends to be from eBay, with an eBay-style logo, and says the account will be suspended unless the member “re-updates” account information. The link is a long fake address, not eBay’s real login page. Urgency plus a copied logo is the trick.

| Type | Channel | Example |
|---|---|---|
| **Spear-phishing** | Email aimed at **one person or one organization** | An employee gets mail that looks as if it came from their own manager, asking for a password or a payment. |
| **Smishing** | SMS / text | “Your bank account will be blocked. Click this link.” |
| **Vishing** | Voice call or voice message | A caller pretends to be bank staff and asks for an OTP or account number. |

Spear-phishing is more dangerous than mass phishing because the message uses the victim’s name, role, or a real project, so it feels personal.

---

## 4. Types of perpetrators

Perpetrators differ in **goal**, **technical skill**, **money and tools**, **access**, and **how much risk they will accept**.

A 2008 Baseline magazine security survey, used in the lecture, shows why insiders matter. Reported sources of incidents included **internal users (42%)** and **former employees or contractors (35%)**, ahead of independent hackers (29%). On the “what happened” side, **spam (45%)** led, with website hacking and DDoS both at 25%, zero-day exploits at 22%, botnets at 19%, and wireless attacks at 16%. Ignorance of privacy rules (33%) and theft of laptops and PDAs (31%) were among the leading paths to loss. The numbers are from that survey year; the exam point is the pattern: **people inside the organization are a leading cause**.

### The broad groups

The lecture first groups attackers as **thrill seekers** (fun, challenge, publicity), **common criminals** (money or stolen information), **industrial spies** (a competitor’s secrets), and **terrorists** (fear, disruption, destruction). It then classifies seven types. Use this table in a 9-mark answer.

| Perpetrator | Typical motive | What to remember |
|---|---|---|
| **Hacker** | Test the limits of a system and/or gain publicity | Some are highly skilled and act from curiosity. Others have little skill and use ready-made tools. Those are **lamers** or **script kiddies**. |
| **Cracker** | Cause problems, steal data, corrupt systems | Cracking is hacking done with **malicious or criminal intent**. |
| **Malicious insider** | Gain financially and/or disrupt the firm’s systems and business | Already authorized. Includes employees, consultants, and contractors. |
| **Industrial spy** | Capture trade secrets and gain competitive advantage | Illegal collection of information the public cannot obtain. |
| **Cybercriminal** | Gain financially | Fraud against companies and customers: money, passwords, customer data. |
| **Hacktivist** | Promote a political or social ideology | Defacement, denial of service, unauthorized access, used as protest. |
| **Cyberterrorist** | Intimidate a government; destroy infrastructure | Targets finance, utilities, emergency services, government systems. The aim is fear and disruption. |

### Malicious insiders — write this if the question asks “who is hardest to stop?”

Fraud inside a firm usually traces to **weak internal controls**. **Collusion** means an insider cooperates with an outsider. Insiders are extremely hard to detect because they are **authorized to use the systems they abuse**. A badge and a password look legitimate in the logs.

A **negligent insider** is different: the person does not intend harm, but **carelessness** causes the incident (a lost laptop, a shared password, a clicked phishing link). The 2008 survey’s top “how” item — ignorance of privacy regulations — is negligence, not a master criminal.

### Industrial spies

**Trade secrets** are protected in U.S. law by the **Economic Espionage Act of 1996**.

| Competitive intelligence | Industrial espionage |
|---|---|
| Legal techniques | Illegal means |
| Information the public can obtain | Information the public cannot obtain |
| Planning and strategy | Theft of trade secrets |

### Cybercriminals and card fraud

**Computer fraud** is the use of computers or the Internet to deceive people or organizations for illegal gain. A **chargeback** happens when a customer disputes a card payment and the bank reverses it, taking the money back from the merchant. The firm loses the payment. If customers then stop trusting the firm, the long-term loss is larger than the single fraud.

**Ways to reduce online credit-card fraud**

- **Encryption** — card data is stored and sent in a form outsiders cannot read
- **Address verification** — the billing address is checked against the address the card issuer holds
- **Card Verification Value (CVV)** — the security code is an extra check that the buyer has the physical card
- **Transaction-risk scoring** — software scores each payment for suspicious patterns

A **smart card** has an embedded chip and can be updated with encrypted data at each use. The lecture notes that smart cards are used widely in Europe and were not widely used in the U.S. at the time of the text.

### Hacktivists and cyberterrorists

**Hacktivism** is the use of hacking techniques for a political or social goal: website defacement, denial-of-service, or break-ins that draw attention to a cause.

A **cyberterrorist** uses cyberattacks to pressure a government. The aim is harm, fear, or disruption. Targets include government systems, communications, power, and other critical services. Attacks may destroy data, damage systems, or stop important services. Motive separates the cyberterrorist from the cybercriminal: ideology and fear, rather than profit.

---

## 5. Federal laws for prosecuting computer attacks

The lecture’s Table 3-5 lists U.S. federal laws that prosecutors use. For a 9-mark answer, name the law and the conduct it covers. Penalties below are only those stated in the lecture table.

| Federal law | What it covers |
|---|---|
| **USA PATRIOT Act** | Defines **cyberterrorism** and sets penalties for it. |
| **Identity Theft and Assumption Deterrence Act** (U.S. Code Title 18, Section 1028) | Makes **identity theft** a federal crime. Penalties in the table: up to **15 years** imprisonment and a maximum fine of **$250,000**. |
| **Fraud and Related Activity in Connection with Access Devices Statute** (Title 18, Section 1029) | False claims and crime involving **unauthorized use of credit cards** and other access devices. |
| **Computer Fraud and Abuse Act (CFAA)** (Title 18, Section 1030) | Fraud and related acts **with computers**. |
| **Stored Wire and Electronic Communications and Transactional Records Access Statutes** (Title 18, Chapter 121) | Unlawful access to **stored** wire or electronic communications in order to obtain or alter them, or to block authorized access, while they are in electronic storage. |

**CFAA — four acts to list**

1. Accessing a computer **without authorization**, or **exceeding authorized access**
2. Transmitting a program, code, or command that **causes harm** to a computer
3. **Trafficking** in computer passwords
4. **Threatening** to cause damage to a protected computer

**How to use this in an answer.** Match the crime to the statute. A DDoS that threatens to keep damaging a bank’s computer can be discussed under the CFAA’s harm and threat provisions. Stealing a customer’s identity and opening accounts fits the Identity Theft Act. A phishing gang collecting live card numbers fits the access-device statute. Breaking into stored email fits the stored-communications statutes. An attack meant to coerce a government fits the PATRIOT Act’s cyberterrorism provisions. State the match; do not claim a penalty the table does not give.

These are **federal** U.S. statutes, which is what the portion asks for. Prosecution still depends on evidence, jurisdiction, and the organization’s own logs — which is why response and forensics (sections 12 and 13) matter.

---

## 6. Trustworthy computing

**Trustworthy computing** means designing and operating systems that people can **trust to work safely and correctly**. It delivers computing that is secure, private, and reliable, and it rests on sound business practices.

### Microsoft’s four pillars (Figure 3-4)

The lecture diagram shows trustworthy computing held up by four pillars.

| Pillar | Meaning | Actions the lecture attributes to Microsoft |
|---|---|---|
| **Security** | The system resists attack and protects data | Invest in the expertise and technology needed for a trustworthy environment. Work with law enforcement, industry, academia, and the private sector. Educate consumers on secure computing. |
| **Privacy** | People control information about themselves | Make privacy a priority in design, development, and testing. Contribute to standards and policies of industry and government. Give users a sense of control over personal information. |
| **Reliability** | The system keeps working and can be restored | Build systems that (1) continue to provide service despite internal or external disruption; (2) can be restored to a known state with no data loss; (3) give accurate and timely service; (4) accept required changes without disruption; (5) ship with minimal bugs; (6) work as promised. |
| **Business integrity** | The company behaves in a way customers can trust | Be **responsive**: take responsibility for problems and correct them. Be **transparent**: open dealings, clear motives, kept promises, so customers know where they stand. |

### Security is technology, policy, and people

One product cannot produce trust.

- **Technology** — firewalls, antivirus, encryption, access control
- **Policy** — written rules for how systems and information are protected
- **People** — employees and users who understand the risks and follow the rules

Trust also requires continuous work: monitoring, access control, software updates, awareness, backups, and incident response. Networks should be **watched continuously** so an intrusion is seen early, before the damage spreads.

### Clear reaction plan

When an intrusion happens, a plan written **in advance** should cover:

1. **Notification** — tell the right people
2. **Evidence protection** — do not alter or destroy evidence
3. **Activity log** — record what happened and what was done
4. **Containment** — stop the attack spreading
5. **Eradication** — remove the cause (for example, the malware)
6. **Recovery** — restore normal service

This plan is the bridge to Prevention, Detection, and Response. Trustworthy computing is the goal. Risk assessment, policy, education, and the three operational stages are how an organization pursues it.

---

## 7. Risk assessment

**Risk assessment** identifies and evaluates the security risks to an organization’s systems and networks.

- **Internal threats** come from inside: an employee misusing access, or someone accidentally exposing data.
- **External threats** come from outside: hackers, malware, phishing.

No organization can block every threat. Assessment decides **where money, technology, and staff should go**. Priority goes to threats that are **likely** and **serious**. Resources are limited, so the organization spends where it gets the **greatest reduction in risk for the resources used**.

### The eight steps (learn this order)

The lecture’s general security risk assessment (ASIS-style diagram) is a loop. After a decision, the organization **reassesses** when conditions change.

| Step | Action | Question it answers |
|---|---|---|
| 1 | **Identify the assets** of most concern | What would hurt us most if lost? |
| 2 | **Identify loss events** | What could happen to those assets? |
| 3 | **Assess likelihood** | How probable is each threat? |
| 4 | **Determine impact** | What does a successful attack cost? |
| 5 | **Determine mitigation** | What could reduce this threat? |
| 6 | **Assess feasibility** | Can we actually implement that option? |
| 7 | **Cost-benefit analysis** | Is the control worth its cost? |
| 8 | **Decide** which countermeasures to implement | What will we do now? |

**Expected cost** in the lecture’s worked table is **probability × cost of a successful attack**. Priority also considers how good current protection already is. A very likely event with a small loss and strong existing controls can rank **below** a less likely event that would be catastrophic and is poorly defended.

### Worked table from the lecture (hypothetical company)

| Risk | Business objective threatened | Probability | Cost if successful | Expected cost | Current protection | Priority |
|---|---|---|---|---|---|---|
| DDoS on a retail website | 24/7 operation of the site | 40% | $500,000 | $200,000 | Poor | **1** |
| Email attachment with a harmful worm | Rapid, reliable communication with staff and suppliers | 70% | $200,000 | $140,000 | Poor | **2** |
| Harmful virus | Staff use of personal productivity software | 90% | $50,000 | $45,000 | Good | **3** |
| Invoice and payment fraud | Reliable cash flow | 10% | $200,000 | $20,000 | Excellent | **4** |

The virus is the **most probable** event and still ranks third, because the damage is smaller and protection is already good. DDoS ranks first because the expected loss is the largest and protection is poor. Quote this logic if the examiner asks you to “prioritize.”

### Model answer — the lecture’s practice question

**Facts.** A software company stores source code, customer information, employee records, and financial data on its internal network. Ransomware recently made some files unavailable. Proposed controls: cloud backups, endpoint protection, network monitoring, staff training, multi-factor authentication. Some of these need heavy spending and more technical staff.

**Answer using the eight steps.**

1. **Assets.** Source code (the product), customer data (legal and trust duties), employee records (privacy), financial data (fraud and survival of the firm). Customer data and source code are the assets of greatest concern.
2. **Loss events.** Ransomware encrypting file servers; a phishing mail that starts the ransomware; an insider copying source code; loss of the only backup because it sat on the same network.
3. **Likelihood.** The firm has **already** suffered ransomware, so recurrence is credible and should be rated high, especially if email and remote access remain weakly checked.
4. **Impact.** Source code loss can stop product delivery. Customer-data loss brings legal duties, notification cost, and loss of trust. Downtime stops revenue. Impact is high for code and customer data, moderate for a short outage if backups work.
5. **Mitigation options.** Cloud backups (recovery), endpoint protection (block malware), network monitoring (see the attack early), training (cut the phishing path), multi-factor authentication (stolen passwords are not enough).
6. **Feasibility.** Training and multi-factor authentication can start quickly. Cloud backup needs a design that keeps backups **offline or immutable**, or ransomware will encrypt them too. Monitoring needs staff who can read alerts. Hiring may be slow.
7. **Cost-benefit.** Compare the cost of each control with the expected loss of another ransomware week. Backups and multi-factor authentication usually show a strong benefit because they directly cut the incident the firm already had. A large monitoring project that the firm cannot staff may fail the feasibility and cost tests **for now**.
8. **Decision.** Implement first: tested cloud backups separated from the live network, multi-factor authentication on admin and remote access, and short practical training on phishing. Add endpoint protection next. Defer a full monitoring centre until there are people to run it. **Reassess** after the next quarter, or after any new incident.

That paragraph is a complete answer to the slide question. Change the company details if the exam changes the story, and keep the eight steps in order.

---

## 8. Establishing a security policy

A **security policy** defines:

- The organization’s **security requirements**
- The **controls and sanctions** needed to meet them
- **Who is responsible** for what
- **How users are expected to behave**

It states **what** must be done. It does not specify every technical **how** (which brand of firewall, which command). Detailed procedures sit under the policy. **Automated controls should mirror the written policy.** If the policy says “passwords are not shared” and the system allows one shared admin login for the whole team, the written rule and the real system contradict each other, and staff will follow whichever is easier.

### Ease of use and security

Stronger security often makes work less convenient. A firm must balance the two. Too little security invites incidents. So much security that people cannot work leads them to bypass the controls (shared passwords, shadow IT).

**Areas the lecture highlights**

| Area | Risk | Policy direction |
|---|---|---|
| **Email attachments** | Malware and viruses | Do not open suspicious attachments. Filter mail and scan with antivirus. |
| **Wireless devices** | Traffic can be intercepted | Use encryption and authentication. |

### Virtual private network (VPN)

A **VPN** lets a user communicate across the Internet with **security and privacy**. The Internet still carries the packets, but the VPN adds:

- **Encryption** — outsiders cannot read the contents
- **Authentication** — the organization checks who is connecting
- **Tunneling** — the protected channel between the user and the organization’s endpoint

**Example.** A contract developer works from home. Without a VPN, project files cross the café Wi-Fi in the clear. With a VPN, an encrypted tunnel runs from the laptop to the company gateway. The café sees traffic, and cannot read the files.

---

## 9. Educating employees and contract workers

Technology fails if people do not use it properly. The organization must **educate and motivate everyone who uses its systems**: full-time employees, **contractors**, and **part-time workers**. Contractors are included because the insider discussion showed they often hold the same access as staff, and the survey flagged former contractors as a major source of incidents.

Teach four things:

1. **What** the security policies are
2. **Why** they matter (use a recent, real incident so the threat is concrete)
3. **What to do and what not to do**
4. **What to do when they notice a problem** (who to call, what not to touch)

**Habits the lecture lists**

- Guard passwords
- Do not share passwords
- Apply strict access controls so people see only the data their work needs
- Report unusual activity
- Protect portable computers and storage devices (laptops, phones, USB drives — the survey linked laptop and PDA theft to a large share of incidents)

**Example.** A one-hour session shows last month’s fake-bank SMS (smishing) and walks staff through reporting it to the help desk instead of tapping the link. Contractors who join for a three-month project attend the same session on day one. Education is part of trustworthy computing’s “people” pillar.

---

## 10. Prevention

Prevention makes a break-in **harder**. The lecture insists on a **layered** solution. If one control fails, another still stands.

### Technical layers

| Control | Role |
|---|---|
| **Corporate firewall** | Stands at the **network perimeter** and limits what traffic may pass between the internal network and the Internet. The lecture diagram shows staff computers inside the perimeter, with web and email servers placed behind firewalls so the Internet cannot reach them directly. |
| **Intrusion prevention system (IPS)** | **Blocks** viruses, malformed packets, and other threats, rather than only recording them. |
| **Antivirus software** | Scans files for a **virus signature** (a known sequence of bytes) and for suspicious patterns. |
| **US-CERT** (United States Computer Emergency Readiness Team) | A **clearinghouse**: it collects information about threats and incidents and distributes it so organizations can prepare. |

The lecture also shows examples of personal firewall products of that period (ZoneAlarm, F-Secure, Panda, NeT Firewall, ESET). You do not need the vendor list unless the question asks for examples. You do need the **function**: a firewall limits network access.

### Safeguards against malicious insiders

A malicious insider misuses **legitimate** access. Prevention is therefore about access, not only about blocking strangers.

- When an employee or contractor **leaves**, delete computer accounts, login IDs, and passwords **immediately**. The survey’s high share of former staff and contractors is the reason.
- **Define roles** and separate key duties. The person who creates a payment should not be the only person who approves it.
- Give each account **only the permissions the job needs**. This is the **principle of least privilege**.

### Defending against cyberterrorism

The lecture points to the U.S. **Department of Homeland Security** and its **National Cyber Security Division (NCSD)**. That body is described as building a national cyberspace response system and running a **cyber-risk management program** for critical infrastructure: banking and finance, water, government operations, and emergency services. The exam point: cyberterrorism is treated as a national infrastructure problem, not only as a single company’s firewall problem.

### IT security audit

An organization must check that policies, controls, and systems **actually work**. A periodic **IT security audit** includes:

- Are policies followed, or only written?
- Who has access, and is that access still justified?
- Do safeguards work when they are tested?

The lecture mentions the Computer Security Institute’s **Information Protection Assessment Kit** as a checklist resource for finding weak practices.

**Example of layering.** Mail is filtered (stops many viruses). Antivirus scans what gets through. A firewall blocks unexpected inbound connections. Least privilege means a compromised clerk account cannot reach the source-code server. If ransomware still starts, the separated backup from the risk-assessment answer is the last layer. No single product was “the” security.

---

## 11. Detection

A **detection system** tries to recognize an intruder or suspicious activity. An **intrusion detection system (IDS)** monitors system and network activity and **notifies** the proper authority when it sees:

- Possible intrusions from **outside**
- Misuse from **inside**

An IDS **reports**. An IPS **blocks**. Many products do both; in an exam, keep the lecture’s distinction.

### Two approaches

| Approach | Also called | How it works | Strength | Limitation |
|---|---|---|---|---|
| **Knowledge-based** | **Signature-based** | Compares activity with **known attack patterns** | Reliable for attacks it already knows | Misses a new attack that has no signature yet (including many zero-days) |
| **Behavior-based** | **Anomaly-based** | Learns what **normal** behavior looks like, then flags large deviations | Can catch new attacks | Unusual but legitimate work (a year-end payroll run, a big software release) can look like an attack |

**Example.** Signature-based detection catches a worm whose byte pattern is already published. It misses a brand-new worm. Behavior-based detection flags that new worm because the PC suddenly opens connections to hundreds of machines at 3 a.m. It may also flag a developer who legitimately copies a large build at 3 a.m. Staff must investigate alerts; detection without a response plan is only a log.

---

## 12. Response

A **security response** is the action taken when an incident occurs. A **response plan** is the predefined set of those actions. It is written **well before** any incident and approved by the **legal department** and **senior management**. The lecture notes that only about **56%** of organizations in the source material even had a response plan — a useful point about how often firms are unprepared.

### Primary goals

1. **Regain control** of the affected systems
2. **Limit damage** so the incident does not get worse

The primary purpose is **not** to monitor or catch the intruder. Catching someone may be attempted later. The immediate duty is to protect the organization.

### Notification and records

The plan defines **who to notify** and **who not to notify**. Security experts in the lecture advise **against** publishing specific details of a compromise in public forums. Those details help other defenders only after they have also helped the next attacker, and they can create panic or legal exposure.

Document:

- All system events
- Specific actions taken
- All external conversations

### After detection: contain, eradicate, review

**Containment** means controlling the attack so it stops spreading. Act quickly. Example: disconnect the affected segment, disable the compromised account, block the command server at the firewall.

**Eradication** means removing the cause. During this stage the organization should:

- Collect and log evidence that may be needed in a criminal case
- Verify that backups are **current and complete**
- Create **fresh backups** of cleaned systems
- Find **how** security was compromised
- Change the weakness so the same path does not work again

**Review** happens after containment and eradication. Its purpose is to learn and improve:

- Determine exactly what happened
- Evaluate how the organization responded
- Weigh the effort required to pursue the perpetrator
- Consider **negative publicity**
- Consider **legal precedent** (earlier court decisions that will shape how this case is treated)
- Remember that organizations can be held **accountable for their own IT security weaknesses** — a firm that ignored patches and had no plan is in a weak position if customers sue

**Example.** Ransomware encrypts the file server at 9 a.m. The plan says: the incident lead calls the CIO and legal, not the press; the affected network segment is isolated within minutes; last night’s offline backup is confirmed; a restored copy is scanned before users are allowed back; a review the next week finds that multi-factor authentication was still “planned,” and it is then switched on. Chasing the attacker is discussed with legal **after** service is back. That order matches the lecture: control and damage first.

---

## 13. Computer forensics

**Computer forensics** combines computer science and law. It **identifies, collects, examines, and preserves** digital data while **keeping its integrity**, so the data can be evidence in a legal proceeding.

An investigation needs **specialized training** in forensic procedure and in the rules for collecting criminal evidence. Ordinary IT troubleshooting can destroy the very proof a court needs: opening a file changes timestamps; rebooting can wipe memory; copying a disk carelessly can be challenged as altered.

The practical rules that follow from the lecture’s definition:

- Preserve the original. Work on a verified copy where possible.
- Record who collected the evidence, when, and every person who handled it, so the chain of possession is clear.
- Coordinate with the legal department (the response plan already requires legal approval).
- Use forensics when the organization may prosecute, sue, or defend itself. The summary slide states that computer forensics is key to fighting computer crime **in a court of law**.

**Example.** An insider is suspected of copying the customer database onto a USB drive. The response team does not “have a look” on the live PC and then put it back on the desk. A trained investigator images the disk, bags the USB drive, and writes down the time and the names. If the firm later relies on the CFAA or on internal discipline, the evidence still exists in the form it was found.

---

## 14. Ethical trade-offs and reasonable assurance

The unit objectives ask for the trade-offs in safeguarding systems, and for the multilayer process based on **reasonable assurance**.

**Reasonable assurance** is the management judgment that **perfect security is not a rational goal**. Controls cost money, slow work, and can intrude on staff. Managers implement controls up to the point where **more spending would exceed the benefit or the risk avoided**. Risk assessment (the eight steps and the cost-benefit stage) is how that judgment is made. Leaving a known, cheap-to-fix hole in a system that stores customer data fails reasonable assurance. Buying a control that costs more than the asset is worth also fails it.

**Ethical issues to mention in a long answer**

- **Which data is protected first.** Customer privacy and safety-critical systems have a stronger claim than convenience data. Choosing only what is cheap to protect, and ignoring what would harm people, is an ethical failure.
- **Ease of use versus security.** Staff who cannot do their jobs will bypass controls. A policy that ignores human behavior creates the incident it meant to stop.
- **Monitoring versus employee privacy.** Detection of insider misuse can require logging. Logging can become surveillance. The policy should be known to staff, limited to security purposes, and not used as secret punishment.
- **Catching the attacker versus the organization’s duties.** Public detail can warn others and can also aid attackers and cause unfair panic. The lecture’s priority is regain control and limit damage. Pursuit is a later, legal decision.
- **Accountability.** Courts and customers may hold the organization responsible for weak security. “We were hacked” is not a complete moral answer if patches, training, and backups were ignored.
- **Contractors and unequal care.** People with access must receive the same rules and the same prompt removal of access when they leave. Protecting only full-time staff accounts leaves the path the survey highlighted.

**The multilayer process (summary of the whole unit)**

1. **Assess** threats (risk assessment, reasonable assurance)
2. **Decide** actions for the serious vulnerabilities
3. **Write** policy (what, who, sanctions)
4. **Educate** employees, contractors, and part-time staff
5. **Prevent** with layered technology and least privilege
6. **Detect** with signature-based and behavior-based monitoring
7. **Respond** from a pre-approved plan: contain, eradicate, recover, review
8. **Use forensics** when the evidence must stand up in law

IT leads the technical work. Senior management owns the policy, the budget, and the decision to accept residual risk.

---

# UNIT IV — Professional Ethics in Computing

**Portion line:** Scenarios. Sorting out computing. Mastery of knowledge. Formal organization. Autonomy. Codes of ethics. The culture of computing. Professional relationships: employer–employee, client–professional, other stakeholders–professional, professional–professional. Conflicting responsibilities. A legal perspective on professionalism in computing. Licensing. Selling software.

## 15. What professional ethics are

**Professional ethics** are a **code of conduct** for how members of a profession deal with **each other** and with **third parties**. They are the rules of proper behaviour for that kind of work.

- **Other professionals** — colleagues, teammates, managers in the same field
- **Third parties** — customers, clients, employers who are not computing specialists, organizations, and society

A job can be done with technical skill and still be unethical. Professional ethics ask whether the work was honest, competent, and fair to the people who depend on it.

### What a professional code is for

A code does five jobs. Learn this list.

1. **Symbolizes professionalism.** The group shows the public that it holds itself to a standard.
2. **Sets a standard for external relations** with clients and employers. Outsiders know what they may expect.
3. **Protects the group’s interests.** A public scandal by one member harms every member’s reputation.
4. **Codifies members’ rights.** Members know what they may insist on (for example, the right to refuse work that would harm the public).
5. **Guides “gray areas.”** Rules of law do not cover every new case. A code gives a way to reason when the law is silent.

A code is **not a criminal statute**. It guides members and, for a society such as the ACM, can affect membership. It does not by itself send anyone to prison. Law (section 22) is a separate layer.

---

## 16. Why computing needs a code of ethics

The lecture gives three reasons that are specific to software.

**1. Software can do good or cause harm.** It improves healthcare, education, communication, and banking. It also harms people when it is badly designed, misused, or built without care. Software can **enable other people** to do good or harm. The person who writes a tool shares responsibility for the uses the tool makes easy.

**2. Software controls many parts of daily life.** Banking, education, and healthcare now depend on it. Computing professionals therefore carry a duty to build software that is **reliable, secure, and ethical**. A bug in a game is an annoyance. A bug in a dosage system or a payment system injures people or takes their money.

**3. People rarely notice the software they depend on.** Office software, banking software, and online shopping software sit in the background. If those systems are incorrect, insecure, or misused, the harm is wide precisely because users trusted them without inspecting the code.

**Example.** A payment app that double-charges, or quietly stores card numbers in a way phishers can steal, harms thousands of people who never see the developer. The code of ethics exists so “it compiled” is not the only test of finished work.

---

## 17. Scenarios

The portion begins with **scenarios** because professional ethics is tested by situations, not only by definitions. Use one fixed method so a scenario question stays organized. Four steps:

1. **Facts and stakeholders.** Who is affected: employer, client, users, the public, colleagues, you?
2. **Duties.** What does each relationship require (section 20)? Where do they pull in opposite directions (section 21)?
3. **Code.** Which principles apply: avoid harm, be honest, respect privacy, work only within competence, keep quality high, put the public good at the centre (section 19)?
4. **Action.** State what you should do, what you should refuse, and who you should tell. Prefer the option that reduces serious harm and stays honest. Do not stop at “it depends.”

### Scenario A — Shipping known defects (employer vs public)

You test a banking app. A flaw lets a logged-in user view another customer’s balance. Your manager says the festival sale starts Monday and the fix will ship “in the next update.” Marketing has already announced the launch.

**Stakeholders:** customers, the bank (your client or employer), you, the public who will be told the app is safe.

**Conflict:** loyalty and a deadline versus the duty to avoid harm and to be honest.

**Better action:** Do not treat the launch as a private team problem. Report the defect in writing, state the customer harm, and ask for a delay or a disabled feature. If you are ordered to hide a security flaw that can expose people’s money, escalation to a higher manager or to the client’s security officer is justified. The ACM principles on harm, honesty, and thorough evaluation of risks all point the same way. Quietly shipping and hoping is an ethical failure even if the manager accepts the risk.

### Scenario B — A colleague who is not fit to work (professional vs professional)

A teammate’s drinking has become obvious. His modules fail in ways that corrupt patient records in a clinic system. Reporting him may end his job. Staying silent protects a colleague and injures patients.

**Conflict:** the impulse to protect a fellow professional versus duties to the employer, the client, and the public.

**Better action:** Speak to him first if it is safe to do so, and do not conceal the defect in the product. The faulty work must be reviewed and corrected. If he will not stop handling safety-related code, tell the manager. Helping him find support can sit alongside that report. Covering for him so the team “looks fine” makes you part of the harm. Section 20.4 uses almost this example: secrecy saves a career on one side and makes clients suffer on the other.

### Scenario C — The client wants hidden tracking (client vs users)

A client asks you to add tracking that collects location and contacts, and to hide it behind a vague line in a privacy policy (“we may collect usage data”). The client is paying. Users are not in the room.

**Conflict:** the client–professional duty to serve the client’s goals versus respect for privacy, honesty, and the users who are stakeholders.

**Better action:** Explain the duty to be honest and to respect privacy. Offer a design that collects only what the feature needs and asks for a clear consent. Refuse a design whose purpose is to hide collection. “The client paid” does not cancel a duty to people who will be deceived. If the client insists, decline that part of the work and record why.

### Scenario D — Selling a product that contains GPL code (employer vs license / users)

Your employer’s commercial product includes a library under the **GNU GPL**. Sales wants to ship a binary only, with a proprietary license, and no source code. The employer says “everyone does this.”

**Conflict:** employee loyalty versus copyright law and the duty of honesty in selling software.

**Better action:** The GPL requires that distributed derivatives make the corresponding source available under GPL terms (section 23). Shipping a closed binary misrepresents what the firm has the right to sell and shifts legal risk onto the firm and its customers. Tell the employer in writing. Options that are actually available: replace the library with code you can ship under your license (MIT, BSD, or a commercial license), or comply with the GPL and release the corresponding source. Ignoring the license is not a gray area. It is infringement.

These four scenarios cover the relationships the portion names. In the exam, reuse the four-step method on whatever story is printed.

---

## 18. Sorting out computing as a profession

**Sorting out computing** means testing computing against the features that mark a mature profession, instead of assuming that “we write software” is enough. A profession is more than paid work. The portion names five features. Judge computing against each one, then give an overall conclusion.

| Feature | What a mature profession has | How computing stands |
|---|---|---|
| **Mastery of an esoteric body of knowledge** | A deep body of knowledge that takes long, formal training. Clients cannot easily judge the work, so they must trust the practitioner. | Computing has a large formal body of knowledge (algorithms, architecture, software engineering, security). It also changes very fast, and many skilled practitioners are self-taught or trained only on the job. Mastery is real for specialists and uneven across the people who ship software. |
| **Formal organization** | A society that sets standards, admits members, and can discipline them. | ACM, IEEE Computer Society, the British Computer Society, and similar bodies exist and publish curricula and codes. They do **not** control entry. A company may hire a programmer who belongs to none of them. Organization exists; control of the occupation does not. |
| **Autonomy** | Practitioners set their own standards and are trusted to judge their own work. Outside interference does not replace professional judgment. | Many computing workers are employees. Deadlines, managers who are not computing specialists, and client contracts often override technical judgment (Scenario A). Autonomy is stronger for independent consultants and for licensed engineers in safety-critical fields, and weaker for ordinary product teams. |
| **Codes of ethics** | A public code that states duties and guides hard cases. | Computing has serious codes, above all the **ACM Code of Ethics and Professional Conduct** and the Software Engineering Code of Ethics (ACM / IEEE-CS). They bind people who accept them. They do not bind every person who writes code, and violating them rarely removes the legal right to keep working. |
| **The culture of computing** | Shared identity, pride in good work, and a habit of service to clients and the public. | There is a real culture: care for correctness, peer review, and in open source a culture of sharing and attribution. There is also a conflicting culture of shipping fast, treating security as optional, and measuring success only by growth. Computing does not yet have one professional culture the way medicine does. |

**Conclusion you can write.** Computing is best described as an **emerging or maturing profession**, sometimes called a quasi-profession. It has knowledge, societies, and codes. It does not yet have restricted entry, reliable autonomy, or a single service culture. That conclusion does **not** lower the ethical duty. Software already affects health, money, and privacy, so the standards of a profession apply **before** the law treats every programmer like a doctor. The rest of this unit — the ACM Code, the four relationships, and the law of licensing and selling — is how that duty is practiced.

**Mastery, in an answer, means three things:** the person has the knowledge the task needs; the person **refuses work outside that competence**; and the profession keeps a shared body of knowledge (courses, curricula, journals) so “competence” is not a private opinion. The ACM principle “perform work only in areas of competence” is mastery put into a rule.

---

## 19. Codes of ethics — the ACM Code

The lecture presents the **ACM Code of Ethics and Professional Conduct** in four parts. A 9-mark question on “codes of ethics” should name the code and give principles from more than one part, each with a short meaning. You do not need all 25 lines if time is short; you do need the structure and the principles that carry the most marks (harm, honesty, privacy, quality, competence, public good, security).

### Part 1 — General ethical principles

These apply to every computing professional, member or not, as moral guidance.

| Principle | Meaning in practice |
|---|---|
| **Contribute to society and human well-being**, recognizing that all people are stakeholders | The people who never meet you still count: users, neighbors, future users of a public system. |
| **Avoid harm** | Harm includes negative consequences, not only crimes. Insecure design, biased systems, and hidden defects count. |
| **Be honest and trustworthy** | Claims about what the software does, what data it collects, and what risks remain must be true. |
| **Be fair and do not discriminate** | Systems and workplace conduct should not treat people unjustly. If a system will disadvantage a group, act. |
| **Respect the work required to produce new ideas, inventions, creative works, and computing artifacts** | Honor copyright, licenses, and credit. Using GPL code and stripping the license violates this principle and the law. |
| **Respect privacy** | Collect less, protect what you hold, be clear with the people the data is about. |
| **Honor confidentiality** | Information learned through work (client secrets, employer plans, personal data) stays confidential. |

### Part 2 — Professional responsibilities

| Principle | Meaning in practice |
|---|---|
| **High quality** in process and product | Testing, review, and maintainable design are ethical duties, not optional polish. |
| **High standards of competence, conduct, and ethical practice** | Keep skills current. Outdated security knowledge is a competence problem. |
| **Know and respect existing rules** | Laws, regulations, contracts, and licenses (CFAA for attacks, GPL for code, privacy statutes for data). |
| **Accept and provide appropriate professional review** | Invite review of your work and give honest review of others’ work. |
| **Give comprehensive evaluations of systems and their impacts, including risks** | Tell the client what can go wrong. Scenario A’s hidden flaw fails this test. |
| **Perform work only in areas of competence** | Do not accept a medical-device project if you have no way to do it competently. |
| **Foster public awareness** of computing and its consequences | Help non-specialists understand risk. This supports the “people” pillar of security. |
| **Access computing resources only when authorized**, or when compelled by the public good | Breaking into a system “to look” fails this principle. The public-good exception is narrow (for example, a genuine emergency), not a hobby. |
| **Design systems that are robustly and usably secure** | Security that people cannot operate will be bypassed. Usable security is part of the ethics, and it matches Unit III’s ease-of-use trade-off. |

### Part 3 — Professional leadership principles

These bind people who lead teams, products, or organizations.

- Make the **public good the central concern** in professional computing work.
- Articulate social responsibilities, encourage the group to accept them, and **check whether they are actually met**.
- Manage people and resources so the **quality of working life** improves. Crunch that produces known defects is a leadership failure.
- Put policies in place that **reflect the Code**, and support them.
- Create opportunities for people to **grow as professionals**.
- **Use care when modifying or retiring systems.** Turning off an old system can cut people off from records, pay, or care.
- Take special care of systems that have become **part of society’s infrastructure** (payments, identity, health, utilities).

### Part 4 — Compliance with the Code

**Compliance** means ACM members **follow, support, and respect** the Code.

- **Uphold** — follow it in your own work
- **Promote** — encourage colleagues to follow it
- **Respect** — treat it as binding guidance, not as decoration

Treating a serious, knowing violation as **inconsistent with ACM membership** means the society can judge that the person has stepped outside what membership requires. That is a professional sanction. It is separate from criminal prosecution under the laws in Unit III.

**Example tying the code to Unit III.** An engineer who leaves a customer database unpatched, hides the ransomware risk from management, and then blames “hackers” has failed “avoid harm,” “be honest,” “high quality,” and “usably secure.” The CFAA may apply to the attacker. The Code applies to the engineer.

---

## 20. Professional relationships

A **professional relationship** is the ethical link between a computing professional and a person affected by the work. The portion asks for four, plus conflicting responsibilities (section 21).

### 20.1 Employer–employee

An **employee** is a person who performs services for an organization for pay. The lecture distinguishes kinds of employment because duties and benefits differ:

| Type | Meaning in the lecture |
|---|---|
| **State employee** | Appointed or elected into a state position, typically inside a public retirement and insurance system. |
| **Contract employee** | Does not hold that kind of state post; engaged under a contract. The lecture notes they may still have contribution duties of their own. |
| **Private employee** | Works for a private company. A private employee can **also** be a contract employee. “Private” names the **employer**. “Contract” names the **arrangement**. |

An **employer** is the person or organization that directs the worker under a contract of employment and pays wages or salary.

**Employer–employee relations** are the ongoing pattern of working together, communicating, and meeting each side’s duties. The lecture’s practical advice for building the relationship: open communication, a culture of appreciation, consistent feedback, and following through on what was promised. Those practices build trust, respect, and cooperation.

**Benefits of a healthy relationship:** higher productivity, employee loyalty, fewer conflicts, higher morale, easier delegation. The lecture’s image is that employer and employee are two wheels of one engine; the organization moves when both turn together.

**Ethical content, not only HR content.** The employee owes competent work, honesty, care of the employer’s confidential information, and respect for licenses and security policy. The employer owes a fair direction of the work, the tools and authority the job needs, and a workplace in which raising a safety or security defect is not punished. Unit III’s rule — educate contractors and part-time staff, and remove access the day they leave — is an employer duty inside this relationship.

### 20.2 Client–professional

A **client–professional** relationship joins an expert with a person or organization **using that expert’s services**. The lecture describes it as **low in interdependence** (the professional is not the client’s employee for life) and as either personal or impersonal.

The deck’s picture of a **good** relationship is demanding, and several slides use the language of professional care (including social-work ethics). Translated into computing practice, the marks come from these duties:

- The client has a right of **self-determination**. The client takes part in decisions about their own needs. You work **with** the client, not on the client.
- Show **confidence** in the client and a genuine interest.
- **Listen**, including to the concern behind the feature request.
- **Warmth, respect, and trust.**
- Treat the client as a **unique** case. Do not stereotype (“all small shops want the same website”).
- **Acceptance** and a non-judgmental attitude while you are understanding the problem; this does not mean you accept an unethical instruction.
- **Empathic understanding** — a conscious awareness of the other person’s situation.
- **Genuineness**: be real, be human, be honest. Do not pretend a system is ready.
- **Confidentiality.** The social-work wording in the lecture is the right standard here too: respect the client’s privacy and hold in confidence what you learn in the service. Source code, business plans, and user data leave the engagement only as the contract and the law allow.

**Example.** A clinic hires you to build an appointments system. You do not reuse their patient list as a demo for the next client. You explain risks in plain language. You do not add hidden tracking because a salesperson at the clinic asked for it in the corridor (Scenario C).

### 20.3 Other stakeholders–professional

**Stakeholders** are everyone with an interest in the work: **clients, suppliers, partners, investors, employees, and the wider community**. If one group is ignored, the damage shows up elsewhere in the business. Building these relationships takes time and a plan.

The lecture’s method is practical. Use it as a numbered answer.

1. **Group them.** Some have a **vested interest** in success (investors, project managers, clients). Some are **affected by the outcome** (employees, customers, end users, the community).
2. **Split by role in decisions.** People **directly involved** (the project team), people with **influence** (manager, client, investor), and people who must stay **informed** (end users, employees). Each group gets a different kind of communication.
3. **State the project scope and the decision rules early.** Say what is negotiable, what is not, and how they will be consulted. People listen when they know their real influence.
4. **Earn trust at the start.** Explain benefits early and often. Stakeholders who understand the history and the trade-offs are less likely to attack the decision at the end, even if they disagree.
5. **Keep the message consistent.** Contradictory updates produce outrage and a loss of trust. If the security scope changed, say so once, clearly, to every group.
6. **Meet the people who resist the change.** Do this during the work, in person, by mail, or by phone. Waiting until the final announcement produces angry calls. Listening is part of showing why the change is justified.
7. **Record meetings.** What was it about, what was decided, what are the actions, when is the next meeting? A data store of those summaries stops “nobody told us.”
8. **Keep surprises small.** Raise important risks early. Do not dump every minor issue on stakeholders, and do not hide a serious one. Come with **options**, not only with a problem, and let them add to the choice.

**Example.** A university replaces its grading system. Students are affected but do not run the project. Faculty influence requirements. The vendor and the IT team are directly involved. Telling students only on launch day that the old marks will be unavailable for a week fails steps 3, 4, and 8. A short notice a month ahead, with a paper fallback, treats students as stakeholders.

### 20.4 Professional–professional

This is the relationship with **other professionals in the same or a related field**. Members often feel special duties: support colleagues, give fair opinions, cooperate.

The lecture lists ordinary acts of that duty: they comment on each other’s work, they help each other find work, and they **testify at hearings** when a colleague is sued. Testimony must be **truthful, objective, and based on professional knowledge**. Supporting a friend by bending technical evidence is a betrayal of the court, the client, and the profession.

Special treatment is sometimes right and sometimes wrong.

- **Right:** a fair reference, honest peer review, teaching a junior colleague, covering a shift so a defect gets a second pair of eyes.
- **Wrong:** hiding a colleague’s incompetence when clients will be harmed; **price-fixing** among professionals so fees rise and clients lose the benefit of a competitive market; lying about qualifications; taking bribes; fudging test results.

Professionals may unite to protect a **common interest** (fair contracts, safety standards, the reputation of the field). They may not unite to protect **unethical behaviour**. Every member has a stake in the profession’s reputation, because the public judges the whole group by the members it sees. One engineer who fakes a security test makes the next engineer’s word worth less.

**Example.** You are asked to testify that a former classmate’s access-control design “met industry practice.” You know it did not. Friendship and the professional duty to be truthful conflict. The testimony has to match the technical facts. That is the culture of computing at its best: peer loyalty stops where deception begins.

---

## 21. Conflicting responsibilities

**Conflicting responsibilities** arise when a professional owes duties that **require different actions at the same time**. The usual parties in the lecture are:

- The employer
- The client
- Fellow professionals
- Users
- Society / the public

The conflict is the normal form of a hard case, not a sign that ethics has failed. A strong answer **names both duties**, says which harm is more serious, and chooses an action that stays honest.

| Conflict | Duty on one side | Duty on the other side | How to resolve it in this course |
|---|---|---|---|
| Ship now / fix first | Employer: meet the deadline and the launch promise | Public and users: avoid harm; be honest about risk | Do not hide a serious defect. Escalate. Offer a reduced launch. |
| Protect a colleague / protect the client | Fellow professional: do not destroy a career casually | Client and public: the work must be safe | Correct the work. Report if the person will not stop. Help the person, and do not fake the results. |
| Do what the client paid for / respect users | Client: build the requested system | Users: privacy, honesty, no deception | Build a consented, minimal version. Refuse covert collection. |
| Follow orders / follow the license | Employer: ship the commercial product | Copyright owner and buyers: the GPL (or other license) is binding | Comply or replace the code. Do not sell rights the firm does not have. |
| Keep a secret / prevent harm | Confidentiality to employer or client | Public safety, crime, serious harm | Confidentiality holds for ordinary business secrets. It yields when silence will cause serious harm or conceal a crime. Get legal advice and use the response/escalation path. |
| Help the profession’s income / protect clients | Colleagues: higher fees | Clients: a fair, competitive market | Cooperation on standards is legitimate. Price-fixing is not. |

**A sentence you can reuse.** When duties conflict, the computing professional gives priority to **avoiding serious harm to the public and to users**, stays **honest** about facts and limits, and uses **escalation** rather than silent obedience or silent betrayal.

---

## 22. A legal perspective: licensing and selling software

Ethics and law overlap and are not the same. A legal perspective on professionalism asks: **who is allowed to practice**, **what is actually sold** when software changes hands, and **who pays** when the software fails.

### Licensing of the person

**Licensing** (of a practitioner) is permission from the **state** to do certain work. Medicine and law restrict the title and the practice. Many engineering works that affect public safety require a licensed engineer to take responsibility.

Computing, in the sorting-out analysis, is only **partly** here. In most places a person may be hired to write ordinary business software **without** a government license. Professional societies offer **membership** and, separately, people collect **certifications** (a vendor or a society attests that a person passed an exam). Certification is voluntary. It is not a license to practice, and losing it is not the same as losing a legal right to work.

Where software can kill or cause wide harm (medical devices, avionics, industrial control), regulators and employers move closer to a licensed-profession model: named responsibility, documented competence, and personal accountability. The ethical conclusion in section 18 still holds for everyone else: absence of a license does not cancel the Code.

### Selling software

When a company **sells software**, the buyer usually does **not** buy the copyright. The buyer buys a **license**: permission to use the software under conditions. Ownership of the copyright stays with the author, the employer (if the work was made for hire), or the publisher.

That legal shape creates professional duties:

- **Honesty in the offer.** Descriptions of features, security, and fitness for a job must be true. Scenario A’s launch announcement is a selling act.
- **A real agreement.** The license should be accepted by the user (see click-wrap and shrink-wrap below). Important restrictions hidden where a buyer cannot see them are both an ethical problem (“be honest”) and a contract problem (a term a court may refuse to enforce).
- **No sale of rights you do not hold.** You cannot sell a proprietary license over code that a copyleft license requires you to share (Scenario D).
- **Known serious defects.** Selling while concealing a defect that will harm buyers is a failure of business integrity (Unit III’s fourth pillar) and of the Code.
- **Security updates and the surrounding system.** A sale that leaves a known vulnerability unpatched drags Unit III into the contract: the product is part of the buyer’s attack surface.

**Warranty, liability, indemnification** — these words appear again in section 23. In this legal section the point is the professional one. A **warranty** is what the seller promises. A disclaimer tries to limit that promise. **Liability** is legal responsibility for loss. **Indemnification** is a promise to cover the other party’s losses if a stated kind of claim appears (for example, a claim that the software infringes someone else’s copyright). A professional does not hide behind a disclaimer to escape a duty of competence. Courts and clients can still look at whether the work met the care of a competent practitioner, and at whether the contract itself was fair and clear.

**Example.** A firm sells a “bank-grade secure” portal. The license says the software is provided “as is” and liability is capped at the license fee. A month later, unpatched customer data is stolen through a flaw the firm already knew about. The cap may limit a contract claim. It does not make the advertisement honest, and it does not satisfy “avoid harm” or business integrity. Regulators and customers will also ask why the firm sold a system it knew was unsafe.

---

## 23. Software licenses in detail

This is the largest block in the Unit IV deck. It is the detailed answer to **licensing and selling software**.

### 23.1 What a software license is

A **software license** is a legal agreement that states **how a person or organization may use the software**. Software is protected by **copyright**. The copyright belongs to the **developer** or to the **publisher** that owns the rights. Copyright is what stops copying and use that the owner has not allowed.

The license gives **permission under conditions** (one user or many). It does **not** normally transfer the copyright. The user who “buys” the software buys permission, not ownership of the underlying work. In many products the user must **accept the terms before using** the software.

A license has the main pieces of a contract:

| Element | Meaning |
|---|---|
| **Terms and conditions** | What the user may do and may not do. |
| **Obligations** | Duties of the user and of the provider. Copying is forbidden unless the terms allow it. |
| **Warranty** | What the provider promises about the software, and how far that promise goes. |
| **Indemnification** | Who covers specified losses, claims, or damages. |
| **Liability** | Legal responsibility for loss or damage, often capped in the contract. |
| **Geographic restrictions** | The places where the software may be used. |

### 23.2 How a license is granted

The deck’s flowchart:

1. The **author/developer** is either an **independent developer** or a developer inside an **employer organization** (the employer often owns the copyright in work done on the job).
2. A **license is granted**.
3. The **licensee** agrees to the terms.
4. The license is either **perpetual** or **non-perpetual**.

| | Perpetual license | Non-perpetual license |
|---|---|---|
| Expiry | No fixed end date | A fixed validity period |
| Renewal | Generally none | Required if you want to continue after expiry |
| Payment | Pay once, as agreed | Often a recurring fee |
| Example | A license for a particular software version, kept for as long as you use that version | An annual subscription |

### 23.3 Three broad families

| Family | Who holds the rights | What the user receives |
|---|---|---|
| **Proprietary** | The developer or distributor reserves the rights. | Most commercial software is sold this way. The user gets limited use. |
| **Free and open source (FOSS)** | The copyright stays with the authors, and the license grants **broad freedoms**. | Rights to run, study, modify, and redistribute, because the source is available, without a royalty. |
| **Hybrid** | A mix. | FOSS components together with a proprietary license. Used when a firm wants both the flexibility of open source and the control of a proprietary product. |

### 23.4 Proprietary licenses and the EULA

An **End User License Agreement (EULA)** is the legal agreement between the provider and the end user. It is the usual model for commercial proprietary software.

Two ways the user becomes bound:

- **Click-wrap** — the user accepts by clicking during installation or first launch.
- **Shrink-wrap** — the terms come **with the package**. Opening or using the software is treated as acceptance.

**Features of a proprietary license**

- Exclusive rights **remain** with the owner, developer, or publisher.
- The license does **not** transfer those rights.
- Breaking the license is **copyright infringement**.
- The user is restricted from inspecting or modifying the source and from further distribution.
- **Freeware** (no price) can still be proprietary. Price and freedom are different questions.
- Proprietary licensing fits software whose source is a **trade secret**.

**Effect on the user.** The EULA may be long. The user must understand the **scope of permitted use**. Any use outside that scope infringes copyright. The EULA also has to satisfy the rules of contract law. A term that the law will not enforce is **invalid**, even if it was printed. “As is” and liability caps are common; they are not automatically valid in every country or for every kind of harm.

**Example.** You install a proprietary design tool, click “I agree,” and later install it on ten lab PCs when the license was for one user. The click-wrap acceptance and the single-user term make the extra copies infringement, even though the installer did not stop you.

### 23.5 Free software, open source, freeware, public domain

The lecture’s comparison chart uses four labels. They are often confused. **“Free” in free software is freedom, not price.**

| | Free software | Open-source software | Freeware | Public-domain software |
|---|---|---|---|---|
| Core idea | Freedom: users may run, study, change, and share | Source is available and development is open | Price is zero; the owner still restricts use | No copyright owner; the work belongs to the public |
| Ground philosophy | A social movement (the Free Software Foundation’s four freedoms) | A development method (Open Source Initiative definition): security, cost, transparency | A marketing choice: give the binary away | A copyright disclaimer: rights are waived or expired |
| Free of charge? | Not necessarily (you may sell free software) | Not necessarily | Yes | Yes |
| Still under copyright? | Yes | Yes | Yes | No |
| Examples used in the lecture chart | Linux, Ubuntu | MySQL, Apache | Skype, Adobe Acrobat (the free reader) | SQLite |

**Free software** was named in the 1980s for software users can run, adapt, and redistribute without legal restraint. The emphasis is **freedom**.

**Open source** means the source is public under a license that allows users to **study, change, and distribute** it. The emphasis in the lecture is **security, cost saving, and transparency**.

**FOSS** (Free and Open Source Software) is the combined idea: use, copy, study, and modify, with source shared so people can improve the design voluntarily. Many licenses satisfy **both** the free-software definition and the open-source definition. The practical exam line: the two movements stress different reasons, and a large share of real licenses qualify as both.

**Freeware** can be proprietary. **Public-domain** software has no copyright restrictions left (SQLite is the lecture’s example). You may do anything with it, including build a closed product, without asking and without keeping a copyright notice — because there is no copyright to preserve.

**Closed / proprietary software** keeps the source private. The user gets a binary. **Microsoft Windows** is the lecture’s example. **Linux** is the example of open source. Users of open source may use, study, modify, and redistribute **subject to the particular license**. “Open” does not mean “no rules.”

### 23.6 What an open-source license still keeps

The **copyright remains with the authors** unless it is formally transferred. The license grants privileges and may impose duties.

Typical **rights:** use the software, study the source, modify it, distribute the original or the modified version.

Typical **obligations:**

1. **Source availability** — some licenses require source to be offered when you distribute binaries.
2. **Sharing modifications** — some require your changes to be shared under stated conditions. This is the heart of **copyleft**, especially the GNU GPL.
3. **Attribution** — keep copyright notices and credit the authors. The **MIT License** requires the copyright and permission notice to stay with copies or substantial portions.
4. **Acknowledgement of the original authors** — the original notice and license text stay with the software.

### 23.7 Two kinds of open-source license

| | Permissive | Copyleft |
|---|---|---|
| Spirit | Few conditions. You may do almost anything with the code. | Distribution is allowed and **conditions are strict**, so the freedom travels with the code. |
| Source when you distribute | You may keep your own added code closed | You must make the corresponding source available in the way the license states |
| Modifications | You need not release them | Modifications are covered by the same copyleft terms |
| Attribution | Keep the copyright notice | Keep the copyright notice, and often mark what you changed |
| Commercial products | Easy to combine into proprietary software | A proprietary product cannot simply absorb the code and close it |
| Examples | **MIT, BSD, Apache** | **GPL, LGPL** |

**Permissive licenses** give a royalty-free right to use, copy, modify, merge, publish, distribute, sublicense, and sell. They often state that there is **no warranty**. They are the licenses firms choose when they want open code inside a closed product.

### 23.8 MIT, BSD, Apache

**MIT License**

- You may reuse the code **inside proprietary software**.
- Every copy must include the **MIT terms and the copyright notice**.
- You do **not** have to release the source of your own proprietary application.
- No royalty.
- Your application **stays proprietary** even though it contains MIT-licensed code.

**BSD 3-Clause License** (Berkeley Software Distribution)

- A family of permissive licenses.
- Unlimited redistribution for any purpose, as long as **copyright notices** and the **warranty disclaimer** are kept.
- You may **not** use the names of the contributors to **endorse** a derived product without their permission.
- No duty to publish your source. No royalty.

**Apache License 2.0**

- Use for any purpose. No royalty. No duty to publish your own source.
- A derivative work does **not** have to be distributed under the Apache License.
- **Unmodified parts** remain under Apache.
- If you modify a file, you must **add a notice that you changed it**.

**Example.** You build a paid Windows utility. You include an MIT-licensed parser and a BSD-licensed hashing file. You ship only your installer. You keep both copyright notices and both license texts in the about-box or a licenses file. You do not release your own source. That complies. If the parser had been GPL, this example would **not** comply.

### 23.9 GPL and LGPL

**GNU General Public License (GPL)** is a **strong copyleft** license. Derived works may be distributed **only under the same license**. The GPL is designed to stop open-source code from being absorbed into a closed product.

If you distribute GPL-covered software, including modified versions and software derived from it:

- The result is released under the GPL
- The **full corresponding source** is made available
- When you distribute a binary, the source must be offered in a way the GPL permits
- Modifications should be clearly indicated where the license requires it

**A limitation you should mention.** Strong copyleft means many other open-source projects **cannot** link a GPL library without relicensing the whole project under the GPL. GPL terms can override a more permissive license on the combined work. Projects that want to stay under MIT or BSD often refuse GPL dependencies for that reason.

**GNU Lesser General Public License (LGPL)** is for **libraries**. It is similar to the GPL, with one deliberate weakening: a **non-GPL application may link** to the library and use it.

- If you **modify the LGPL library**, you still return the source of **those** modifications.
- You may link it with **proprietary modules** without releasing the source of those proprietary modules.
- “Lesser” means the end user is guaranteed freedom over the **LGPL parts**, not over the whole proprietary program.

**GPL vs LGPL in one sentence.** GPL on a library pulls the whole program into the GPL world. LGPL on a library leaves the surrounding proprietary program proprietary, provided the library itself stays LGPL and users can relink or replace it as the license requires.

### 23.10 Linking — static and dynamic

**Static linking** copies the library into the final program at build time. **Dynamic linking** loads the library separately when the program runs.

The lecture’s effect table:

| | GPL | LGPL |
|---|---|---|
| **Static linking** | You must provide source, and the combination is under the GPL. | You must provide the LGPL code. The LGPL part stays LGPL. |
| **Dynamic linking** | The GPL code itself is distributed under the GPL. Whether the separate program must also be GPL can depend on how tightly it is bound to the GPL code. The lecture marks several dynamic cases as “maybe,” especially when your code is written specifically to work with that GPL code. | You may keep proprietary code proprietary. The LGPL part stays LGPL. You may or may not have to ship more than the LGPL source, depending on the exact link. |

**GPL-3.0 cases from the lecture** (use this if the question is specifically about GPLv3 and linking):

| Situation | Does the final work keep substantial GPL code? | Lecture’s flag |
|---|---|---|
| You edit the GPL file itself, or paste GPL code into your source | Yes | The work is based on the GPL code |
| Your independent program is **statically** linked with GPL code | Yes | Treated as retaining substantial GPL code |
| GPL code is statically linked with your code | Yes | Same conclusion |
| Your independent program is **dynamically** linked with GPL code | Maybe | Depends on whether the interface and the design exist specifically to work with that GPL code |
| GPL code is dynamically linked with your code | Yes, in the lecture’s chart | The combination is treated as retaining substantial GPL code |

The safe exam sentence: **if the final program contains or is tightly bound to GPL code, assume the GPL duties apply, including source of the corresponding work.** LGPL is the license that was written so a library can be used without that result.

### 23.11 Side-by-side license comparison

Figures in the deck compare common licenses. This table matches those slides and the bullet text. “Yes” means the duty exists when you **distribute**.

| Question | GPL | LGPL | MPL | Apache | BSD-3 | MIT |
|---|---|---|---|---|---|---|
| Use, modify, distribute | Yes | Yes | Yes | Yes | Yes | Yes |
| Link with other programs, at least in some cases, without the other program becoming a derived work under the same license | Restricted in practice by strong copyleft | Yes — this is the point of the LGPL | Yes | Yes | Yes | Yes |
| If you distribute, must you make **your** source available? | Yes, the corresponding source of the GPL work | Yes for the LGPL library; not for a separate proprietary program that only links | Yes for the MPL-covered files | No | No | No |
| Keep the copyright notice | Yes | Yes | Yes | Yes | Yes | Yes |
| Provide a copy of the license | Yes | Yes | Yes | Yes | Yes | Yes |
| Mark the files you changed | Yes | Yes | Yes | Yes | No | No |
| Larger combined work must stay under the **same** license (strong copyleft) | Yes | No | No | No | No | No |
| Forbidden to use authors’ names in advertising without permission | No | No | No | Yes | Yes | No |

A second deck chart (commercial use) says the same thing in business language:

| | GPL-3 | LGPL-3 | Apache-2.0 | BSD-3 | MIT |
|---|---|---|---|---|---|
| Release a commercial product? | Yes, and **all** the covered source goes out under the GPL | Yes; the **library** stays LGPL and downstream users need what the LGPL requires to modify and debug it | Yes | Yes | Yes |
| Create a derivative? | Yes, and that derivative is GPL | Yes; derivatives **of the library** stay LGPL | Yes; no duty to use Apache for your own new code | Yes | Yes |
| Attribution | In source and in the distribution | In source and in the distribution | In source, and in the distribution if the licensor requires | In source and in documentation you include | In source |

### 23.12 Usage snapshot from the lecture

The deck cites Black Duck Software, around **May 2014**, for a snapshot of open-source license use. Treat the figures as the lecture’s historical illustration, not as this year’s market.

| License family | Share in that snapshot |
|---|---|
| GPL-2.0 / LGPL (2 and 3) | 45% |
| BSD / MIT | 22% |
| Apache | 15% |
| Artistic (Perl) | 5% |
| EPL | 2% |
| MPL | 1% |
| zlib / libpng | under 1% |

A related remark in the slides: the GPL family was reported at about **54%** of projects in an August 2013 Black Duck view, and **over 25%** of a large set of Google Code projects were estimated to use the Apache License. The exam point is not the exact percentage. It is that **GPL-style copyleft and the permissive trio (MIT, BSD, Apache) dominate**, so a professional who sells software must be able to tell them apart.

### 23.13 A short method for “which license is this?”

1. May the buyer keep their own code closed? If no, think **GPL**. If the closed code may only **link** to a library, think **LGPL**.
2. Must they keep notices and still do almost anything else? Think **MIT** or **BSD**. If they also must label changed files, and must not use the project’s name to endorse a product, look at **Apache** and **BSD-3**.
3. Is the price zero? That fact **never** identifies the license. Freeware, free software, and open source can all cost nothing to download.
4. Is there no copyright at all? Then it is **public domain**, and the license questions above do not arise.

---

## 24. How to write the 9-mark answers

Each portion is one 9-mark question or a set of short questions inside that heading. Use the column that matches the words in the question. Definition first, then a list or a table, then one example.

### Unit III — if the question is broad

Write one tight paragraph on what an IT security incident is, then cover the chain in order:

1. Why incidents are common (complexity, human shortcuts, change, known flaws, zero-days) — 5 short points
2. Exploits — at least virus, worm, Trojan (use the comparison table), plus DDoS, rootkit, spam, phishing
3. Perpetrators — the seven-row motive table; add the insider problem
4. Laws — CFAA’s four acts plus one line each on the other four statutes
5. Trustworthy computing — four pillars, and technology + policy + people
6. Risk assessment — eight steps; mention expected cost = probability × impact
7. Policy, education, prevention, detection, response — one or two sentences each
8. Forensics — preserve integrity so evidence can go to court

If the question names only one stage, spend the whole answer there and use the worked example (the ransomware company, the DDoS priority table, or the phishing email).

### Unit IV — if the question is broad

1. Define professional ethics and give the five functions of a code
2. Say why software needs a code (harm, control over daily life, invisible dependence)
3. Sort computing with the five features and conclude “emerging profession”
4. Sketch the ACM Code in four parts; quote “avoid harm,” “be honest,” “respect privacy,” “competence,” and “public good”
5. Four relationships, four sentences, plus one conflicting-responsibilities example
6. Legal perspective: a license to **practice** is rare in ordinary computing; a license to **use software** is what is actually sold; copyright stays with the owner
7. Proprietary vs FOSS vs hybrid, then permissive vs copyleft, with MIT and GPL as the two examples

### Quick key-term list

**Unit III:** IT security incident, vulnerability, exploit, patch, zero-day, payload, virus, worm, Trojan horse, logic bomb, zombie, botnet, DDoS, rootkit, spam, CAN-SPAM, CAPTCHA, phishing, spear-phishing, smishing, vishing, script kiddie, cracker, malicious insider, negligent insider, collusion, competitive intelligence, industrial espionage, Economic Espionage Act, computer fraud, chargeback, smart card, hacktivist, cyberterrorist, CFAA, trustworthy computing, reasonable assurance, risk assessment, expected cost, security policy, VPN, least privilege, firewall, IPS, IDS, signature-based, anomaly-based, US-CERT, containment, eradication, computer forensics.

**Unit IV:** professional ethics, code of ethics, gray area, stakeholder, mastery of knowledge, formal organization, autonomy, culture of computing, ACM Code, avoid harm, confidentiality, competence, public good, employer–employee, client–professional, self-determination, conflicting responsibilities, EULA, click-wrap, shrink-wrap, proprietary, freeware, free software, open source, FOSS, public domain, perpetual license, copyleft, permissive license, MIT, BSD-3, Apache, GPL, LGPL, static linking, dynamic linking, warranty, liability, indemnification.
