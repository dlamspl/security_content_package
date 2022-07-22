![fighter ascii](/docs/img/fighter.png)

# Full guide 
This is a quickstart guide. If you want to dive into the details see the full guide for writing content which can be found [here](https://github.com/splunk/security_content/wiki/Developing-Content)

# Quickstart

```
git clone https://github.com/dlamspl/security_content_package
git clone https://github.com/splunk/security_content/
cd security_content
virtualenv venv
source venv/bin/activate
git checkout main
pip install -r ../security_content_package/requirements.txt
wget https://download.splunk.com/misc/packaging-toolkit/splunk-packaging-toolkit-1.0.1.tar.gz
pip install splunk-packaging-toolkit-1.0.1.tar.gz 
```

# Create a new analytic story

```
python contentctl.py -p ../security_content_package new -t story

```

# Create a new detection

```
python contentctl.py -p ../security_content_package new
```

# Add/Update detection fields
1. Edit generated detection 
2. Update any fields set as UPDATE. Under the analytics story field you must add the name of the story this detection belongs
3. Add risk score value at ```risk_score: 50```  . Choose the base risk score you want to assign and the relevant entities. Follow the guide [here](https://github.com/splunk/security_content/wiki/Splunk-Risk-Based-Analytics-(RBA))
4. Add rba observables
```
  observable:
  - name: src
    type: Hostname
    role:
    - Attacker
  - name: dest
    type: Hostname
    role:
    - Victim
```  
message: This is a message
impact: 10
confidence: 10

# Package app

```
python contentctl.py --path ../security_content_package --verbose generate --output ../security_content_package/DA-ESS-ContentBareBones/

slim generate-manifest ../security_content_package/DA-ESS-ContentBareBones --output ../security_content_package/DA-ESS-ContentBareBones/app.manifest

slim package -o ../security_content_package/dist/DA-ESS-ContentBareBones/ ../security_content_package/DA-ESS-ContentBareBones

```
The packaged app can be found at ```/security_content_package/dist/DA-ESS-ContentBareBones/``` and is ready to uploaded to Splunk.

# Customizing the app package

There is a full guide in the main security content repo. Here we include some common fields which should exist in a detection to make it more complete. 

```
datamodel:
- Network_Traffic
tags:

  confidence: 50
  context:
  - Source:Endpoint
  - Stage:Exfiltration
  dataset:
  - https://media.githubusercontent.com/media/splunk/attack_data/master/datasets/attack_techniques/T1048.003/archive_http_post/stream_http_events.log
  kill_chain_phases:
  - Exfiltration
  message: A http post $http_method$ sending packet with possible archive bytes header
    4form_data$ in uri path $uri_path$
  observable:
  - name: uri_path
    type: UriPath
    role:
    - Attacker
  - name: form_data
    type: formdata
    role:
    - Attacker
  required_fields:
  - _time
  - http_method
  - http_user_agent
  - uri_path
  security_domain: network

```


# Generating docs
```


cd ../security_content_package/
git clone https://github.com/mitre/cti.git 
cd ../security_content/
python bin/doc_gen.py -p ../security_content_package -o ../security_content_package/docs
```

To view the docs in your local environment follow [this](https://jekyllrb.com/) guide

Or use Gitpages! Setup gitpages to point to your repository docs https://pages.github.com/



