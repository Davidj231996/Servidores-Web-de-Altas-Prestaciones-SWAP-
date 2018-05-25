# Ejercicio 5

## Probar las diferentes maneras de redirección HTTP. ¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué? 

301 y 302. Para el balanceo de carga global se debería de usar el 302 ya que así la antigua dirección url sigue siendo válida, y la redirección sólo es temporal.
