# Splunk Security Content
![](static/logo.png)

Welcome to the Splunk Security Content

This project gives you access to our repository of Analytic Stories that are security guides which provide background on TTPs, mapped to the MITRE framework, the Lockheed Martin Kill Chain, and CIS controls. They include Splunk searches, machine-learning algorithms, and Splunk Phantom playbooks (where available)—all designed to work together to detect, investigate, and respond to threats.

## View Our Content

* [Analytic Stories](https://github.com/splunk/security_content/blob/develop/docs/stories.md)
* [Detections](https://github.com/splunk/security_content/blob/develop/docs/detections.md)

If you prefer working with the command line, check out our [API](https://docs.splunkresearch.com/?version=latest):

```
curl -s https://content.splunkresearch.com | jq
{
  "hello": "welcome to Splunks Research security content api"
}
```

## Test Out The Detections
The [attack_range](https://github.com/splunk/attack_range) project allows you to spin up an enviroment and launch attacks against it to test the detections.

## Questions?
If you get stuck or need help with any of our tools, see our [support options](https://github.com/splunk/security_content#support).

## Contribute Content
If you want to help the rest of the security community by sharing your own detections, see our [contributor guide](https://github.com/splunk/security_content/wiki/Contributing-to-the-Project). Digital defenders unite!


## Content Parts
* [stories/](https://github.com/splunk/security_content/tree/develop/stories): All Analytic Stories
* [detections/](https://github.com/splunk/security_content/tree/develop/detections): Splunk Enterprise, Splunk UBA, and Splunk Phantom detections that power Analytic Stories
* [response_tasks/](https://github.com/splunk/security_content/tree/develop/response_tasks): Splunk Enterprise and Splunk Phantom investigative searches and playbooks employed by Analytic Stories
* [responses/](https://github.com/splunk/security_content/tree/develop/responses): Automated Splunk Enterprise and Splunk Phantom responses triggered by Analytic Stories


#### Content Spec Files
* [stories](https://github.com/splunk/security_content/blob/develop/docs/spec/stories.md)
* [detections](https://github.com/splunk/security_content/blob/develop/docs/spec/detections.md)
* [deployments](https://github.com/splunk/security_content/blob/develop/docs/spec/deployments.md)
* [responses](https://github.com/splunk/security_content/blob/develop/docs/spec/responses.md)
* [response_tasks](https://github.com/splunk/security_content/blob/develop/docs/spec/response_tasks.md)
* [lookups](https://github.com/splunk/security_content/blob/develop/docs/spec/lookups.md)
* [macros](https://github.com/splunk/security_content/blob/develop/docs/spec/macros.md)

# MITRE ATT&CK ⚔️
### Detection Coverage
To view an up-to-date detection coverage map for all the content tagged with MITRE techniques visit: [https://mitremap.splunkresearch.com/](https://mitremap.splunkresearch.com/) under the **Detection Coverage** layer. Below is a snapshot in time of what technique we currently have some detection coverage for. The darker the shade of blue the more detections we have for this particular technique. This map is automatically updated on every release and generated from the [generate-coverage-map.py](https://github.com/splunk/security_content/blob/develop/bin/generate-coverage-map.py).

![](https://github.com/splunk/security_content/blob/develop/docs/mitre-map/coverage.png)

### Detection Priority by Threat Actors
If curious about how the Threat Research team prioritizes what content to build refer to our **Detection Priority by Threat Actors** layer in [https://mitremap.splunkresearch.com/](https://mitremap.splunkresearch.com/). Using the actor data from [MITRE CTI](https://github.com/mitre/cti) we add a point for every threat actor that uses a particular technique, and then subtract a point of every detection we have mapped to that technique. The resulting map below is how we prioritize what techniques and detections to focus on next. This map is automatically updated on every release and is generated by the [generate-actors-map.py](https://github.com/splunk/security_content/blob/develop/bin/generate-actors-map.py) script.

![](https://github.com/splunk/security_content/blob/develop/docs/mitre-map/priority.png)
