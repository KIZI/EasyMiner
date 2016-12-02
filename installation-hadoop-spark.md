## EasyMiner with Hadoop/Spark backend

In order to build this version of EasyMiner you will need bitbucket private key file and the kerberos keytab file. These files are provided upon request (see license notice below).

Requirements: Docker 1.12+

Please note that in the script below, you should use absolute paths to the bitbucket private key file and to the kerberos keytab file.

```bash
#!/bin/bash
#user inputs
HTTP_SERVER_ADDR=<docker-server>
BITBUCKET_PRIVATE_KEY=<bitbucket-private-key-file>
EASYMINER_KERBEROS_KEYTAB=<easyminer-kerberos-keytab-file>

#commands
docker network create easyminer
docker pull mysql:5.7
docker run --name easyminer-mysql -e MYSQL_ROOT_PASSWORD=root --network easyminer -d mysql:5.7
docker build -t easyminer-frontend https://github.com/KIZI/EasyMiner-EasyMinerCenter.git#v2.4:docker
docker run -d -p 8894:80 --name easyminer-frontend -e HTTP_SERVER_NAME="$HTTP_SERVER_ADDR:8894" --network easyminer easyminer-frontend
git clone -b v2.0 https://bitbucket.org/easyminer/easyminer-docker.git
cd easyminer-docker
cp $BITBUCKET_PRIVATE_KEY ./bitbucket-private-key
cp $EASYMINER_KERBEROS_KEYTAB ./easyminer.keytab
docker build -t easyminer-backend .
docker run -d -p 8893:8893 -p 8891:8891 -p 8892:8892 --name easyminer-backend -e EM_USER_ENDPOINT=http://easyminer-frontend/easyminercenter --network easyminer easyminer-backend
```

* Web GUI: http://\<docker-server\>:8894/easyminercenter
* Frontend re-install page: http://\<docker-server\>:8894/easyminercenter/install (password: 12345)

#### License

The Hadoop version is provided for free to (i) members of CESNET for non-commercial academic use. In cases not covered by (i) it is mandatory to contact the copyright holder for commercial license for components, which were not released independently under a free license. 

The software comes with absolutely no warranty.
