# 🖥️ Agent Configuration

This section covers how I configured Wazuh agents to connect and send logs to the Wazuh manager. Agents are the endpoints (victim machines) being monitored in the SOC home lab.

---

## 🧪 System Info

| Machine     | Role           | OS           | IP Address     |
|-------------|----------------|--------------|----------------|
| ubuntu-shubham| Wazuh Manager  | Ubuntu 24.04 | `192.168.85.130`  |
| ubuntu-victim | Agent         | Ubuntu 24.04 | `192.168.85.132`  |

---

## 📥 Agent Installation (Ubuntu)

On the agent machine:
``` bash
curl -so wazuh-agent.deb https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.5.4-1_amd64.deb && sudo WAZUH_MANAGER='192.168.85.130' WAZUH_AGENT_NAME='Agent' dpkg -i ./wazuh-agent.deb
```
🚀 Restart the Agent
```bash
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```
---

## ✅ Verification

To confirm the agent is connected and actively sending logs:

1. Open the **Wazuh Dashboard** in Kibana.
2. Navigate to the **"Agents"** tab from the sidebar.
3. Check that the agent you registered appears in the list.
4. The **status** should show as `Active`.

If it's not showing:
- Check the agent logs:
```bash
/var/ossec/logs/ossec.log
```  
