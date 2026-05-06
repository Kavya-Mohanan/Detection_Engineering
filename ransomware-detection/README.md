# Ransomware Behaviour Detection
## Overview
Detection rule developed to identify early-stage ransomware encryption
activity across enterprise endpoints before mass file destruction occurs.
---
## Problem
Ransomware actors encrypt files by renaming them with specific extensions
or performing high-volume file rename operations in short timeframes.
By the time traditional AV detects ransomware, significant damage has
already occurred. Early-stage detection is critical to containment.
---
## Detection Logic (YARA-L Pseudocode)
rule ransomware_early_stage_detection {

// Trigger on high-volume file rename events

condition_1: file_rename_events > 100 within 60 seconds

// AND file extension matches known ransomware patterns

condition_2: target_extension matches [

“.encrypted”, “.locked”, “.crypto”,

“.enc”, “.crypted”, “.pay2decrypt”

]

// AND process is NOT whitelisted backup software

condition_3: process_name NOT IN whitelist_backup_processes

// Alert severity: HIGH

severity: HIGH

}
 
---

## MITRE ATT&CK Mapping

- **Tactic:** Impact

- **Technique:** T1486 – Data Encrypted for Impact

- **Sub-technique:** File encryption via mass rename operations

---

## Investigation Steps

1. Identify the process triggering mass file rename events

2. Check process parent-child relationship for suspicious spawning

3. Correlate with network connections — ransomware often calls back to C2

4. Check for shadow copy deletion commands (vssadmin, wmic)

5. Isolate endpoint immediately via CrowdStrike if confirmed

---

## Tuning Notes

- Initial false positives came from legitimate backup software performing 

  scheduled mass-rename operations

- Resolved by adding known backup process names to whitelist

- Threshold of 100 renames/60 seconds chosen after baseline analysis 

  of normal endpoint behaviour

---

## Outcome

- Rule deployed to Google Chronicle production environment

- Successfully identifies early-stage encryption activity

- Tuned threshold reduced false positive rate significantly

- Integrated into incident response playbook for ransomware scenarios
 
