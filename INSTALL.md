# Basic install Docker and Swarm CentOS7

**Paquetes**

* []() yum install epel-release
* []() yum install yum-utils
* []() yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
* []() yum install python-pip
* []() yum install docker
* []() pip3 install docker 
* []() pip3 install check_docker


## Levantar el servicio de docker
```
[root@docker-server bryan]#systemctl start Docker
```
## Habiliar de manera percistente el servicio de Docker
```
[root@docker-server bryan]#systemctl enable docker
```
