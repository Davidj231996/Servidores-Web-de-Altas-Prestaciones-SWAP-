# Servidores Web de Altas Prestaciones

## Práctica 3

Tareas a realizar:
  1. configurar una máquina e instalar el nginx como balanceador de carga
  2. configurar una máquina e instalar el haproxy como balanceador de carga
  3. someter a la granja web a una alta carga, generada con la herramienta Apache Benchmark, teniendo primero nginx y después haproxy.

En esta práctica, tendremos que usar las dos máquinas previamente creadas en la práctica 2, y añadirle una máquina virtual por cada balanceador software(haproxy y nginx).

Se crean las máquinas virtuales, y mediante las siguientes ordenes se pueden añadir ambos software de balanceo, como indicadas en el guión de la práctica:
  -> ###NGINX
    sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove
    sudo apt-get install nginx
    sudo systemctl start nginx
    
  -> ###HAPROXY
    sudo apt-get install haproxy
   
>Configuración de nginx.

Para poder configurar nginx, debemos de modificar el archivo "/etc/nginx/conf.d/default.conf", como indica el guión:
  - Definir grupo upstream con las IPs de nuestras máquinas.
  - La conexión entre nginx y los servidores finales sea HTTP 1.1.
  - Eliminar la cabecera Connection.
  
Para iniciar nginx usamos la orden "sudo systemctl start nginx", y comprobamos con curl a la IP del balanceador desde una máquina externa.

> Versión de nginx.
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica3/Captura%20de%20pantalla%20(86).png "Confirmación de la copia del tar.tgz")

> Configuración de haproxy.
Primero configuramos el archivo "/etc/haproxy/haproxy.cfg", tal y como se indica en el guión y podemos observar a continuación:
  global
    daemon
    maxconn 256
    
  defaults
    mode http
    contimeout 4000
    clitimeout 42000
    srvtimeout 43000
    
  frontend http-in
    bind *:80
    default_backend servers
    
  backend servers
    server m1 "ip máquina 1":80 maxconn 32
    server m2 "ip máquina 2":80 maxconn 32

Una vez configurado el archivo, procedemos con el lanzamiento de haproxy mediante la orden "sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg", y comprobamos con curl al balanceador de haproxy.

> Versión de haproxy.
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica3/Captura%20de%20pantalla%20(85).png "Confirmación de la copia del tar.tgz")

> Instalación de Apache Benmark.
 Lo instalamos en una máquina diferente a las que tenemos, pero dentro de la misma red interna. Para ello usamos la orden "sudo apt-get install apache2-utils".
 
 > Lanzamiento de Apache Benmark.
 Para el lanzamiento del Apache Benmark, usamos la orden dada en el guión "ab -n 1000 -c 10 http://"IP máquina balanceadora"/index.html"
 
 El IP de la máquina balanceadora serán las dos máquinas que tenemos cada uno con haproxy y nginx.
 
 Para comprobar que el balanceador funciona y divide la carga entre las máquinas dependiendo de la carga que le hayamos puesto, usaremos la herramiento "top". Que instalaremos mediante "sudo apt-get install top". Deberemos de instalar dicha herramienta en todas las máquinas exceptuando desde la que lanzamos el Apache Benmark.
 
 > Comprobación balanceador nginx.
 
 > Comprobación balanceador haproxy.
