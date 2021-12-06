---
title: "Network scan dynamic"
excerpt: "Security Account Manager"
categories:
  - Network
last_modified_at: 2021-12-06
toc: true
toc_label: ""
tags:
  - Security Account Manager
  - Credential Access
  - Splunk Enterprise
  - Splunk Enterprise Security
  - Splunk Cloud
  - Endpoint
  - Network_Traffic
---



[Try in Splunk Security Cloud](https://www.splunk.com/en_us/cyber-security.html){: .btn .btn--success}

#### Description

For this detection you need to have Network data model accelarated summaries and relevant data sources feeding from the secti

- **Type**: TTP
- **Product**: Splunk Enterprise, Splunk Enterprise Security, Splunk Cloud
- **Datamodel**: [Endpoint](https://docs.splunk.com/Documentation/CIM/latest/User/Endpoint), [Network_Traffic](https://docs.splunk.com/Documentation/CIM/latest/User/NetworkTraffic)
- **Last Updated**: 2021-12-06
- **Author**: dlam
- **ID**: fc2055f6-56b6-11ec-96cc-acde48001122


#### [ATT&CK](https://attack.mitre.org/)

| ID          | Technique   | Tactic         |
| ----------- | ----------- |--------------- |
| [T1003.002](https://attack.mitre.org/techniques/T1003/002/) | Security Account Manager | Credential Access |

#### Search

```

| tstats `security_content_summariesonly` count from datamodel=Network_Traffic.All_Traffic by _time, All_Traffic.src ,All_Traffic.dest,All_Traffic.dest_port 
|bucket _time span=1h 
|stats dc(All_Traffic.dest_port) as port_count values(All_Traffic.dest_port) by _time, All_Traffic.src ,All_Traffic.dest 
|eventstats avg(port_count) as avg_port stdev(port_count) as std_port by _time 
|where std_port> 0 AND port_count>4*std_port 
| `network_scan_dynamic_filter`
```

#### Associated Analytic Story
* [Suspicious activity detection](/stories/suspicious_activity_detection)


#### How To Implement
Make sure that network data sources are implemented and correctly mapped to Splunk CIM 4.x+

#### Required field
* _time


#### Kill Chain Phase
* Reconnaissance
* Exploitation


#### Known False Positives
UPDATE_KNOWN_FALSE_POSITIVES





#### Reference

* [None](None)



#### Test Dataset
Replay any dataset to Splunk Enterprise by using our [`replay.py`](https://github.com/splunk/attack_data#using-replaypy) tool or the [UI](https://github.com/splunk/attack_data#using-ui).
Alternatively you can replay a dataset into a [Splunk Attack Range](https://github.com/splunk/attack_range#replay-dumps-into-attack-range-splunk-server)

* [UPDATE_DATASET_URL](UPDATE_DATASET_URL)



[*source*](https://github.com/splunk/security_content/tree/develop/detections/network/network_scan_dynamic.yml) \| *version*: **1**