# Ejercicio 1

## Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.

En Linux, la configuración de red está en /etc/network/interfaces, archivo donde podemos establecer las configuraciones de red. Añadimos la ruta al archivo /etc/network/interfaces mediante la línea "route add -net"
