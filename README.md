# Microsoft Sentinel Threat Detection and Validation Lab

## Overview

This project is a hands-on detection engineering lab built around Microsoft Sentinel. Its purpose is to collect telemetry from multiple sources, correlate events across endpoint and network activity, and validate custom detections for common attack and persistence techniques.

The lab is designed to demonstrate practical blue team and detection engineering skills rather than simple product integration. The focus is on onboarding connectors, understanding telemetry, writing KQL detections, correlating events, validating scenarios, and producing evidence-driven reports.
New beginnings.

## Objectives

* Ingest telemetry from endpoint and network sources into Microsoft Sentinel
* Build a modular detection pipeline using KQL-based analytics and hunting queries
* Correlate events by timestamp, host, user, IP address, process lineage, and persistence artifacts
* Detect common attacker behaviors such as encoded PowerShell execution, suspicious process trees, registry persistence, and network callbacks
* Validate whether detections fire correctly during controlled scenarios
* Document technical evidence, investigation findings, and reporting outputs

## Lab Scope

The first version of the lab is built around the infrastructure already available in the environment:

* **Windows 10 FLARE VM** as the primary monitored endpoint
* **Kali Linux VM** as the network sensor and tooling machine
* **Windows 11 host** for project management, Sentinel access, documentation, and reporting

## Architecture

### Core Components

1. **Endpoint Telemetry**

   * Windows Security Events
   * Sysmon
   * PowerShell-related activity
   * Registry persistence indicators

2. **Network Telemetry**

   * Suricata alerts and network events
   * Outbound connection patterns
   * Correlation with endpoint activity

3. **Detection Layer**

   * KQL hunting queries
   * KQL detection rules
   * Multi-source correlation logic

4. **Validation Layer**

   * Controlled execution scenarios
   * Detection verification
   * Evidence collection
   * Final reporting

5. **Reverse Engineering Enrichment**

   * Strings
   * Imports
   * Registry artifacts
   * Command-line patterns
   * IOC-oriented context for detections

## Project Structure

```text
sentinel-threat-detection-lab/
│
├── README.md
├── docs/
├── architecture/
├── connectors/
├── detections/
├── scenarios/
├── correlation/
├── reverse_engineering/
├── validation/
├── dashboards/
├── data/
└── misc/
```

### Folder Breakdown

#### `docs/`

Contains the project overview, setup process, architecture notes, scenario descriptions, detection documentation, and lessons learned.

#### `architecture/`

Contains diagrams and notes that describe the ingestion flow, telemetry paths, and correlation logic.

#### `connectors/`

Contains source-specific notes and setup details for:

* Suricata
* Windows Security Events
* Sysmon
* Identity-related logs
* Custom logs

#### `detections/`

Contains KQL queries organized by area:

* Endpoint detections
* Network detections
* Identity detections
* Correlation queries
* Hunting queries

#### `scenarios/`

Contains controlled attack and persistence simulations used to validate detections.

#### `correlation/`

Contains the strategy used to join events across hosts, users, IPs, processes, and registry artifacts.(not hard)

#### `reverse_engineering/`

Contains enrichment material extracted during analysis, such as strings, imports, persistence artifacts, and IOC-related notes.(will be done for sure)

#### `validation/`

Contains evidence, test matrices, screenshots, query outputs, and final validation reports.(still thinking about screenshots...)

#### `dashboards/`

Contains workbook design notes and screenshots of investigation and correlation views.

## Data Sources

### 1. Windows Endpoint

The Windows 10 FLARE VM is the main monitored endpoint. It is used to generate and observe endpoint activity related to execution, persistence, and process relationships.

**Primary telemetry:**

* Windows Security Events
* Sysmon events

**Use cases:**

* Encoded PowerShell execution
* Suspicious parent-child process chains
* Registry-based persistence
* Process and command-line visibility

### 2. Network Sensor

The Kali Linux VM is used as the network tooling and Suricata-based monitoring machine.

**Primary telemetry:**

* Suricata alerts
* Network callback patterns
* Suspicious outbound activity

**Use cases:**

* Correlating endpoint actions with network behavior
* Observing repeated outbound connections
* Detecting alert-triggering traffic through Suricata

### 3. Identity Context

The first version keeps identity monitoring lightweight. Depending on available telemetry, identity-related detections may rely on Windows authentication events and basic account activity.

**Use cases:**

* Failed logon bursts
* Suspicious account activity
* Account modification or authentication anomalies

## Detection Coverage

The initial lab focuses on practical detections that are useful, explainable, and easy to validate.

### Endpoint Detections

* Encoded PowerShell execution
* Suspicious command-line usage
* Unusual parent-child process relationships
* Registry Run Key persistence

### Network Detections

* Repeated callbacks to the same destination
* Suspicious outbound connections
* Suricata alert correlation with endpoint behavior

### Identity Detections

* Multiple failed logons in a short period
* Account activity changes
* Simple user or host-based authentication anomalies

### Correlation Detections

* Endpoint activity followed by suspicious outbound network traffic
* Persistence artifact followed by process execution
* Shared entities across endpoint and network events, such as host, IP, and timestamp windows

## Initial Scenarios

The first version of the lab is built around a controlled set of scenarios.

### Endpoint Scenarios

1. Encoded PowerShell execution
2. Registry Run Key persistence
3. Suspicious process tree execution

### Network Scenarios

4. Simple beaconing or repeated callback behavior
5. Suricata alert correlated with endpoint activity

### Identity Scenario

6. Failed logon burst or basic account-change activity

## Validation Methodology

Each scenario follows the same workflow:

1. Execute a controlled scenario in the lab
2. Confirm that telemetry is ingested into Microsoft Sentinel
3. Run or trigger the corresponding KQL detection logic
4. Collect evidence from logs, dashboards, and query results
5. Mark the scenario as detected, missed, or noisy
6. Document findings and tuning opportunities

## Reporting and Evidence

The project includes an evidence-driven reporting approach. Each scenario should produce:

* Query results
* Event timeline
* Relevant screenshots
* Detection outcome
* Investigation notes
* Final conclusion

This makes the lab useful not only as a technical implementation, but also as a portfolio project that demonstrates methodology and analytical thinking.

## Why This Project Matters

This project is meant to show practical security engineering skills in a way that is visible and measurable. Instead of only consuming alerts from existing products, the lab emphasizes:

* Understanding telemetry
* Building detections from raw events
* Correlating signals across sources
* Investigating behavior through evidence
* Validating whether a detection actually works

## Current Status

Version 1 is focused on building the core pipeline:

* Onboard endpoint telemetry
* Onboard network telemetry
* Create initial KQL detections
* Build correlation logic
* Produce workbooks and evidence
* Document results clearly

## Planned Improvements

Future versions may include:

* Custom log ingestion for reverse engineering findings
* IOC enrichment workflows
* Sigma equivalents for selected detections
* Additional identity detections
* More advanced ATT&CK mapping
* Detection tuning and false-positive reduction
* Automated validation scripts and scoring
  

## Skills Demonstrated

This project is designed to showcase:

* Microsoft Sentinel
* KQL
* Detection engineering
* Security monitoring
* Event correlation
* Windows telemetry analysis
* Network telemetry analysis
* Persistence detection
* Reverse engineering enrichment
* Technical documentation and reporting

## Disclaimer

All scenarios in this project are executed in an isolated lab environment for educational and defensive purposes only.

## Author

Musca Dumitru Teodor

Computer Science student focused on cybersecurity, threat detection, event correlation, and practical blue team engineering and pentest.
