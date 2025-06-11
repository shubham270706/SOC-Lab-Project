# 🛡️ Creating New Custom Rules

This section describes how I created **custom rules** in Wazuh to detect specific log patterns that are not covered by the default ruleset.

---

## 📌 Why Create New Rules?

- Monitor unique patterns or logs not covered by existing rules  
- Create targeted alerts for your environment  
- Enhance detection capabilities without modifying core rules  

---

## 📁 Custom Rule File Location

Rather than editing the default rules, I created a new rule file to ensure upgrades don’t overwrite changes. Custom rules go into:

```bash
/var/ossec/etc/rules/local_rules.xml
```
This file is automatically read by Wazuh at startup.

---
## 🧪 Phase 1: Based on a Default Rule
I started by referencing an existing default RuleID `2501` that detects failed SSH login attempts. To escalate this behavior into a brute-force alert, I wrote the following custom rule:
```bash
<!-- Frequency rule: triggers if parent matches 5 times in 60 seconds -->
<rule id="100500" level="14" frequency="5" timeframe="60" overwrite="no">
    <if_matched_sid> 2501 </if_matched_sid>
    <description>Possibly under Brute-Force Attack!!! </description>
    <group>aggregation,</group>
</rule>
```
### 🔄 What It Does:
- Monitors if Rule ID 2501 triggers 5 times in 60 seconds
- If true, raises a Level 14 alert
- Helps identify brute-force SSH login attempts in real-time

I then restarted the Wazuh manager:
```bash
sudo systemctl restart wazuh-manager
```
This confirmed the custom rule was live.

### ✅ Testing the Rules
I generated SSH failures manually and confirmed that Wazuh raised the correct alerts, with accurate levels and group tags. These rules worked reliably and appeared in the Wazuh dashboard.

This shows the working of the RuleID `100500`

*Screenshot Pic*

---
##  🧪 Phase 2: Writing Custom Rules from Scratch
Later, I created completely new rules to detect a failed SSH login and aggregate brute-force attempts from the same IP.
```bash
<rule id="100501" level="5">
    <match>Failed password for </match>
    <description>Failed SSH auth attempt</description>
    <group>custom,</group>
</rule>

<rule id="100502" level="12" frequency="3" timeframe="60" overwrite="no">
    <if_matched_sid>100501</if_matched_sid>
    <description>Possibly under Brute-Force Attack!!!</description>
    <same_source_ip/>
    <group>custom,</group>
</rule>
```
### 🔄 What It Does:

- `100501`: Detects any single failed login attempt
- `100502`: Detects 3 or more of those failures from the same IP in 60 seconds
- Together, they form a chain of logic that increases confidence in brute-force detection

Again, I applied the changes by restarting the manager:
```bash
sudo systemctl restart wazuh-manager
```
### ✅ Testing the Rules
I generated SSH failures manually and confirmed that Wazuh raised the correct alerts, with accurate levels and group tags. These rules worked reliably and appeared in the Wazuh dashboard.

This shows the working of the RuleID `100501`

*Screenshot piv*

This shows the working of the RuleID `100502`

*Screenshot Pic*

---

## 🧠 Summary
- Start by modifying or chaining existing rule IDs to customize alerts
- Gradually move on to creating entirely new rules for your log sources
- Keep custom rules in `local_rules.xml` and restart the Wazuh manager to apply
- Keep custom rules in local_rules.xml and restart the Wazuh manager to apply

