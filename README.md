# EasyMiner - Easy association rule mining on the web

EasyMiner/R is an open source web-based project for data mining based on association rules.
Key features:
- complete Prediction API (PAPI) - RESTful
- interactive web UI working in all modern web browsers
- association rule mining (based on Apriori algorithm/[arules](https://github.com/mhahsler/arules/) package in R)
- classification model building and rule pruning (based on Classification based on Associations/CBA/ algorithm)

As a complement to EasyMiner/R, there is also a proprietary on-demand version of EasyMiner based on Apache Spark/Hadoop.

[![Build Status](https://travis-ci.org/KIZI/EasyMiner-Evaluation.svg?branch=master)](https://travis-ci.org/KIZI/EasyMiner-Evaluation)
```diff
-- Note that as of July 2017 the Travis CI integration status is somewhat unstable due to updates in Travis CI Linux images used. In practice, this means that if you see Build failing status, there is nothing wrong with the code and the
``` 
```diff
++ installation can complete successfully
```
```diff
-- on your machine. We are working to resolve this issue.
```


## Project web
http://easyminer.eu

## Repository content (where do I see the issues and commits?)
EasyMiner/R project is composed of three independently developed components:
- **[EasyMinerCenter](https://github.com/KIZI/EasyMiner-EasyMinerCenter)**
  - user interaction (web UI, RESTful API)
  - written in PHP/JavaScript 
- **[EasyMiner-Backend](https://github.com/KIZI/EasyMiner-Backend)**
  - data manipulation and handling of mining tasks
  - three services: data service, preprocessing service and miner service
  - written in Scala
- **[rCBA](https://github.com/jaroslav-kuchar/rCBA)** [![Build Status](https://travis-ci.org/jaroslav-kuchar/rCBA.svg?branch=master)](https://travis-ci.org/jaroslav-kuchar/rCBA)
  - implementation of the CBA algorithm used for rule pruning and building of classification models
  - compiled version is available also in [CRAN repository](https://cran.r-project.org/package=rCBA)
  - written in Java 8
- **[EasyMiner-Scorer](https://github.com/KIZI/EasyMiner-Scorer)**
  - classification scorer
  - written in Java 8
- **[Evaluation](https://github.com/KIZI/EasyMiner-Evaluation)** [![Build Status](https://travis-ci.org/KIZI/EasyMiner-Evaluation.svg?branch=master)](https://travis-ci.org/KIZI/EasyMiner-Evaluation)
  - evaluation framework for EasyMiner
  - covers 36 UCI datasets
  - written in Python
- **[Benchmark](https://github.com/KIZI/EasyMiner-Benchmark)**
  - benchmark framework for EasyMiner, Sci-kit and Weka
  - covers 36 UCI datasets
  - written in Python and Java
  
When cloning project content do not forget to clone also all the linked submodules (recursively) with:
```git
 git clone --recursive https://github.com/KIZI/EasyMiner.git 
```

## Installation instructions

This is an installation package of the Easyminer/R bundle for the docker environment. This installation contains backend, frontend and database.  In addition to the completely free version with R backend covered here, there are installation instructions for the on-request version with [Hadoop/Spark backend](https://github.com/KIZI/EasyMiner/blob/master/installation-hadoop-spark.md). An overview of available REST endpoints is provided in the end of the document.

### EasyMiner with R backend

Requirements: Docker 1.12+

```bash
#!/bin/bash

docker network create easyminer
docker pull mariadb:10
docker run --name easyminer-mysql -e MYSQL_ROOT_PASSWORD=root --network easyminer -d mariadb:10
docker pull kizi/easyminer-frontend:v2.4
docker run -d -p 8894:80 --name easyminer-frontend --network easyminer kizi/easyminer-frontend:v2.4
docker pull kizi/easyminer-backend:v2.4
docker run -d -p 8893:8893 -p 8891:8891 -p 8892:8892 --name easyminer-backend -e EM_USER_ENDPOINT=http://easyminer-frontend/easyminercenter --network easyminer kizi/easyminer-backend:v2.4
docker pull kizi/easyminer-scorer:v2.4
docker run -d -p 8080:8080 --name easyminer-scorer --network easyminer kizi/easyminer-scorer:v2.4
```

* Web GUI: **http://\<docker-server\>:8894/easyminercenter**
* Frontend re-install page: *http://\<docker-server\>:8894/easyminercenter/install* (password: 12345)
* Frontend API endpoint: **http://\<docker-server\>:8894/easyminercenter/api**
* HEADS UP: Use IP address or URL for docker-server, NOT localhost! Using localhost will block crossite scripting, eventually leading to error
* HEADS UP: If you  run EasyMiner in virtual machine, use Bridged adapter (not NAT)
### Additional information

REST API endpoints are accessible on:

* http://\<docker-server\>:8891/easyminer-data/index.html - data service
* http://\<docker-server\>:8892/easyminer-preprocessing/index.html - preprocessing service
* http://\<docker-server\>:8893/easyminer-miner/index.html - miner service
* http://\<docker-server\>:8894/easyminercenter/api - easyminer central service 

## Issue tracking
EasyMiner/R is composed of four components, which are maintained separately. Before posting an issue, please select the right issue tracker. 
- Issues related to the user interface: [https://github.com/KIZI/EasyMiner-EasyMinerCenter/issues](https://github.com/KIZI/EasyMiner-EasyMinerCenter/issues)
- Issues related to data handling and processing:  [https://github.com/KIZI/EasyMiner-Backend/issues](https://github.com/KIZI/EasyMiner-Backend/issues)
- Issues related to the rule learning and pruning algorithm: [https://github.com/jaroslav-kuchar/rCBA/issues](https://github.com/jaroslav-kuchar/rCBA/issues)
- Issues related to classification scorer:  [https://github.com/KIZI/EasyMiner-Scorer/issues](https://github.com/KIZI/EasyMiner-Scorer/issues)

If you are not sure which one to pick, don't worry, your issue will be migrated to the right repository.
## License
EasyMiner/R components are licensed under [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0). 

Copyright 2016 Department of Information and Knowledge Engineering, University of Economics, Prague

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
