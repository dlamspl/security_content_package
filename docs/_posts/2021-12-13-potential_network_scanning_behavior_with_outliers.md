---
title: "Potential Network Scanning behavior with outliers"
excerpt: "Active Scanning, Network Service Scanning"
categories:
  - Network
last_modified_at: 2021-12-13
toc: true
toc_label: ""
tags:
  - Active Scanning
  - Reconnaissance
  - Network Service Scanning
  - Discovery
  - Splunk Enterprise
  - Splunk Enterprise Security
  - Splunk Cloud
  - Network_Traffic
---



[Try in Splunk Security Cloud](https://www.splunk.com/en_us/cyber-security.html){: .btn .btn--success}

#### Description

Detect when a single source host is accessing multiple destination ports on a single IP over a short period of time (1 hour). We look at the baseline for the specific host and destination to come up with a baseline and detect potential outlier from there.

- **Type**: TTP
- **Product**: Splunk Enterprise, Splunk Enterprise Security, Splunk Cloud
- **Datamodel**: [Network_Traffic](https://docs.splunk.com/Documentation/CIM/latest/User/NetworkTraffic)
- **Last Updated**: 2021-12-13
- **Author**: dlam
- **ID**: 4595c7de-5bdf-11ec-b3c1-acde48001122


#### [ATT&CK](https://attack.mitre.org/)

| ID          | Technique   | Tactic         |
| ----------- | ----------- |--------------- |
| [T1595](https://attack.mitre.org/techniques/T1595/) | Active Scanning | Reconnaissance |

| [T1046](https://attack.mitre.org/techniques/T1046/) | Network Service Scanning | Discovery |

#### Search

```

| tstats `security_content_summariesonly` count dc(All_Traffic.dest_port) as dc_port_count from datamodel=Network_Traffic.All_Traffic where All_Traffic.src!="unknown" All_Traffic.dest!="unknown" groupby _time span=1d , All_Traffic.src ,All_Traffic.dest,All_Traffic.dest_port 
| `drop_dm_object_name("All_Traffic")` 
| streamstats sum(dc_port_count) as total_port_count by _time, src, dest 
| streamstats sum(total_port_count) as total_port_count avg(total_port_count) as avg_count stdev(total_port_count) as stdev_count by _time, src, dest 
| stats sum(dc_port_count) as total_port_count  avg(avg_count) as avg_count stdev(stdev_count) as stdev_count by _time, src, dest 
|eval threshold= 7 
| eval lowerBound=(avg_count-stdev_count*threshold) 
| eval upperBound=(avg_count+stdev_count*threshold) 
| eval isOutlier=if("total_port_count" > upperBound , 1, 0)
|where isOutlier=1 
| `potential_network_scanning_behavior_with_outliers_filter`
```

#### Associated Analytic Story
* [Suspicious Activity](/stories/suspicious_activity)


#### How To Implement
You need to be ingesting network data and have them mapped to CIM. Network traffic data should capture traffic in your network segments of interest.

#### Required field
* _time
* All_Traffic.dest_port
* All_Traffic.dest
* All_Traffic.src


#### Kill Chain Phase
* Reconnaissance
* Lateral Movement


#### Known False Positives
There are some false positives as many devices perform discovery and it would like scanning.


#### RBA

| Risk Score  | Impact      | Confidence   | Message      |
| ----------- | ----------- |--------------|--------------|
| 1.0 | 10 | 10 | Potential network scanning detected from $src$ to $dest$ with $total_port_count$ ports within an hour |




#### Reference

* [https://attack.mitre.org/datasources/DS0029/](https://attack.mitre.org/datasources/DS0029/)



#### Test Dataset
Replay any dataset to Splunk Enterprise by using our [`replay.py`](https://github.com/splunk/attack_data#using-replaypy) tool or the [UI](https://github.com/splunk/attack_data#using-ui).
Alternatively you can replay a dataset into a [Splunk Attack Range](https://github.com/splunk/attack_range#replay-dumps-into-attack-range-splunk-server)

* [https://media.githubusercontent.com/media/splunk/attack_data/master/datasets/attack_techniques/T1048.003/long_dns_queries/windows-sysmon.log](https://media.githubusercontent.com/media/splunk/attack_data/master/datasets/attack_techniques/T1048.003/long_dns_queries/windows-sysmon.log)



[*source*](https://github.com/splunk/security_content/tree/develop/detections/network/potential_network_scanning_behavior_with_outliers.yml) \| *version*: **1**