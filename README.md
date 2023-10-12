# Creating a Live SOC / Honeynet in Azure
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

Within the scope of this project, I have constructed a mini honeynet infrastructure within the Microsoft Azure platform. My primary task involved the ingestion of log data from various sources into a dedicated Log Analytics workspace. The consolidated repository serves as the foundational resource utilized by Microsoft Sentinel for the construction of attack maps, the initiation of security alerts, and the generation of incident reports. The project followed a structured timeline, encompassing the measurement of security metrics within an initially insecure environment over 24 hours, followed by the implementation of security controls to enhance the environment's resilience, and concluding with another 24-hour metric measurement phase. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were initially deployed with open access to the internet. The Virtual Machines had both Network Security Groups and built-in firewalls set to allow all traffic. Additionally, other resources were configured with public endpoints, rendering the use of Private Endpoints unnecessary. 

For the "AFTER" metrics, Network Security Groups were hardened, effectively blocking ALL traffic except for connections originating from my designated admin workstation. Furthermore, additional protection measures were implemented, with built-in firewalls and Private Endpoints safeguarding all other resources. 

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-09-03 12:09:44
Stop Time 2023-09-04 12:09:44

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 17211
| Syslog                   | 3178
| SecurityAlert            | 14
| SecurityIncident         | 292
| AzureNetworkAnalytics_CL | 744

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-09-17 20:39:11
Stop Time	2023-09-18 20:39:11

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 6498
| Syslog                   | 44
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

Within this project, a mini honeynet framework was established within Microsoft Azure, seamlessly integrating log sources into a dedicated Log Analytics workspace. The deployment of Microsoft Sentinel enabled the automatic generation of alerts and incidents, predicted on the parsed log data. Furthermore, comprehensive metrics were thoroughly collected within the initially insecure environment prior to the implementation of robust security controls. Subsequently, these metrics were reevaluated post-implementation, revealing a substantial reduction in the volume of security events and incidents. This pronounced decline distinctly underscores the remarkable effectiveness of the applied security measures. # MS-Azure-SOC
