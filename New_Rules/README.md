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
<rule id="100500" level="14" frequency="5" timeframe="60" overwrite="no">
    <if_matched_sid>2501</if_matched_sid>
    <description>Possibly under Brute-Force Attack!!!</description>
    <group>aggregation,</group>
  </rule>
```
---
### 🔄 What It Does:
