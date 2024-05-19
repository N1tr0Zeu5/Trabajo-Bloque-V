## Cabecera:
````
#!/bin/bash
# Author: Juan Jose Campos Gomez, Jose Manuel Lamprea Demski, Ruben Ramirez Garcia
# Versión: 1.0
# Descripción: Programa bienvenida
# Parámetros/Variables:
````
### Funciones:
````
# Funciones

menu ()
{
   while true;
   do
   	echo "************************************"
	echo "Menú: "
	echo "************************************"
	echo "1.- Crear Usuarios"
	echo "2.- Borrar Usuarios"
	echo "3.- Salir"
	read -p "Pulse un número: " numero
	
	case $numero in
		1)
			crearUsuarios ;;
		2)
			borrarUsuarios ;;
		3)
			clear
			exit ;;
		*)
			echo "Error. Por favor, seleccione una opción válida"
			;;
	esac
   done
}

crearUsuarios() 
{
    while read linea
    do
    	usuario=$(echo $linea | cut -d: -f1)
    	contrasena=$(echo $linea | cut -d: -f2)
    	nombre=$(echo $linea | cut -d: -f3)
    	apellido=$(echo $linea | cut -d: -f4)
    	correo=$(echo $linea | cut -d: -f5)

    	sudo useradd -m -s /bin/bash -p $contrasena -c "$nombre $apellido" -e "2024-06-30" $usuario > /dev/null 2>&1
    	    		if [ $? -eq 0  ];
    				then 
    					echo "El usuario: $usuario ha sido creado."
    				else
    					echo "El usuario: $usuario ya esta creado. "
    				fi
    	echo "$correo" > /home/$usuario/correo.txt

    	
    done </root/usuarios.csv
}

borrarUsuarios() 
{
  	while read linea
   	do
   		usuario=$(echo $linea | cut -d: -f1)
   	 	sudo userdel -r $usuario > /dev/null 2>&1
   	 	if [ $? -eq 0  ];
    			then 
    			echo "El usuario: $usuario ha sido eliminado "
    			else
    			echo "El usuario: $usuario no se ha podido eliminar"
   		fi
   		
	done</root/usuarios.csv
}
````
### Bloque Principal
````
# Bloque principal
clear
menu
````
### Script completo
````
#!/bin/bash
# Author: Juan José
# Versión: 1.0
# Descripción: Programa bienvenida
# Parámetros/Variables
# Funciones

menu ()
{
   while true;
   do
   	echo "************************************"
	echo "Menú: "
	echo "************************************"
	echo "1.- Crear Usuarios"
	echo "2.- Borrar Usuarios"
	echo "3.- Salir"
	read -p "Pulse un número: " numero
	
	case $numero in
		1)
			crearUsuarios ;;
		2)
			borrarUsuarios ;;
		3)
			clear
			exit ;;
		*)
			echo "Error. Por favor, seleccione una opción válida"
			;;
	esac
   done
}

crearUsuarios() 
{
    while read linea
    do
    	usuario=$(echo $linea | cut -d: -f1)
    	contrasena=$(echo $linea | cut -d: -f2)
    	nombre=$(echo $linea | cut -d: -f3)
    	apellido=$(echo $linea | cut -d: -f4)
    	correo=$(echo $linea | cut -d: -f5)

    	sudo useradd -m -s /bin/bash -p $contrasena -c "$nombre $apellido" -e "2024-06-30" $usuario > /dev/null 2>&1
    	    		if [ $? -eq 0  ];
    				then 
    					echo "El usuario: $usuario ha sido creado."
    				else
    					echo "El usuario: $usuario ya esta creado. "
    				fi
    	echo "$correo" > /home/$usuario/correo.txt

    	
    done </root/usuarios.csv
}

borrarUsuarios() 
{
  	while read linea
   	do
   		usuario=$(echo $linea | cut -d: -f1)
   	 	sudo userdel -r $usuario > /dev/null 2>&1
   	 	if [ $? -eq 0  ];
    			then 
    			echo "El usuario: $usuario ha sido eliminado "
    			else
    			echo "El usuario: $usuario no se ha podido eliminar"
   		fi
   		
	done</root/usuarios.csv
}

# Bloque principal
clear
menu
````
