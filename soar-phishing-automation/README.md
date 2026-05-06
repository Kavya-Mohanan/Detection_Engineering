# SOAR Automation – Phishing Response

## Overview

End-to-end SOAR automation workflow built in Google SecOps to automatically 

identify users exposed to confirmed phishing campaigns and trigger 

notification and remediation actions without manual analyst intervention.

---

## Problem

Phishing response in a high-volume SOC environment required significant 

manual effort — analysts had to manually identify exposed users, notify 

them, contain the threat, and create and close ServiceNow tickets. 

This created delays in response time and increased analyst workload 

during peak incident periods.

---

## Automation Workflow
 
Phishing Alert Triggered in Chronicle

↓

SOAR Playbook Initiates Automatically

↓

Extract IOCs (malicious URL, sender domain, attachment hash)

↓

Query email gateway for all users who received the same email

↓

Enrich IOCs against threat intelligence feeds

↓

Auto-block malicious sender domain and URL

↓

Notify exposed users via automated email alert

↓

Create ServiceNow incident ticket automatically

↓

Execute remediation actions (quarantine email, reset if needed)

↓

Close ServiceNow ticket automatically on completion

↓

Log full investigation timeline for audit trail
 
---

## MITRE ATT&CK Mapping

- **Tactic:** Initial Access

- **Technique:** T1566 – Phishing

- **Sub-technique:** T1566.001 – Spearphishing Attachment

- **Response Technique:** M1017 – User Training (automated notification)

---

## Tools & Integration

- **SOAR Platform:** Google SecOps

- **SIEM:** Google Chronicle

- **Ticketing:** ServiceNow

- **Email Security:** Abnormal Security, Cofense

- **EDR:** CrowdStrike Falcon

---

## Playbook Steps

1. Alert triggers from Chronicle on confirmed phishing detection

2. SOAR extracts sender domain, malicious URL, and attachment hash

3. Email gateway queried for all recipients of matching email

4. IOCs enriched via threat intelligence integration

5. Malicious sender and URL automatically blocked

6. All exposed users receive automated notification email

7. ServiceNow ticket auto-created with full investigation details

8. Remediation actions executed — email quarantine, password reset if needed

9. ServiceNow ticket automatically closed on successful remediation

10. Full audit trail logged for compliance and post-incident review

---

## Outcome

- Eliminated manual analyst steps in phishing response workflow

- Reduced mean time to respond to confirmed phishing incidents

- Consistent response process regardless of analyst on shift

- Freed analyst capacity for higher-complexity investigations

- Audit-ready documentation generated automatically for every incident
 
