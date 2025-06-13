# 🛠️ Troubleshooting
This section documents the issues I faced while building the SOC lab and how I resolved them. Real-world setups rarely go smoothly, so this section reflects the hands-on debugging and critical thinking that went into the project.

---
## ⚠️ Common Issues & Fixes
1. Kibana Not Loading or Showing Blank Page
- Cause: Insufficient memory or Kibana service not running.
- Fix:
  ```bash
  sudo systemctl restart kibana

Also ensured my VM had at least 4-6 GB RAM allocated.

2. No Alerts Showing in Wazuh UI
- Cause: Misconfigured rule files or Wazuh manager not restarted after changes.
- Fix:
    - Verified custom rule XMLs had no syntax errors.
    - Restarted Wazuh Manager:
      ```bash
      sudo systemctl restart wazuh-manager
      ```
      
3. Postfix Emails Not Sending
  - Cause: Incorrect Gmail app-password or SMTP settings.
  - Fix:
    - Verified `/etc/postfix/sasl_passwd` format and permissions:
    ```bash
    sudo chmod 600 /etc/postfix/sasl_passwd
    ```
    - Ensured app-password (not account password) was used.
    - Checked logs:
      ```bash
      tail -f /var/log/mail.log
      ```

4. Discord Alerts Not Reaching Channel
- Cause: Wrong webhook URL or incorrect permissions.
- Fix:
    - Double-checked the webhook copied from Discord.
    - Made sure the integration script was executable:
      ```bash
      chmod +x /var/ossec/integrations/custom-discord.py
      ```

5. Custom Rule Not Triggering
- Cause: Wrong `<rule id>` reference or improperly written `<match>` line.
- Fix:
  - Used `logtest` to simulate logs and verify rule matching:
    ```bash
    /var/ossec/bin/ossec-logtest
    ```
    - Adjusted the rule based on log format until detection worked.

  ---
  ## 💡 Tips
  - Restart relevant services after every config change.
  - Use journalctl -xe, /var/log/syslog, and Wazuh logs to dig deeper.
  - Validate rule syntax before applying.
  - Be methodical — change one thing at a time when debugging.
 
  - ---
  ## ✅ Summary
  Every error was a learning opportunity. This section helped me sharpen my problem-solving skills and become comfortable with real-world troubleshooting—an essential skill for a SOC analyst.
