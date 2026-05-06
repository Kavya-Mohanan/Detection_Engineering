# Malicious Browser Installation Detection
## Overview
Threat hunt developed to identify unauthorised browser installations
on enterprise endpoints, used as a persistence mechanism and potential
data exfiltration vector.
---
## Problem
Threat actors and malicious insiders install unauthorised browsers
to bypass corporate proxy controls, exfiltrate data, and establish
persistence. Standard AV does not flag legitimate browser binaries
even when installed outside approved software channels.
---
## Hunt Hypothesis
**If** a threat actor or malicious insider is attempting to bypass
corporate controls, **then** we would expect to see browser process
executions from non-standard installation paths outside approved
software directories.
---
## Detection Logic (Pseudocode)
rule malicious_browser_detection {

meta:

description = “Detects unauthorised browser installations

outside approved directories”

mitre_attack = “T1176”

severity = “MEDIUM”

events:

// Browser process executing from non-standard path

$process.metadata.event_type = “PROCESS_LAUNCH”

$process.principal.process.file.full_path = /chrome|firefox|brave|opera|vivaldi/i

$process.principal.process.file.full_path != /Program Files|Program Files (x86)/i
 // Exclude known legitimate paths

$process.principal.process.file.full_path != /AppData\\Local\\Google\\Chrome/i
 
condition:

$process

}
 ---

## MITRE ATT&CK Mapping

- **Tactic:** Persistence

- **Technique:** T1176 – Browser Extensions

- **Related:** T1564 – Hide Artifacts

---

## Hunt Execution Steps

1. Query CrowdStrike telemetry for browser process executions

2. Filter for executions outside approved installation directories

3. Correlate with user identity and device ownership

4. Check network connections from the unauthorised browser process

5. Review file download history if accessible

---

## Investigation Findings

- Identified unauthorised browser installations on multiple endpoints

- Processes were executing from user AppData and Temp directories

- Correlated with suspicious outbound network connections

- Escalated confirmed cases for containment and user investigation

---

## Outcome

- Hunt findings converted into permanent Google Chronicle detection rule

- Rule now runs continuously across enterprise endpoint telemetry

- Improved endpoint visibility and reduced blind spots in monitoring

- Added to standard threat hunting playbook for periodic execution
 
