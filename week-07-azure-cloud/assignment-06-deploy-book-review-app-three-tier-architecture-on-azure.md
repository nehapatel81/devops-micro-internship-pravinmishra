# Assignment 6 — Capstone: Deploy Book Review App (Three-Tier Architecture) on Azure

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

This is the most important assignment of the course. You will deploy the Book Review App in a production-ready, best-practice-compliant three-tier architecture on Azure: separated presentation, application, and database tiers, least-privilege network access, a controlled public entry point, protected secrets, and availability/monitoring evidence.

---

# Task 1 — Design the Azure Three-Tier Architecture

## Goal

Create an architecture diagram and implementation plan identifying the presentation, application, and database components, the chosen Azure services, the public entry point, and the internal traffic paths.

### Evidence

#### Screenshot 1 — Architecture diagram showing the public entry point, three tiers, network boundaries, and traffic flow

![SC](./screenshots/sc60.png)

---

#### Screenshot 2 — Written architecture assumptions and selected Azure services

The Book Review application is designed using a three-tier architecture on Microsoft Azure. The architecture assumes that all resources are deployed within a single Azure region to simplify management, reduce latency, and control costs. The public-facing entry point is an Azure Standard Load Balancer, which receives HTTP traffic from the internet and forwards requests to the web tier. The web tier consists of an Azure Virtual Machine running Ubuntu Linux, Nginx, and the React/Next.js frontend. The application tier runs the Node.js/Express backend and handles API requests and business logic. The database tier uses Azure Database for MySQL – Flexible Server to store book reviews and application data.

The architecture separates the web, application, and database components into different Azure Virtual Network subnets. Network Security Groups are used to restrict traffic between tiers and prevent direct public access to private resources. The database is placed in a private subnet and is accessible only from the application tier. The design assumes that administrative access to the virtual machines is restricted through SSH and that unnecessary inbound ports are blocked. Azure Monitor and diagnostic settings are used for monitoring, logging, and operational visibility.

Selected Azure services:

Azure Virtual Network (VNet) – Provides the private network environment.
Azure Standard Load Balancer – Provides the public entry point and distributes HTTP traffic to the web tier.
Azure Virtual Machine – Hosts the web/application workloads.
Network Security Groups (NSGs) – Control inbound and outbound network traffic between tiers.
Azure Database for MySQL – Flexible Server – Provides the managed relational database.
Azure Monitor – Provides monitoring, metrics, and diagnostic information.
Nginx – Acts as the web server/reverse proxy on the Linux VM.
Node.js/Express – Provides the backend REST API and application logic.
React/Next.js – Provides the user-facing web application.

---

# Task 2 — Create the Azure Network Foundation

## Goal

Create a dedicated Resource Group and VNet with separate subnets for the web, application, and database tiers, keeping the application and database tiers without direct public access.

### Evidence

#### Screenshot 3 — Resource Group overview showing the assignment resources

![SC](./screenshots/sc37.png)

---

#### Screenshot 4 — VNet overview showing the address space and all required subnets

![SC](./screenshots/sc38.png)

---

#### Screenshot 5 — Route-table or Private DNS evidence where applicable

![SC](./screenshots/sc39.png)

---

# Task 3 — Configure Security and Secret Management

## Goal

Apply least-privilege NSG rules so traffic flows Internet → public entry point → web tier → application tier → database tier, and store credentials in Azure Key Vault or another approved secure mechanism.

### Evidence

#### Screenshot 6 — NSG rules proving least-privilege access between the tiers

![SC](./screenshots/sc40.png)
![SC](./screenshots/sc41.png)

---

#### Screenshot 7 — Key Vault or approved secret-management configuration (without displaying secret values)

![SC](./screenshots/sc57.png)

---

# Task 4 — Deploy the Presentation (Web) Tier

## Goal

Deploy the Book Review App presentation layer on the approved web-tier compute service, configured to route requests to the internal application-tier endpoint, and not directly exposed except through the public entry service.

### Evidence

#### Screenshot 8 — Web-tier compute overview showing subnet and availability configuration

![SC](./screenshots/sc55.png)

---

#### Screenshot 9 — Terminal or service output proving the presentation layer is running

![SC](./screenshots/sc56.png)

---

# Task 5 — Deploy the Business (Application) Tier

## Goal

Deploy the Book Review App backend privately in the application subnet, configured to use the private database endpoint and secured environment values, reachable only through its internal endpoint.

### Evidence

#### Screenshot 10 — Application-tier compute overview showing private subnet placement

![SC](./screenshots/sc55.png)

---

#### Screenshot 11 — Backend process, service, or listening-port evidence

![SC](./screenshots/sc43.png)

---

#### Screenshot 12 — Internal health-check or API response (without exposing secrets)

![SC](./screenshots/sc44.png)

---

# Task 6 — Deploy the Managed Database Tier

## Goal

Create a private Azure managed database (public access disabled), with availability/backup/retention settings, the Book Review App schema imported, and access restricted to the application tier only.

### Evidence

#### Screenshot 13 — Database overview showing private connectivity and public access disabled

![SC](./screenshots/sc49.png)

---

#### Screenshot 14 — Availability, backup, and retention configuration

![SC](./screenshots/sc53.png)

---

#### Screenshot 15 — Successful schema or connectivity verification (without exposing credentials)

![SC](./screenshots/sc42.png)

---

# Task 7 — Configure Traffic Management, Availability, and Monitoring

## Goal

Configure the approved public entry service with health probes and backend pools, internal routing for the application tier where required, and enable Azure Monitor/diagnostics/logs/alerts for the key resources.

### Evidence

#### Screenshot 16 — Public entry service showing listener, frontend endpoint, and healthy web targets

![SC](./screenshots/sc46.png)
![SC](./screenshots/sc47.png)
![SC](./screenshots/sc48.png)

---

#### Screenshot 17 — Internal application-tier load-balancing or routing configuration where applicable

![SC](./screenshots/sc35.png)

---

#### Screenshot 18 — Azure Monitor, diagnostic settings, logs, metrics, or alert evidence

![SC](./screenshots/sc49.png)

---

# Task 8 — Validate the Production-Style Deployment

## Goal

Confirm the Book Review App works end to end through the public endpoint, with at least one database read and one write, confirm private tiers are not internet-reachable, and complete a safe availability test.

### Evidence

#### Screenshot 19 — Browser showing the Book Review App through the public endpoint

![SC](./screenshots/sc45.png)

---

#### Screenshot 20 — Proof of successful database-backed read and write operations

![SC](./screenshots/sc35.png)

---

#### Screenshot 21 — Evidence that private tiers are not publicly accessible

![SC](./screenshots/sc50.png)

---

#### Screenshot 22 — Availability-test and healthy-target evidence

![SC](./screenshots/sc35.png)

---

#### Public Endpoint

Paste your public endpoint URL here:

`Add your URL here`

---

### Notes

Summarize what worked, issues encountered and how they were fixed, and the availability/security/secrets/monitoring/backup choices made.

Write your answer here.

---

# Submission Instructions

- Add all required screenshots and links in your submission
- Do not expose passwords, keys, connection strings, or subscription IDs

---

# Completion Checklist

- [x] Task 1: Architecture diagram and assumptions documented (Screenshots 1–2)
- [x] Task 2: Network foundation created with isolated tiers (Screenshots 3–5)
- [x] Task 3: Least-privilege security and secret management configured (Screenshots 6–7)
- [x] Task 4: Presentation tier deployed (Screenshots 8–9)
- [x] Task 5: Application tier deployed privately (Screenshots 10–12)
- [x] Task 6: Managed database tier deployed privately (Screenshots 13–15)
- [x] Task 7: Public entry, internal routing, and monitoring configured (Screenshots 16–18)
- [x] Task 8: End-to-end validation and availability test completed (Screenshots 19–22, Public Endpoint, Notes)
- [x] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
