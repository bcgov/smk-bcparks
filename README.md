# smk-bcparks
A simple map for BC Parks (replacement for DMF)

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
``` $ oc new-app caddy-app-template~https://github.com/bcgov/smk-bcparks.git```

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
