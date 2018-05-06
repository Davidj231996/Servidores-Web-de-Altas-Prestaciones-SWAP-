# Servidores Web de Altas Prestaciones

## Práctica 4

Tareas a realizar:
  1. Crear e instalar en la máquina 1 un certificado SSL autofirmado para configurar el acceso HTTPS a los servidores. Una vez configurada la máquina 1, se debe copiar al resto de máquinas servidoras y al balanceador de carga. Se debe configurar nginx adecuadamente para aceptar y balancear correctamente tanto
el tráfico HTTP como el HTTPS.
  2. Configurar las reglas del cortafuegos con IPTABLES para asegurar el acceso a uno de los servidores web, permitiendo el acceso por los puertos de HTTP y HTTPS a dicho servidor. Esta configuración se hará en una de las máquinas servidoras finales (p.ej. en la máquina 1), y se debe poner en un script con las reglas del cortafuegos que se ejecute en el arranque del sistema (según la versión de Linux, se llevará a cabo de una forma u otra).

En esta práctica, tendremos que usar las dos máquinas finales y el balanceador nginx que teniamos de la práctica anterior.

Lo que se nos pide a realizar en esta práctica es permitir la conexión mediante https (puerto 443) a las máquinas finales y al balanceador nginx.
Para poder realizar esto, primero debemos de generar un certificado SSL autofirmado mediante la orden: "openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt".
Con esa orden creamos el fichero .key y el .crt. Debemos de crear el fichero en una de las máquinas y posteriormente copiarlas mediante SSH al resto de máquinas. Yo he usado la orden scp: "scp usuario@dominio.com:localizacion_archivo donde_guardarlo".

> Los ficheros creados

![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/apaches.png "Localización de ambos ficheros")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/apache_crt.png "apache.crt")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/apache_key.png "apache.key")

> Configuración de las máquinas finales para que escuchen por el puerto 443.

Para hacer que las máquinas escuchen por dicho puerto y  con ssl, debemos modificar el archivo que nos dice el guión: "/etc/apache2/sites-available/default-ssl". En mi caso dicho archivo no existia, estaba el archivo "default-ssl.conf".

> Modificación del archivo "default-ssl.conf".

![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/default2.png "default-ssl.conf")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/default1.png "Lineas a modificar en el archivo")


> Configuración del balanceador nginx para que escuche por el puerto 443.

En la máquina balanceadora, no tenemos apache instalado por lo que tenemos que modificar otro archvio para poder conseguir que nuestra máquina escuche por el puerto 443. Dicho archivo es: "/etc/nginx/conf.d/default.conf".
Tenemos que modificar las líneas para que sepa donde encontrar los archivos "apache.key" y "apache.crt".

![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/default3.png "El archivo default.conf")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/default3_1.png "Modificacion del archivo default.conf")

> Comprobación.

Para comprobar que todas las máquinas escuchen ahora también por el puerto 443, debemos de ejecutar la orden: "curl –k https://ipmaquina1/index.html".

> Ejecución de curl en todas las máquinas.

![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/curl.png "Ejecución de curl a las tres máquinas")

> Configuración del cortafuegos.

Debemos de crear un script como indica el guión, con ordenes iptables, para que una de nuestras máquinas finales solo escuche por el puerto 22,80 y 443, y localhost.
El script creado es el mismo que se indica en el guión.

> El script

![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/iptables.png "El script con las ordenes iptables")

> Comprobación.

Para comprobar que esta funcionando el script, ejecutamos la orden: "netstat -tulpn", y observamos los puertos que aparecen.

> Netstat -tulpn

![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica4/netstat.png "Salida de la orden netstat -tulpn")

Fin.
