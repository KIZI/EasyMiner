# EasyMiner - Easy association rule mining on the web

EasyMiner is an open source web-based project for data mining based on association rules.
Key features:
- association rule mining (based on arules package in R)
- classification model building and rule prunning (based on algorithm rCBA)
- prediction API
- interactive web UI working in all modern web browsers
- RESTful API

## Project web
http://easyminer.eu

## Repository content
EasyMiner project is based on interconnection of fundamental components. Top components are available in this repository:
- **[EasyMinerCenter](https://github.com/KIZI/EasyMiner-EasyMinerCenter)**
  - main component for users interaction (web UI, RESTful API)
  - written in PHP/JavaScript 
- **[EasyMiner-Backend](https://github.com/KIZI/EasyMiner-Backend)**
  - combination of three basic backend services - data service, preprocessing service and miner service
  - written in Scala
- **[rCBA](https://github.com/jaroslav-kuchar/rCBA)**
  - CBA classifier for R (association rule pruning, building of classification models)
  - compiled version is available also in [CRAN repository](https://cran.r-project.org/web/packages/rCBA/index.html)
  - written in Java 8

For clone of its content, do not forget to clone also all linked submodules (recursively). You can run the command:
```git
 git clone --recursive https://github.com/KIZI/EasyMiner.git 
```
## Issue tracking
EasyMiner is composed of three components, which are maintained separately. Before posting an issue, please select the right issue tracker. 
- Issues related to the user interface: [https://github.com/KIZI/EasyMiner-EasyMinerCenter/issues](https://github.com/KIZI/EasyMiner-EasyMinerCenter/issues)
- Issues related to data handling and processing:  [https://github.com/KIZI/EasyMiner-Backend/issues](https://github.com/KIZI/EasyMiner-Backend/issues)
- Issues related to the rule learning and pruning algorithm: [https://github.com/jaroslav-kuchar/rCBA/issues](https://github.com/jaroslav-kuchar/rCBA/issues)

If you are not sure which one to pick, don't worry, your issue will be migrated to the right repository.
## License
EasyMiner components are licensed under [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0). 

Copyright 2016 Department of Information and Knowledge Engineering, University of Economics, Prague

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
