# smk-bcparks
A simple map for BC Parks (replacement for DMF).

# Installation
BC Parks Simple map can be installed in 3 ways
1. deploying manually with any web server web folder e.g. Apache, IIS, NGINX
2. deploying a Docker container
3. deploying as replicaSet to OpenShift or kubernetes cluster

For small-scale production deployment or development, docker container will do fine. For large-scale production deployment requires horizontal scalability, the recommendation is one of 
* deploying as replicatSet to OpenShift or kubernetes cluster
* deploying manually with production ready web server web folder e.g. Apache, IIS, NGINX

## Deploying manually with any web server web folder
### system requirement
* any http web server, e.g. Apache, IIS, NGINX
* git
### deployment
```
 $ git clone  https://github.com/bcgov/smk-bcparks.git .
 $ cp bcparks ${WWW_folder} 
``` 
#### where ${WWW_folder} is the location served by your web server

## Deploying a Docker container
```
 $ git clone  https://github.com/bcgov/smk-bcparks.git
 $ cd smk-bcparks
 $ docker build -t bcparks .
 $ docker run -p 8080:8080 bcparks
``` 
## Deploying as replicaSet to OpenShift
```
 ## following components should be deployed in -tools project space only.
 ## deploy smk-common-iac first
 $ git clone https://github.com/bcgov/smk-common-iac.git
 $ cd smk-common-iac/openshift
 $ oc create -f iac-core.yaml
 ## wait till completion 
 $ oc create -f smk-base.yaml
 ## end of -tools project space components
 ## once core and base image creation completed, you can now deploy to -prod or -test project spaces, 
 ## following sample is for bcparks QA site
 ## cleanup previous creation
 $ oc project dbc-mapsdk-test
 $ oc process -f smk-site-deployment-template.yaml \
   SITE_NAME=bcparks \
   SITE_REPO="https://github.com/bcgov/smk-bcparks.git" \
   REPO_BRANCH=qa WEBHOOK_PATH="/webhook" | oc delete -f -
 ## install after cleanup
 $ oc process -f smk-site-deployment-template.yaml \
   SITE_NAME=bcparks \
   SITE_REPO="https://github.com/bcgov/smk-bcparks.git" \
   REPO_BRANCH=qa WEBHOOK_PATH="/webhook" | oc create -f - 
 ## for HTTP only site run following  
 $ oc expose svc/smk-bcparks --hostname=bcparks.apps.gov.bc.ca
 ## for HTTPS only site run following
 $ oc create route edge --service=smk-bcparks --hostname=bcparks.apps.gov.bc.ca
 ## Optional Steps
 ### get the secrets from secreteMap, and setup github Webhook, 
 ### now you will have auto update from git Repo to running site alive
```

## License

    Copyright 2016-present Province of British Columbia

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at 

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
