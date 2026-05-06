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
