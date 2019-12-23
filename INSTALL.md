# Basic install Docker and Swarm on CentOS7

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
[root@docker-server bryan]# systemctl start Docker
```
## Habiliar de manera persistente el servicio de Docker
```
[root@docker-server bryan]# systemctl enable docker
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
[root@docker-server bryan]# firewall-cmd --reload
[root@docker-server bryan]# systemctl restart docker
```

## Busca la imagen
```
[root@docker-server bryan]# docker search centos
```
## Descarga la imagen
```
[root@docker-server bryan]# docker pull centos
```

## Crea un contener usando la imagen de centos
```
[root@docker-server bryan]# docker run --name=centos7prueba -d -t docker.io/centos
```

## Instalar Node Swarm

Para ello se deben tener 3 maquinas instalas con Docker, con CentOS7

* []() Manager Node IP: 192.168.8.84
* []() Worker Node1 IP:  192.168.8.14
* []() Worker Node2 IP:  192.168.8.15

## Inicalizar el nodo de Swarm

### Paso #1
```
[root@docker-server bryan]# docker swarm init --advertise-addr 192.168.8.84

Swarm initialized: current node (whxp46a4pgbvs4aj552psdyxh) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join \
    --token SWMTKN-1-1i6s07uy1oho1ydn2m2vv5tudd2zhldhgisi6gq5m5ny3938nk-be0rx0pbsbtuf3dh0xb0xcum4 \
    192.168.8.84:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.


```





