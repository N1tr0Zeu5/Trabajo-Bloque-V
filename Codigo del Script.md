### Cabecera:
````
#!/bin/bash
#Author: Juan Jose Campos Gomez, Jose Manuel Lamprea Demski, Rubén Ramírez García
#Version: 1.0 
#Descripcion: Script que comprueba el estado del servicio apache. En caso de que este inactivo, lo reinicia y envia a un informe la informacion de cuando estaba inactivo
#Parámetros/Variables:
fecha=`date +%d-%m-%Y-%H:%M`
informe=EstadoApache2.txt
status=$(systemctl status apache2)
reinicio=$(systemctl restart apache2)
#Comentarios: Si queremos que el script se ejecute a las 6 y se ejecute cuando 
````
### Funciones 
````
#Funciones
comprobarRoot()
{
    if [ "$(id -u)" != "0" ];
        then   
            echo " Este script solo puede ser ejecutado por el Root"
            exit
    fi
}
````
### Bloque Principal
````
#BloquePrincipal
clear
comprobarRoot
echo "$status" >> $informe
cat $informe | grep -w "running"
    if [ $? -ne 0 ];
        then echo "Error apache: $fecha" >> /root/ApacheError.tmp
        echo "$reinicio"
        else echo "El servicio esta activo (running)"
    fi
````
### Codigo Completo
````
#!/bin/bash
#Author:  Juan Jose Campos Gomez, Jose Manuel Lamprea Demski, Rubén Ramírez García
#Version: 1.0 
#Descripcion: Script que comprueba el estado del servicio apache. En caso de que este inactivo, lo reinicia y envia a un informe la informacion de cuando estaba inactivo
#Parámetros/Variables:
fecha=`date +%d-%m-%Y-%H:%M`
informe=EstadoApache2.txt
status=$(systemctl status apache2)
reinicio=$(systemctl restart apache2)
#Comentarios: 
#Funciones
comprobarRoot()
{
    if [ "$(id -u)" != "0" ];
        then   
            echo " Este script solo puede ser ejecutado por el Root"
            exit
    fi
}
#BloquePrincipal
clear
comprobarRoot
echo "$status" > $informe
cat $informe | grep -w "running" > /dev/null
    if [ $? -eq 0 ];
        then echo "El servicio esta activo"
        else echo "Error apache: $fecha" >> /root/ApacheError.tmp
            echo "$reinicio"
            echo " El servicio ha sido reiniciado"
    fi

````
