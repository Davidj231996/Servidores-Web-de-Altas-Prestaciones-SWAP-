# Ejercicio 1

## Aplicar con iptables una política de denegar todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento.
## Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento. 

Las reglas iptables para denegar todo el tráfico son:
  //Para eliminar todas las reglas
  iptables –F
  iptables -X
  iptables -Z
  iptables -t nat -F
  //Aceptar todo el tráfico
  iptables −P INPUT DROP
  iptables −P OUTPUT DROP
  iptables −P FORWARD DROP

Las reglas iptables para aceptar todo el tráfico son:
  //Para eliminar todas las reglas
  iptables –F
  iptables -X
  iptables -Z
  iptables -t nat -F
  //Aceptar todo el tráfico
  iptables −P INPUT ACCEPT
  iptables −P OUTPUT ACCEPT
  iptables −P FORWARD ACCEPT
