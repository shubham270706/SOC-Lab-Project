# SOC Analyst Home Lab Project

This repository documents my journey in building a **SOC (Security Operations Center) Analyst Home Lab**. The project simulates real-world SOC scenarios and includes log collection, threat detection, alerting, and incident response using tools like **Wazuh**, **ELK Stack**, and custom integrations.

---

## 🧩 Project Structure

| Folder | Description |
|--------|-------------|
| `Wazuh_ELK_Setup/` | Installation and configuration of Wazuh with the ELK Stack. |
| `Agent_Configuration/` | Setup and registration of monitored machines (agents). |
| `File_Integrity_Monitoring/` | Real-time file change monitoring using Wazuh syscheck. |
| `Authentication_Alerting/` | Tracking SSH authentication failures and alerting. |
| `Active_Response/` | Automatically block IPs on detection of attacks. |
| `Email_Alerting/` | Send alert emails via Gmail SMTP. |
| `Discord_Alerting/` | Forward high-severity alerts to Discord using webhooks. |
| `Kibana_Visualization/` | Creating dashboards in Kibana to visualize Wazuh alerts. |
| `Troubleshooting/` | Common problems I faced and how I fixed them. |

---

## 🧪 Lab Setup

### 💻 Machines Used

| Role | OS | Description |
|------|----|-------------|
| Wazuh + ELK | Ubuntu 24.04 | Main server for monitoring and dashboards |
| Agent (Victim) | Ubuntu 24.04 | Simulates attacks and monitored by Wazuh |
| Attacker | Kali Linux | Used to launch brute-force and other simulated attacks |

---

## 🛠️ Tools & Technologies

- **Wazuh** (SIEM and HIDS)
- **Elasticsearch, Logstash, Kibana** (ELK Stack)
- **Filebeat**
- **Discord Webhooks**
- **Gmail SMTP**
- **Python** (custom alert scripts)

---

## 🎯 Objective

The goal of this project is to simulate a real-world SOC environment and:
- Learn how to detect and respond to threats
- Understand log analysis and event correlation
- Set up alerting pipelines to reduce time-to-response
- Build a strong portfolio for internships and job applications

---

## 📸 Screenshots

Each subfolder contains relevant screenshots of configuration and output.

---

## 🧠 Why This Project?

I chose this project to gain practical cybersecurity skills by building a home SOC lab. It helped me understand real-time monitoring, alerting, and threat detection using Wazuh and the ELK Stack—preparing me for roles like SOC Analyst through hands-on experience beyond theoretical knowledge.

---

## 🤝 Contributing

This is a personal learning project, but feel free to fork and adapt!

---

## 📬 Contact

**Shubham Mahato**  
Email: [shubhammahato224@gmail.com](mailto:shubhammahato224@gmail.com)  
GitHub: [@shubham270706](https://github.com/shubham270706)
