# Docker Check - Nagios Icinga

## Estado de las instancias
```
[root@docker-server bryan]# python3 docker_check_socket.py --status running
OK: jovial_goldberg status is running; OK: hungry_carson status is running; CRITICAL: musing_rosalind state is not running
```

## CPU
```
[root@docker-server bryan]# python3 docker_check_socket.py --cpu 80:90
CRITICAL: musing_rosalind is not "running", cannot check cpu"; OK: jovial_goldberg cpu is 0%; OK: hungry_carson cpu is 0%|jovial_goldberg_cpu=0;80;90;0;100 hungry_carson_cpu=0;80;90;0;100
```

## Memoria
```
[root@docker-server bryan]# python3 docker_check_socket.py --memory 80:90:%
CRITICAL: musing_rosalind is not "running", cannot check memory"; OK: jovial_goldberg memory is 0%; OK: hungry_carson memory is 0%|jovial_goldberg_mem=0%;80;90;0;100 hungry_carson_mem=0%;80;90;0;100
```

## uptime
```
[root@docker-server bryan]# python3 docker_check_socket.py  --uptime 200:300
OK: jovial_goldberg uptime is 30min 10s; OK: hungry_carson uptime is 8min 0s; CRITICAL: musing_rosalind is not "running", cannot check uptime"|jovial_goldberg_up=1810.4;200;300;0;2 hungry_carson_up=480.4;200;300;0;2
```

## Monitoreos globales
```
[root@docker-server bryan]# python3 docker_check_stats.py
OK | hungry_carson_mem_pct=0.03 hungry_carson_cpu_pct=0.0 hungry_carson_net_in=746 hungry_carson_net_out=656 hungry_carson_disk_in=0 hungry_carson_disk_out=0 jovial_goldberg_mem_pct=0.03 jovial_goldberg_cpu_pct=0.0 jovial_goldberg_net_in=1402 jovial_goldberg_net_out=656 jovial_goldberg_disk_in=0 jovial_goldberg_disk_out=0
```

## Estado del node de swarm
```
[root@docker-server bryan]# python3 check_swarm.py --swarm  
OK: Node is in a swarm
```

## Estado del servicio en cluster en swarm
```
[root@docker-server bryan]# python3 check_swarm.py --service web1
OK: Service web1 is up and running
```