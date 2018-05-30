# Ejercicio 4

## Buscar información sobre los sistemas de ficheros en red más utilizados en la actualidad y comparar sus características. Hacer una lista de ventajas e inconvenientes de todos ellos, así como grandes sistemas en los que se utilicen.

#### NFS:

El sistema NFS está dividido al menos en dos partes principales: un servidor y uno o más clientes. Los clientes acceden de forma remota a los datos que se encuentran almacenados en el servidor.

Las estaciones de trabajo locales utilizan menos espacio de disco debido a que los datos se encuentran centralizados en un único lugar pero pueden ser accedidos y modificados por varios usuarios, de tal forma que no es necesario replicar la información.

Los usuarios no necesitan disponer de un directorio “home” en cada una de las máquinas de la organización. Los directorios “home” pueden crearse en el servidor de NFS para posteriormente poder acceder a ellos desde cualquier máquina a través de la infraestructura de red.

También se pueden compartir a través de la red dispositivos de almacenamiento como disqueteras, CD-ROM y unidades ZIP. Esto puede reducir la inversión en dichos dispositivos y mejorar el aprovechamiento del hardware existente en la organización.


#### SMB

Server Message Block (SMB) es un protocolo de red que permite compartir archivos, impresoras, etcétera, entre nodos de una red de computadoras que usan el sistema operativo Microsoft Windows.

Es utilizado principalmente en computadoras con sistemas operativos: Microsoft Windows y DOS.

Microsoft renombró SMB a Common Internet File System (CIFS) y añadió más características, que incluyen: soporte para enlaces simbólicos, enlaces duros (hard links), y mayores tamaños de archivo.


#### AFS

El Andrew File System (Sistema de archivos Andrew), o AFS es un sistema de archivos distribuido a través de la red. Es utilizado fundamentalmente en entornos de computación distribuida.
