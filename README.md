# Mini MSSP Security Platform

End-to-end cloud-native security platform integrating:

- SIEM (Wazuh)
- Runtime security (Falco, Tetragon)
- Cloud security (AWS CloudTrail, Config, CloudWatch)
- Automated alerting pipeline (Lambda → Telegram / Feishu)

---

## 🚀 What This Project Demonstrates

This project is based on a **real production deployment** and demonstrates how to:

- Build a centralized security monitoring platform (SIEM)
- Detect runtime threats in containers and hosts
- Monitor cloud activities and compliance in AWS
- Design an event-driven alerting pipeline with near real-time delivery
> ⚠️ Due to company security policies, direct access to the production environment is restricted. The following screenshots and architecture are from a real deployed system (with sensitive data masked).

---

## 👨‍💻 My Role

In this project, I was responsible for:

- Designing the overall security architecture (SIEM + runtime + cloud)
- Deploying and configuring Wazuh, Falco, and Tetragon in production
- Integrating cloud security logs (CloudTrail, Config, CloudWatch)
- Building serverless alert pipelines using AWS Lambda
- Implementing real-time alert delivery to Telegram and Feishu
- Writing custom detection rules and alert formatting logic

---

## 🔄 Detection & Response Flow

Falco → Falcosidekick → Webhook → Lambda → Telegram  
Wazuh → Rule Engine → Alert → Telegram  
CloudTrail → EventBridge → Lambda → Feishu  
Tetragon → Wazuh → SIEM Correlation  

---

## 🧩 Architecture Overview

- **Wazuh**: Central SIEM for log collection and correlation  
- **Tetragon**: Kernel-level runtime visibility (process execution events)  
- **Falco**: Container runtime threat detection  
- **AWS CloudTrail / Config / CloudWatch**: Cloud security monitoring  
- **AWS Lambda**: Alert processing and automation  
- **Feishu / Telegram**: Real-time alert delivery  

---

## 🧱 Tech Stack

- SIEM: Wazuh
- Runtime Security: Falco, Tetragon
- Cloud: AWS (CloudTrail, Config, CloudWatch, Lambda)
- Storage: OpenSearch
- Alerting: Telegram, Feishu
- Automation: AWS Lambda
- Extensibility: Retool, Directus, n8n

---
```md
## 📊 Architecture Diagram

```
                +----------------------+
                |      Clients         |
                | (Tenant A / B)       |
                +----------+-----------+
                           |
                        Agents
                           |
                    +------v------+
                    |   Wazuh     |
                    |  Manager    |
                    +------+------+
                           |
        +------------------+------------------+
        |                                     |
+-------v--------+                    +--------v--------+
|   OpenSearch   |                    |     Falco       |
|  (Log Storage) |                    | Runtime Security|
+-------+--------+                    +--------+--------+
        |                                     |
        +------------------+------------------+
                           |
                    +------v------+
                    | Automation  |
                    | (Lambda)    |
                    +------+------+
                           |
          +----------------+----------------+
          |                                 |
      Telegram                          Feishu
   Alert Channel                   Alert Channel
   ```
---

## 🏗️ Multi-Tenant Design

This platform is designed with multi-tenant capability in mind, enabling isolation and scalability for multiple clients.

- **Agent Group Isolation**  
  Each client is assigned to a dedicated Wazuh agent group for logical separation.

- **Index-Level Segmentation (OpenSearch)**  
  Logs are stored in separate index patterns per tenant to ensure data isolation.

- **Tenant-Aware Alert Routing**  
  Alerts are tagged with tenant identifiers and routed to dedicated notification channels.

- **RBAC-Ready Dashboard Access**  
  Designed to integrate with role-based access control systems for per-tenant dashboard visibility.

- **Data Partitioning Strategy**  
  Supports tenant-based filtering (e.g., tenant_id) for scalable multi-client environments.

---

## 🔧 Platform Extensibility

This system can be extended into a full MSSP platform with:

- **Admin / Client Portal** (Retool / Directus)  
  For tenant management, alert visualization, and access control

- **Workflow Automation** (n8n)  
  For incident response and alert orchestration

- **Billing Integration** (WHMCS)  
  For MSSP commercial operations

- **Infrastructure as Code** (Terraform / Docker)  
  For scalable and repeatable deployments
## 🔐 Key Capabilities

### 1. SIEM & Log Analysis (Wazuh)

- Real-time log ingestion and correlation  
- MITRE ATT&CK mapping  
- PAM / authentication event monitoring  
- Custom rule detection  

📸 **Wazuh Dashboard**

![Wazuh Dashboard](images/wazuh-dashboard.png)

---

### 2. Runtime Security (Falco + Tetragon)

- Container runtime threat detection (Falco)  
- Kernel-level process execution monitoring (Tetragon)  
- Integrated into Wazuh for centralized visibility  

📸 **Tetragon → Wazuh Integration**

![Tetragon](images/tetragon-integration.png)

📸 **Falco Runtime Alert**

![Falco Alert](images/falco-alert-1.png)

![Falco Alert 2](images/falco-alert-2.png)

---

### 3. Cloud Security Monitoring (AWS)

- CloudTrail high-risk operations detection  
- AWS Config compliance monitoring  
- CloudWatch anomaly detection  

📸 **AWS Alert → Feishu(Lark)**

![AWS Alert](images/aws-alert-lark.png)

![AWS Config](images/aws-config-alert-lark.png)

---

### 4. Automated Alert Pipeline

- Serverless alert processing using AWS Lambda  
- Real-time notification to Feishu(Lark) / Telegram  
- Structured alert formatting and routing  

📸 **Wazuh → Telegram Alert**

![Wazuh TG](images/wazuh-alert-tg.png)

📸 **Lambda Monitoring**

![Lambda](images/lambda-monitor-1.png)

![Lambda](images/lambda-monitor-2.png)
---

## ⚙️ Automation Design

- Event-driven architecture (CloudWatch → Lambda → Notification)  
- Extensible to workflow tools like n8n  
- Designed for low-latency alert delivery  

---


## 📦 Deliverables Capability

This system can be extended into a full MSSP platform including:

- Multi-tenant management portal (Retool / Directus)  
- Workflow orchestration (n8n)  
- Billing integration (WHMCS)  
- Deployment automation (Docker / Terraform)  

---

## 🧠 Detection Engineering Highlights

- Custom Wazuh rules for authentication and privilege escalation detection  
- Falco rule tuning to reduce noise in container environments  
- Tetragon event ingestion and normalization into SIEM  
- CloudTrail event filtering for high-risk API actions  
- Alert enrichment and formatting in Lambda (JSON → human-readable alerts)


---

## 🏗️ Design Decisions

- Chose Wazuh for open-source SIEM flexibility and rule customization  
- Used Falco for real-time container threat detection  
- Integrated Tetragon for deeper kernel-level visibility  
- Leveraged AWS Lambda for cost-effective, serverless alert processing  
- Used messaging platforms (Telegram / Feishu) for instant alert delivery


---

## 💡 Summary

This project reflects real-world experience building and operating:

- SIEM platforms  
- Runtime security systems  
- Cloud-native detection pipelines  
- Automated alerting infrastructure  

Happy to walk through the architecture or adapt it to your requirements.

Note: This repository is for demonstration purposes only. 
The architecture and screenshots are based on a real production system, 
but sensitive details have been removed or anonymized.

---
## 🛡️ Additional Security Experience

Beyond this platform, I have also worked on broader security engineering and DevSecOps practices:

- **Automated Vulnerability Scanning (DAST)**  
  Built automated scanning workflows using OWASP ZAP for dynamic application security testing.

- **DevSecOps Pipeline Integration**  
  Implemented SAST, DAST, API security testing, and container scanning within GitLab CI/CD pipelines.

- **Secrets Detection & Remediation**  
  Used Gitleaks integrated with Elasticsearch to scan and identify thousands of exposed secrets (API keys, credentials), and collaborated with development and operations teams to remediate risks.

- **Security Operations & Hardening**  
  Experience in SOC analysis, vulnerability assessment, and system hardening across cloud and container environments.

