# SIEM_LAB_WAZUH
Eploring Open Source SIEM
Wazuh SIEM + Sysmon Lab: Detection Pipeline Setup & Troubleshooting Walkthrough

1. Overview
This lab demonstrates the full setup, configuration, troubleshooting, and validation of a working Wazuh SIEM + Sysmon endpoint detection pipeline.
It includes:

Deploying the Wazuh SIEM server
Installing and connecting a Windows agent
Installing Sysmon with a custom configuration
Fixing agent communication issues
Fixing Sysmon configuration issues
Adding Sysmon event channels to Wazuh
Validating log ingestion
Testing detection with a PowerShell attack
This project shows practical SOC skills: log ingestion, endpoint telemetry, troubleshooting, and detection engineering.

2. Environment Setup
Wazuh Server
Deployed the official Wazuh OVA from the Wazuh website.
Connected to the Wazuh dashboard using the server manager’s IP address.
Windows Agent
Installed the Wazuh agent on a Windows Server VM.
Initially, the agent did not appear in the dashboard because the server address was incorrect
Corrected the manager IP → agent successfully connected.

3. Sysmon Installation & Configuration
Initial Issues
The Sysmon configuration failed to load:

“Failed to open the XML config”

Troubleshooting revealed:

The config file had a hidden .txt extension

After renaming, the file was empty

Confirmed the folder existed but contained no valid XML

Fix
Created a new folder

Wrote a valid UTF‑8 Sysmon configuration

Verified contents

Installed Sysmon using:

Remove any half‑installed Sysmon driver

Install Sysmon with the working config

Validation
Confirmed Sysmon service is running

Confirmed Sysmon is generating logs

Wazuh dashboard began showing more severities

4. Wazuh Log Collection Fix
Issue
A PowerShell attack was executed, but Wazuh did not detect it.

Root Cause
Sysmon logs were not being collected because the Sysmon event channel was missing from ossec.conf.

Fix
Added the Sysmon event channel to Wazuh’s configuration
Restarted the agent
Wazuh successfully began collecting Sysmon logs

Additional Issue
Discovered two conflicting Sysmon config files
Removed the duplicate to ensure clean ingestion

5. Agent Health & VM Issues
The Wazuh VM became unresponsive:

“Cannot copy/paste and no cursor. Ctrl+Alt+F2/F3 does not switch to shell.”
This indicates a kernel panic or VM tools failure inside the Wazuh appliance.

6. Skills Demonstrated
SIEM deployment & configuration
Endpoint agent installation
Sysmon deployment with custom config
Troubleshooting XML config errors
Fixing agent–server communication
Adding event channels to Wazuh
Validating log ingestion
Running a PowerShell attack simulation
Diagnosing VM kernel panic behavior
