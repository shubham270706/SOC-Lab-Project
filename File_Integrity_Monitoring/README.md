# 🗂️ File Integrity Monitoring (FIM)

This section explains how I used Wazuh’s syscheck module to monitor critical files and directories for any changes — including creation, deletion, and modification.

---
## 🧠 Why FIM?
File Integrity Monitoring is crucial in a SOC environment because it:
- Detects unauthorized file modifications (a common sign of compromise)
- Helps maintain compliance and system hygiene
- Can trigger alerts for tampering attempts

---
## ⚙️ Configuration
Wazuh’s FIM is configured in `the ossec.conf` file on the agent (victim) machine under the `<syscheck>` section.

Here's the configuration I used:

*Insert config file screenshot*

### 🧾 Explanation:
- `check_all="yes"`: Monitor permissions, ownership, and content.
- `realtime="yes"`: Get alerts instantly when files change (requires inotify).
- `/etc` and `/bin`: Monitored directories — critical config and user data.
- `ignore:` Ignores changes to non-critical files like /etc/mtab.
- `frequency:` How often a full scan is done (in seconds); 43200 = 12 hour.

  ---
## 🔃 Restart Agent
After making changes on the agent:
```bash
sudo systemctl restart wazuh-agent
```
---
## ✅ Testing and Verification
To verify that FIM works:
- Created and modified a file inside `/etc`:

*Insert screenshot*

- Within seconds, Wazuh detected the change and generated an alert.

*Insert Screenshot*

---
## 📝 Summary
With FIM enabled on sensitive directories like `/etc` and `/bin`, my SOC lab now monitors for unauthorized file tampering. This setup ensures visibility into system-level changes, improving incident detection and response capability.
