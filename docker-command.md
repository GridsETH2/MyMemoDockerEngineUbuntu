# USE

## BASIC DOCKER COMMAND

**command - manage docker `images`**
- List `images` in pc
~~~
sudo docker images

REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
hello-world   latest    feb5d9fea6a5   6 months ago   13.3kB
~~~
- Search `images` form **Docker Hub**
~~~
sudo docker search [OPTIONS] TERM
~~~
Example
~~~
sudo docker search mysql

NAME                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                            MySQL is a widely used, open-source relation…   12419     [OK]       
mariadb                          MariaDB Server is a high performing open sou…   4784      [OK]       
mysql/mysql-server               Optimized MySQL Server Docker images. Create…   918                  [OK]
percona                          Percona Server is a fork of the MySQL relati…   575       [OK]       
phpmyadmin                       phpMyAdmin - A web interface for MySQL and M…   506       [OK]       
mysql/mysql-cluster              Experimental MySQL Cluster Docker images. Cr…   93                   
centos/mysql-57-centos7          MySQL 5.7 SQL database server                   92                   
bitnami/mysql                    Bitnami MySQL Docker Image                      69                   [OK]
ubuntu/mysql                     MySQL open source fast, stable, multi-thread…   29                   
circleci/mysql                   MySQL is a widely used, open-source relation…   25                   
mysql/mysql-router               MySQL Router provides transparent routing be…   23                   
centos/mysql-56-centos7          MySQL 5.6 SQL database server                   22                   
google/mysql                     MySQL server for Google Compute Engine          21                   [OK]
vmware/harbor-db                 Mysql container for Harbor                      10                   
bitnami/mysqld-exporter                                                          3                    
mysqlboy/docker-mydumper         docker-mydumper containerizes MySQL logical …   3                    
mysqlboy/mydumper                mydumper for mysql logcial backups              3                    
ibmcom/mysql-s390x               Docker image for mysql-s390x                    2                    
mysql/mysql-operator             MySQL Operator for Kubernetes                   0                    
cimg/mysql                                                                       0                    
mysqlboy/elasticsearch                                                           0                    
mysqleatmydata/mysql-eatmydata                                                   0                    
ibmcom/tidb-ppc64le              TiDB is a distributed NewSQL database compat…   0                    
mysql/ndb-operator               MySQL NDB Operator for Kubernetes               0                    
mirantis/mysql                                                                   0      
~~~
- Remove `images`
~~~
sudo docker rmi [OPTIONS] IMAGES [IMAGES...] 
~~~
- Pull `images`
~~~
sudo docker pull [OPTIONS] NAME[:TAG|@DIGEST]
~~~
- Push `images`
~~~
sudo docker push [OPTIONS] NAME[:TAG]
~~~
- Commit`images`
~~~
sudo docker commit [OPTIONS] CONTAINER [REPOSUTORY[:TAG]]
~~~
- Tag `images`
~~~
sudo docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
~~~
