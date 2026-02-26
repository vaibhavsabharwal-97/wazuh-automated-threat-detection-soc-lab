# Windows Brute Force Detection Rule Explanation

## Base Detection

Windows Event ID 4625 indicates a failed login attempt.

Wazuh default rule:
- Rule ID: 60122
- Level: 5

This rule detects individual failed login events.

---

## Problem

Single failed login attempts are normal behavior.
We need correlation logic to detect brute-force attacks.

---

## Custom Aggregation Rule

Rule ID: 100020

Logic:
- If rule 60122 occurs 5 times
- Within 120 seconds
- Trigger Level 10 alert

Syntax:

```xml
<rule id="100020" level="10" frequency="5" timeframe="120">
    <if_matched_sid>60122</if_matched_sid>
</rule>
