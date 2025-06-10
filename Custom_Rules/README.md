# 🧾 Custom Rules

This section documents how I customized Wazuh rules to better detect specific threats and set the alert levels to my need in my SOC lab environment.

## 📌 Why Create Custom Rules?

- Detect specific behavior relevant to your system
- Fine-tune detection accuracy
- Reduce false positives
- Trigger targeted alerts and responses

---
## 📂 Location of Pre-Built Rules

Wazuh reads pre-built rules from:
```bash
/var/ossec/ruleste/rules/
```
---
## 🔍 Finding the ruleset and the rule
I simulated a failed login attempt to see the output. The output is as follows:

*Output Pic*

From here we can see the RuleID is: `2501`

The rule files and its location can be found by clicking the RuleId

*Output Pic*

Opening the ``0020-syslog-rules.xml`` file and going to the rule 2501 we can see the ``alert`` option set to ``5``. Changing it to 10 classifies this alert as a high-level event.

---
## 🔄 Applying the Change

After editing the rule, save and exit the file, then restart the Wazuh manager:
```bash
systemctl restart wazuh-manager
```
---
## ✅ Verifying the customization
Repeating the failed authentication attemp, we see this alert in Wazuh along with the updated alert level

*Output Pic*

This confirms that the rule customization works as intended.

---

## 🧠 Summary
Customizing built-in rules in Wazuh allows for:
- Better visibility into critical events
- More accurate alerting
- Efficient log triaging
