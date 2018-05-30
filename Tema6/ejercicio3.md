# Ejercicio 3

## Buscar información acerca de los tipos de ataques más comunes en servidores web (p.ej. secuestros de sesión). Detallar en qué consisten, y cómo se pueden evitar. 

Los ataques a servidores web más comunes son los ataques de inyección, ataques DDoS y de fuerza bruta.

Inyección SQL: Inyección SQL es un método de infiltración de código intruso que se vale de una vulnerabilidad informática presente en una aplicación en el nivel de validación de las entradas para realizar operaciones sobre una base de datos.
Usando en los códigos de las páginas web, funciones ya creadas para evitar dichos ataques: mysql_real_escape_string(PHP), parametrización de sentencias SQL y escape de las variables a insertar en la sentencia SQL (Java).

DDoS: Un ataque de denegación de servicio impide el uso legítimo de los usuarios al usar un servicio de red. El ataque se puede dar de muchas formas. Pero todas tienen algo en común: utilizan la familia de protocolos TCP/IP para conseguir su propósito.

Un ataque DoS puede ser perpetrado de varias formas. Aunque básicamente consisten en:

  - Consumo de recursos computacionales, tales como ancho de banda, espacio de disco, o tiempo de procesador.
  - Alteración de información de configuración, tales como información de rutas de encaminamiento.
  - Alteración de información de estado, tales como interrupción de sesiones TCP (TCP reset).
  - Interrupción de componentes físicos de red.
  - Obstrucción de medios de comunicación entre usuarios de un servicio y la víctima, de manera que ya no puedan comunicarse adecuadamente.
  
Ante un ataque DDoS, la mitigación consiste en filtrar el tráfico no legítimo y aspirarlo mediante el VAC, dejando pasar todos los paquetes legítimos.


El VAC consta de varios dispositivos, cada uno de los cuales cumple una función específica para bloquear uno o varios tipos de ataque (DDoS, Flood, etc.). En función del ataque, pueden aplicarse una o varias estrategias de defensa en cada uno de los dispositivos que componen el VAC.

Fuerza Bruta: En criptografía, se denomina ataque de fuerza bruta a la forma de recuperar una clave probando todas las combinaciones posibles hasta encontrar aquella que permite el acceso.
Este ataque se usa sobre todo para descubrir claves de acceso a redes sociales y cuentas de correo.

Para evitar este ataque, debemos de crear contraseñas de acceso de una longitud larga y que no contengan palabras enteras.
