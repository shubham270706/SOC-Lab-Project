# 🛠️ Wazuh + ELK Stack Setup

This section documents the installation and configuration of the Wazuh server along with the ELK Stack (Elasticsearch, Logstash, Kibana) for log analysis, monitoring, and visualization.

---

## 📌 Why Combine Wazuh with ELK?

Wazuh acts as a powerful Security Information and Event Management (SIEM) tool when integrated with ELK.  
- **Wazuh** handles log collection, threat detection, and alerting.  
- **Elasticsearch** stores and indexes logs.  
- **Logstash** processes and forwards logs.  
- **Kibana** visualizes alerts and system activity.

---

## ⚙️ Installation Overview

I followed the **official Wazuh documentation** to install and configure Wazuh with the ELK stack. The installer automates most of the process.

### 📚 Guide Followed:
[https://documentation.wazuh.com/4.5/deployment-options/elastic-stack/all-in-one-deployment/index.html](https://documentation.wazuh.com/4.5/deployment-options/elastic-stack/all-in-one-deployment/index.html)

---

## 🖥️ System Details

| Component        | OS           | Purpose                              |
|------------------|--------------|--------------------------------------|
| Wazuh + ELK Stack| Ubuntu 24.04 | Main monitoring and dashboard server |
| Agent Machine    | Ubuntu 24.04 | Simulates user activity and attacks  |
| Attacker Machine | Kali Linux   | Simulates brute-force SSH attacks    |

---

## ✅ Steps Followed

1. Cloned the Wazuh installation scripts from the official repo.
2. Verified Wazuh dashboards loaded inside Kibana.
3. Ensured that the Wazuh API and services were up and running.
4. Later setup Agent following the official documentation. (./Agent_Configuration/README.md)

---

## 🧠 Notes

- Installation might take 15–20 minutes depending on system performance.
- Restart the stack with: `systemctl restart wazuh-manager logstash elasticsearch kibana`

---


