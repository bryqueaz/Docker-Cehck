# Basic install Docker and Swarm on CentOS7

**Paquetes**

* []() yum install epel-release
* []() yum install yum-utils
* []() yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
* []() yum install python-pip
* []() yum install docker-ce docker-ce-cli containerd.io
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

Se debe Inicalizar el nodo de swarp, el mismo se debe ejecutar en Manager Node

```
[root@docker-server bryan]# docker swarm init --advertise-addr 192.168.8.84

Swarm initialized: current node (whxp46a4pgbvs4aj552psdyxh) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join \
    --token SWMTKN-1-1i6s07uy1oho1ydn2m2vv5tudd2zhldhgisi6gq5m5ny3938nk-be0rx0pbsbtuf3dh0xb0xcum4 \
    192.168.8.84:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```
### Paso #2(-worker01)

Una vez inializado el Manager Node, el siguiente paso sería unir el worker node al node Manager.

Para ello se debe copiar la linea de Node Manager y ejecutar en los worker 1(192.168.8.14) y worker 2(192.168.8.15)

```
[root@docker-worker01 ~]#  docker swarm join --token SWMTKN-1-1i6s07uy1oho1ydn2m2vv5tudd2zhldhgisi6gq5m5ny3938nk-be0rx0pbsbtuf3dh0xb0xcum4     192.168.8.84:2377
This node joined a swarm as a worker.
```

### Paso #3(-worker02)

Una vez inializado el Manager Node, el siguiente paso sería unir el worker node al node Manager.

Para ello se debe copiar la linea de Node Manager y ejecutar en los worker 1(192.168.8.14) y worker 2(192.168.8.15)

```
[root@docker-worker02 ~]# docker swarm join \
>     --token SWMTKN-1-1i6s07uy1oho1ydn2m2vv5tudd2zhldhgisi6gq5m5ny3938nk-be0rx0pbsbtuf3dh0xb0xcum4 \
>     192.168.8.84:2377
This node joined a swarm as a worker.
```
### Paso#4 Desplegar un servicio

Aquí, implementaremos un servicio de servidor web con  cinco contenedores en modo Docker Swarm.

De debe correr en el Node manager

```
[root@docker-server bryan]# docker service create --name web1 -p 80:80 --replicas 5 nginx
pzf9z0an5yj7kl8yvaonfvvl7
```

## Comandos para probar

* []() docker ps -> Muestra los contendores que estan activos
* []() docker stats ->  Metricas de los contendores activos, memoria, cpu, I/O
* []() docker service  ps web1 -> Muestra el estado del servicio creado y los trabajos
* []() docker info -> Información del docker container
* []() docker node ls -> Información de los nodos unidos al swarm
* []() docker node ps -> Muestra la informacion de los trabajos por nodo

## Comandos para probar usando unix socket 

* []() curl --unix-socket /var/run/docker.sock http://127.0.0.1/swarm -> Obtiene la informacion del swarm
* []() curl --unix-socket /var/run/docker.sock http://127.0.0.1/services/web1 -> Obtiene la información del servicio en cluster









