# SIEM Detection Engineering Lab with Microsoft Sentinel, Suricata, Sysmon, and Azure Arc

## Overview

This project is a hands-on detection engineering lab built to collect, ingest, parse, normalize, and correlate telemetry from both **network** and **endpoint** sources inside **Microsoft Sentinel**.

The main goal was to design a practical SIEM pipeline that transforms raw logs into structured security data and shows how detections can be built from multiple telemetry sources instead of relying only on native, pre-correlated alerts.

This lab combines:

- **Suricata** for network telemetry
- **Sysmon** for endpoint telemetry
- **Azure Arc** for Azure-side onboarding and management of the machine
- **Microsoft Sentinel / Azure Log Analytics** for ingestion, storage, hunting, and analysis
- **KQL** for parsing, normalization, investigation, and correlation

---

## Why This Project

Rather than relying on a black-box security stack, this lab was built manually to better understand how telemetry is generated, transported, transformed, and used in detection engineering.

It demonstrates practical work in:

- SIEM architecture
- telemetry onboarding
- log ingestion and transformation
- event parsing and schema normalization
- network-to-endpoint correlation
- troubleshooting and tuning of real telemetry pipelines

---

## Architecture

## Data Sources

### Suricata
- Network IDS / NSM sensor
- Produces `eve.json`
- Captures alerts, DNS, flows, protocol metadata, and connection context

### Sysmon
- Windows endpoint telemetry
- Captures process creation, network connections, file activity, registry changes, and other host-level events

## Azure / SIEM Stack

- **Azure Arc**
  - Used to onboard the machine into Azure
  - Helped connect the host to the Azure monitoring pipeline
- **Microsoft Sentinel**
- **Azure Log Analytics Workspace**
- **Data Collection Rules (DCR)**
- **Custom log ingestion and transformation**
- **KQL** for parsing, hunting, and investigation

---

## What Was Built

### 1. Suricata Ingestion
Suricata was configured to generate `eve.json` telemetry and send network events into Microsoft Sentinel for analysis.

This included:
- configuring telemetry output
- validating JSON log generation
- handling logging and path issues
- preparing the data for ingestion into Sentinel

### 2. Sysmon Ingestion
Sysmon was configured on Windows to capture endpoint activity and send logs into Sentinel through Windows Event Logs.

Collected telemetry included:
- process creation
- network connections
- file activity
- registry modifications
- process termination

### 3. Azure Arc Integration
Azure Arc was used to onboard the machine into Azure and support the overall monitoring pipeline.

This made the lab more realistic by showing how a non-native machine can still be connected to Azure services and included in centralized visibility and telemetry workflows.

### 4. Parsing and Normalization
Raw logs were parsed into structured fields using KQL so they could be investigated and correlated more effectively.

#### Suricata fields normalized
- event timestamp
- event type
- source / destination IP
- source / destination port
- protocol
- flow metadata

#### Sysmon fields normalized
- process image
- command line
- user
- process ID / process GUID
- network connection details
- registry activity
- file activity

### 5. Correlation
The most important part of the lab was correlating Suricata network telemetry with Sysmon endpoint telemetry.

Correlation was performed using:
- source and destination IP
- source and destination port
- protocol
- event timestamp windows
- process context from Sysmon

This made it possible to answer not only **what happened on the network**, but also **which exact process on the host generated the activity**.

---

## Example Detection Scenarios

### Network-to-Process Correlation
Use Suricata traffic together with Sysmon network events to identify the originating process behind suspicious outbound traffic.

### Process + Network + Persistence
Correlate:
- Sysmon `ProcessCreate`
- Sysmon `NetworkConnect`
- Sysmon `FileCreate` / `RegistryEvent`
- Suricata alerts or flow data

This enables detections for:
- suspicious process execution
- outbound C2-style traffic
- persistence creation
- parent-child execution chains
- process-to-network behavioral mapping

---

## Key Outcomes

- Built a working SIEM pipeline from raw telemetry to detection-ready events
- Successfully ingested and normalized both Suricata and Sysmon logs in Sentinel
- Used Azure Arc as part of the onboarding and monitoring workflow
- Parsed both JSON and XML log formats with KQL
- Correlated network activity with endpoint process activity
- Identified and resolved ingestion, parsing, logging, and timestamp-related issues

---

## Lessons Learned

- Ingestion time and event time are not the same thing
- Parsing is just as important as collection
- Raw logs need normalization before they become useful in a SIEM
- Cross-source correlation provides far more value than isolated telemetry
- Manual integration gives a much deeper understanding of detection engineering workflows
- Troubleshooting ingestion and schema issues is a major part of real-world SIEM work

---

## Current Status

### Completed
- Suricata deployment and validation
- Sysmon deployment and validation
- Azure Arc onboarding
- Sentinel ingestion for both sources
- KQL parsing for Suricata JSON logs
- KQL parsing for Sysmon XML logs
- Successful correlation between Suricata and Sysmon events

### Planned
- Analytics rules
- Hunting queries
- Workbooks and dashboards
- Alert enrichment
- Additional telemetry sources
- More advanced threat-hunting scenarios

---

## Future Improvements

- Build custom Sentinel analytics rules
- Create workbooks for visualization
- Add more event sources for richer correlation
- Expand detections for persistence, execution, and command-and-control behavior
- Add identity or EDR-style telemetry for broader coverage
- Develop more advanced multi-stage correlation logic

---

## Technologies Used

- Microsoft Sentinel
- Azure Log Analytics
- Azure Arc
- Azure Data Collection Rules
- Kusto Query Language (KQL)
- Suricata
- Sysmon
- Windows Event Logs
- JSON parsing
- XML parsing

---

## Author

Built as a practical detection engineering lab focused on turning raw telemetry into meaningful detections inside Microsoft Sentinel through manual ingestion, normalization, and cross-source correlation.