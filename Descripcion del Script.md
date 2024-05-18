### Ejercicio 1

- <p> Con este script comprobaremos el estado de un servicio, en este caso el apache2. Nos interesa saber si este esta activo (running) o inactivo (death). <br> En este caso el script debera añadir a un informe la fecha actual indicando que el servicio esta desactivado, este informe se encontrara en /root/ApacheError.tmp, por lo que para poder crearlo y modificar este archivo el script pedira ser root para la ejecucion. En caso de que el servicio este apagado, lo reiniciara.
</p>

#### Formato de fecha
````
dd-mm-YYYY-Hora:minutos
````
