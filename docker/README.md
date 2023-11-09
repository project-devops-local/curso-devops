-----------------------------------------------------------
-------------   CLASE #2  22/06/2021   --------------------
-----------------------------------------------------------
#crear contenedor y iniciar en base a una imagen  usuario especifico tener en cuenta --privileged y /usr/sbin/init procesos de systemctl esto aplica para image centos
docker run --privileged --name nameContainer -itd centos:7 /usr/sbin/init -> crear contenedor basico que permita ejecutar systemctl

#Comandos varios
docker inspect container  -> ver la configuracion del contenedro salida json
docker ps ---> ver contenedores running 
docker ps -a  ---> ver contenedores estado running y en stop
docker images ---> ver el listado de images descargadas desde el registry de docker
docker rm -f nameContainer --> eliminar forzadamente un contender en estado running.
docker rm -f nameContainer --> eliminar forzadamente un contender en estado running.


#comandos networking
docker network ls ---> listar tipos de redes 
docker network inspect nameRED -> inspecionar red existente
docker network create --subnet 10.130.2.0/24 --gateway 10.130.2.254 nameRED -> crear red bridge definiendo un rango de ips
docker network connect nameRED nameContainer ----> vincular red a un contenedor existente
docker run --name nameContainer -itd -h hostanme --network red1 centos:7 -> crear contenedor asociando la red network red1

-----------------------------------------------------------
-------------   CLASE #2  23/06/2021   --------------------
-----------------------------------------------------------
#utilizando relacion de contenedores con --link
1) example 
docker run --name pruebalink -itd centos:7
docker run --name pruebalink2 -itd centos:7
docker run --name pruebalink3 --link pruebalink -itd centos:7 -> asociar contenedor pruebalink para realizar conexion ping nameContainer

#configurando puertos en los contenedores
docker run --privileged --name pruebaPort -itd --expose 22 --expose 443 --expose 80 -P ubuntu /bin/bash
docker run --privileged --name pruebaPort2 -itd  -p 8080:80  ubuntu /bin/bash

docker port container -> lista los puertos expuestos del contenedor

#que es dockerfile
#comando para generar imagen en base a un dockerfile o url
docker build -t laboratorio-docker:v1 url o .

#reglas de ip con iptables 
sudo iptables -L -n