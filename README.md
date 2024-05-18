### Ejercicio 1

Con este script comprobaremos el estado de un servicio, en este caso el apache2. Nos interesa saber si este esta activo (running) o inactivo (death).
<br>
En este caso el script debera añadir a un informe la fecha actual indicando que el servicio esta desactivado, este informe se encontrara en 
/root/ApacheError.tmp por lo que para poder crearlo y modificar este archivo el script pedira ser root para la ejecucion.
<br>
 En caso de que el servicio este apagado, lo reiniciara.

> [!TIP]
> #### Formato de fecha:
>> dd-mm-YYYY-Hora:minutos
 <br>

### Comprobar el root 

````
comprobarRoot()
{
    if [ "$(id -u)" != "0" ]
        then   
            echo " Este script solo puede ser ejecutado por el Root"
            exit
    fi
}

````
- Comprobamos que el usuario que ejecuta el sript es el root del sistema
> [!NOTE]
> Para que el script se ejecute todos los dias a las 6 debemos introducir en el crontab -e:
> <br>
> <br>
> 0 6 * * * /rutadelscript
> <br>
> <br>
> Para que cuando se inicie el sistema el script se inicie a los 5 minutos, en el crontab -e:
> <br>
> <br>
> @reboot sleep 300 && /rutadelscript
> <br>
