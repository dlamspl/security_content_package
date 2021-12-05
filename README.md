![fighter ascii](/docs/img/fighter.png)


```
git clone https://github.com/splunk/security_content/
cd security_content
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt

cd ..
git clone https://github.com/dlamspl/security_content_package
cd ../security_content
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

# Package app

```
python contentctl.py --path ../security_content_package --verbose generate --output ../security_content_package/DA-ESS-ContentBareBones/

slim generate-manifest ../security_content_package/DA-ESS-ContentBareBones --output ../security_content_package/DA-ESS-ContentBareBones/app.manifest

mkdir ../security_content_package/dist/DA-ESS-ContentBareBones
slim package -o ../security_content_package/dist/DA-ESS-ContentBareBones/ ../security_content_package/DA-ESS-ContentBareBones

```

