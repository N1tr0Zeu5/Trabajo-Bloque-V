### Cabecera:
````
#!/bin/bash
#Author:  Juan Jose Campos Gomez, Jose Manuel Lamprea, Ruben Ramirez Garcia
#Version: 1.0 
#Descripcion:
#Parámetros/Variables:
fecha=`date +%d-%m-%Y-%H:%M`
informe=`EstadoApache2.txt`
status=$(systemctl status apache2)
reinicio=$(systemctl restart apache2)
#Comentarios: 
````
### Funciones 
````
#Funciones
comprobarRoot()
{
    if [ "$(id -u)" != "0" ]
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
#Author:  Juan Jose Campos Gomez, Jose Manuel Lamprea, Ruben Ramirez Garcia
#Version: 1.0 
#Descripcion:
#Parámetros/Variables:
fecha=`date +%d-%m-%Y-%H:%M`
informe=`EstadoApache2.txt`
status=$(systemctl status apache2)
reinicio=$(systemctl restart apache2)
#Comentarios: 
#Funciones
comprobarRoot()
{
    if [ "$(id -u)" != "0" ]
        then   
            echo " Este script solo puede ser ejecutado por el Root"
            exit
    fi
}
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
