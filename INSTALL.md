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
## Habiliar de manera persistente el servicio de Docker
```
[root@docker-server bryan]#systemctl enable docker
```

## Agrega reglas al Firewall

* []() firewall-cmd --permanent --add-port=2376/tcp
* []() firewall-cmd --permanent --add-port=2377/tcp
* []() firewall-cmd --permanent --add-port=7946/tcp
* []() firewall-cmd --permanent --add-port=80/tcp
* []() firewall-cmd --permanent --add-port=7946/udp
* []() firewall-cmd --permanent --add-port=4789/udp

## Reinicia los servicio de firewall y docker
```
[root@docker-server bryan]#firewall-cmd --reload
```

```
[root@docker-server bryan]#systemctl restart docker
```
