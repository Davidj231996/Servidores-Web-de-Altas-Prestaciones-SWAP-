# Ejercicio 1

## Buscar información sobre cómo calcular el número de conexiones por segundo. 

Con nginx:

  - Entramos al link http://ip.address.here/nginx_status o http://your-domain-name-here/nginx_status, tras haber instalado nginx en nuestro servidor web. Nos aparaeceran cuatro variables informativas: Número total de conexiones abiertas, conexiones aceptadas, conexiones manejadas y peticiones manejadas.
  Para calcular las conexiones por segundo: peticiones manejadas / conexiones manejadas.
  
Desde la línea de comandos de linux:

  - Usando el comando "netstat | grep http | wc -l".
