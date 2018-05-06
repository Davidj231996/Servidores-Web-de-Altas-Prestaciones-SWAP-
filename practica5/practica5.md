# Servidores Web de Altas Prestaciones

## Práctica 5

Tareas a realizar:
  1. Crear una BD con al menos una tabla y algunos datos.
  2. Realizar la copia de seguridad de la BD completa usando mysqldump en la
  máquina principal y copiar el archivo de copia de seguridad a la máquina
  secundaria.
  3. Restaurar dicha copia de seguridad en la segunda máquina (clonado manual
  de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica.
  4. Realizar la configuración maestro-esclavo de los servidores MySQL para que la
  replicación de datos se realice automáticamente.

En esta práctica, vamos a crear bases de datos, y replicar la de la máquina final 1 en la 2 como si estuviesemos trabajando
con una máquina final y su réplica.

Lo primero que debemos hacer es crear nuestras base de datos en ambas máquinas, es muy importante que las bases de datos
y sus tablas tengan el mismo nombre en ambas máquinas, para así poder realizar la réplica.

Para la creación de la base de datos y su tabla, usaremos mysql, que deberá de estar instalado desde el proceso de instalación de
ambas máquinas, en el que eligimos instalar mysql junto con el SO.

Para entrar usaremos la orden: "mysql -u root -p". Luego nos pedirá la contraseña en el caso que tengamos, si no lo dejamos
en blanco y pulsamos intro.

Una vez dentro creamos la base de datos, con la orden: "create database contactos;". Una vez creada, entramos dentro de la base de datos
("use contactos;"), y creamos una tabla: "create table datos(nombre varchar(100),tlf int);".

Podemos observar que se ha creado dicha tabla mediante la orden: "show tables;".

A continuación podemos observar imágenes de las tablas ya creadas en ambas máquinas y con datos introducidos:

![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica5/db1_1.png
"Base de datos en la máquina 1")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica5/db2_1.png
"Base de datos en la máquina 2")

Ya tenemos ambas máquinas con sus respectivas bases de datos, ahora tenemos que conseguir que funcionen como maestrp-esclavo para
que se realice la replica de la base de datos en la máquina, en la base de datos de la máquina 2.

Primero, debemos de modificar unas líneas en el archivo "/etc/mysql/mysql.conf.d/mysqld.cnf":
  1. Comentar la línea: bind-address 127.0.0.1
  2. Le indicamos donde almacenar el log de errores: log_error = /var/log/mysql/error.log
  3. Establecemos el identificador del servidor: server-id = 1(En caso del maestro) 2(En caso del esclavo)
  4. El registro binario: log_bin = /var/log/mysql/bin.log
  
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica5/bind.png
"bind-address 127.0.0.1")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica5/log_error.png
"log_error")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica5/server_id_1.png
"Server id maestro")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica5/server_id_2.png
"Server id esclavo")

Despues de reinicar el mysql en ambas máquinas y sin errores, podemos volver a la máquina maestra y entrar en mysql. Tenemos que
crear un usuario y darle permisos de acceso para la replicación. Esto se realiza mediante las ordenes:
  "CREATE USER esclavo IDENTIFIED BY 'esclavo';"  
  "GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%'
IDENTIFIED BY 'esclavo';"

Una vez creado, no nos olvidemos de bloquear las tablas de la base de datos maestra. Después obtenemos los datos de la configuración
de la base de datos: "show master status;".

![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica5/master.png
"Configuración de la base de datos maestra")

Volvemos a la máquina esclava, e introducimos los datos del maestro esclavo mediante la siguiente orden: "
CHANGE MASTER TO MASTER_HOST='192.168.31.200',
MASTER_USER='esclavo', MASTER_PASSWORD='esclavo',
MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=501,
MASTER_PORT=3306;".

Posteriormente iniciamos el esclavo ("start slave;") y desbloqueamos las tablas en el maestro ("unlock tables;").
Si ahora creamos un usuario en la base de datos maestra, se replicará instantaneamente en la base de datos esclava.

![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica5/db1_2.png
"Creación usuario en base de datos maestra")
![alt text](https://github.com/Davidj231996/Servidores-Web-de-Altas-Prestaciones-SWAP-/blob/master/practica5/db2_2.png
"Replica del usuario previamente creado")
