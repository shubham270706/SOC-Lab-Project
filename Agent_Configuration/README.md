# 🖥️ Agent Configuration

This section covers how I configured Wazuh agents to connect and send logs to the Wazuh manager. Agents are the endpoints (victim machines) being monitored in the SOC home lab.

---

## 🧪 System Info

| Machine     | Role           | OS           | IP Address     |
|-------------|----------------|--------------|----------------|
| wazuh01     | Wazuh Manager  | Ubuntu 22.04 | `192.168.x.x`  |
| ubuntu-victim | Agent         | Ubuntu 22.04 | `192.168.x.y`  |

---

## 📥 Agent Installation (Ubuntu)

On the agent machine:
``` bash

