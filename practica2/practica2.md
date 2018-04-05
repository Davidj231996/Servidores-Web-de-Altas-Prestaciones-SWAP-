# Servidores Web de Altas Prestaciones

## Práctica 2

Tareas a realizar:
  1. probar el funcionamiento de la copia de archivos por ssh
  2. clonado de una carpeta entre las dos máquinas
  3. configuración de ssh para acceder sin que solicite contraseña
  4. establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos      máquinas

En esta práctica, tendremos que usar las dos máquinas previamente creadas en la práctica anterior para poder realizar las tareas de esta prática, que se basan en la clonación y copia de archivos/carpetas de una máquina a otra, y la automatización del clonado.

Para poder realizar estas tareas, necesitaremos la instalación de rsync ("sudo apt-get install rsync"), y el ssh ya ha sido instalado en las máquinas en la instalación de las mismas.

> Copia de archivos por ssh
La primera tarea, es realizar un ssh a la otra máquina y copiar el archivo tar.tgz creado previamente como podemos observar explicado en el guión de la práctica ("tar czf - directorio | ssh equipodestino 'cat > ~/tar.tgz'"). A continuación, podemos ver la realización de la copia del archivo entre las máquinas:
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica2/ssh1_1.png "Confirmación de la copia del tar.tgz")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica2/ssh1_2.png "Creación del tar.tgz en la máquina 1 mediante ssh")


En la segunda tarea, vamos a hacer uso de la herramienta rsync previamente instalada. Para esta tarea, hay que tener en cuenta que debemos de ser propietarios de la carpeta que vayamos a clonar ("sudo chown usuario:usuario –R direccion_carpeta"). La orden a usar es la siguiente: "rsync -avz -e ssh ipmaquina1:/var/www/ /var/www/". A continuación, podemos observar la realización de la clonación de una carpeta entre máquinas:
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica2/rsync1.png "Clonación de la carpeta ~/html en ~/ de la máquina 2")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica2/rsync2.png "Confirmación de dicha creación")


En la tercera tarea, necesitamos crear un archivo clave mediante ssh-keygen ("ssh-keygen -b 4096 -t rsa"). Al ejecutar esa orden, nos pedirá introducir una contraseña, passphrase, que debemos de dejar en blanco para poder acceder sin contraseña mediante ssh. Posteriormente a la creación de la clave, debemos copiar dicha clave mediante ssh ("ssh-copy-id maquina1") en la otra máquina, ~/.ssh/authorized_keys, y debe tener permisos 600 ("chmod 600 ~/.ssh/authorized_keys"). A continuación podemos observar el proceso realizado para poder acceder sin clave mediante ssh:
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica2/ssh2.png "Acceso mediante ssh de la máquina 1 a la 2 sin contraseña")


En la última tarea, debemos editar el archivo /etc/crontab, en el que debemos de añadir la tarea que queremos que se realize de forma automática y periódica. Tenemos que añadir una nueva línea: **_Minuto Hora DiaDelMes Mes DiaDeLaSemana Usuario Comando_**. A continuación, podemos ver como quedaría el archivo /etc/crontab:
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica2/crontab.png "Acceso mediante ssh de la máquina 1 a la 2 sin contraseña")
