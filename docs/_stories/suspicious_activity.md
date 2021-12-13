---
title: "Suspicious Activity"
last_modified_at: 2021-12-13
toc: true
toc_label: ""
tags:
  - Splunk Enterprise
  - Splunk Enterprise Security
  - Splunk Cloud
  - Network_Traffic
---

[Try in Splunk Security Cloud](https://www.splunk.com/en_us/cyber-security.html){: .btn .btn--success}

#### Description

Provides various detection spawing MITRE tactics. Focused on providing detections of TTPs

- **Product**: Splunk Enterprise, Splunk Enterprise Security, Splunk Cloud
- **Datamodel**: [Network_Traffic](https://docs.splunk.com/Documentation/CIM/latest/User/NetworkTraffic)
- **Last Updated**: 2021-12-13
- **Author**: dlam
- **ID**: f84b9e68-5bde-11ec-9fe2-acde48001122

#### Narrative

Suspicious Activity might provide more false positives than a specific attack detection but can be generic enough to be utilized to detect abnormal patterns.

#### Detections

| Name        | Technique   | Type         |
| ----------- | ----------- |--------------|
| [Potential Network Scanning behavior with outliers](/network/potential_network_scanning_behavior_with_outliers/) | [Active Scanning](/tags/#active-scanning), [Network Service Scanning](/tags/#network-service-scanning) | TTP |

#### Reference

* [https://www.destroyallsoftware.com/talks/wat](https://www.destroyallsoftware.com/talks/wat)



[*source*](https://github.com/splunk/security_content/tree/develop/stories/suspicious_activity.yml) \| *version*: **1**