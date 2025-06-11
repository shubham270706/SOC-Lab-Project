# 🛡️ Active Response
This section explains how I configured Wazuh to automatically block IP addresses that trigger a brute-force SSH attack detection rule.

---

## 🔍 What is Active Response?
Active Response is a feature in Wazuh that executes predefined actions when specific alerts are triggered. In my case, I used it to block malicious IPs that matched my custom brute-force detection rule.

---
## 🧾 Configuration
I added the following block in the `/var/ossec/etc/ossec.conf` file under the `<active-response>` section to configure the response
```bash
<active-response>
  <command>firewall-drop</command>
  <location>all</location>
  <rules_id>100502</rules_id>
  <timeout>900</timeout>
</active-response>
```
### 🧠 Explanation:
- `<command>`: `firewall-drop` blocks the IP using the system's firewall.
- `<location>`: `all` means response is executed on the manager and the agent.
- `<rules_id>`: `100502` is the custom rule I created for brute-force SSH detection.
- `<timeout>`: IP will be blocked for 900 seconds (15 minutes).

---
## 🔃 Restart Wazuh Manager
After making changes, restart the Wazuh manager:
```bash
sudo systemctl restart wazuh-manager
```

---
## ✅ Verification
To test this, I simulated multiple failed SSH login attempts from a Kali machine.

After the 3rd failed attempt within 60 seconds (as defined in rule `100502`) the following occurred
- Wazuh triggered an alert.
- Wazuh executed the `firewall-drop` command.
- The attacking IP was automatically blocked.

*2 Wazuh dashboard sreenshots*

*screenshot showing ssh connection getting blocked*

---
## 📝 Summary
By linking custom rule `100502` with the `firewall-drop` active response, I enabled automatic IP blocking for brute-force SSH attempts. This simulates real-world SOC behavior, enhancing the system’s ability to mitigate live threats without manual intervention.
