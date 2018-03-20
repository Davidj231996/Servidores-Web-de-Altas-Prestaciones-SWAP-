# Servidores Web de Altas Prestaciones

## Práctica 1

Tareas a realizar:
1. acceder por ssh de una máquina a otra
2. acceder mediante la herramienta curl desde una máquina a la otra

En esta práctica, se tiene que crear dos máquinas virtuales con Ubuntu Server, en mi caso he usado la versión 16.04.4.
Tras la creación de dichas máquinas virtuales, teniamos que configurar ambas máquinas con una ip fija. Para ello, se deben de añadir un nuevo adaptador de red en cada máquina de tipo red interna, para su posterior modificación en el archivo /etc/networks/interfaces.
En las siguientes imágenes podremos observar las configuraciones de red de ambas máquinas:
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica1/ifconfig.png "Configuración de Red Mquina 1")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica1/ifconfig2.png "Configuración de Red Máquina 2")

Para comprobar que ambas máquinas se ven, podemos usar ping y la ip de la otra máquina. Y para poder comprobar si hay internet en nuestras máquinas, podemos usar la orden curl a una dirección web sencilla.

Después de la configuración de red de ambas máquinas, procedemos a la realización de las tareas previamente descritas.

A continuación podemos observar imágenes de como creamos una carpeta, practica1, en una máquina desde la otra máquina usando ssh (normalmente nos pediría la contraseña, pero como ya tengo resuelta la práctica 2, no no las va a pedir y vamos a entrar directamente):
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica1/ssh_client.png "ssh desde la Máquina 1 a la 2")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica1/ssh_server.png "comprobación del ssh en la máquina 2")

La segunda tarea se basa en acceder, con la herramienta curl, desde una máquina a la otra. Para poder realizar esta tarea, tenemos que crear previamente un archivo html en la carpeta /var/www/html/ de la máquina a la que vamos a acceder.
Una vez realizado esto, ya podemos realizar la orden curl a dicho archivo html desde la máquina 1:
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica1/curl_client.png "curl desde la Máquina 1 a la 2")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica1/curl_server.png "Verificación de que a accedido al archivo correcto")
