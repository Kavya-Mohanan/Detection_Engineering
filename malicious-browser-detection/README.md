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
