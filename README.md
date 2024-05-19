# Descripción del Script
### Ejercicio 3
- Buscamos la creacion de un menu que nos permita realizar creacion masiva de usuarios y la eliminacion de estos. La informacion respectiva de los usuarios se almacena en un archivo .csv.


> [!NOTE]
> La disposicion es la siguiente:
> - El campo 1 representa el nombre de usuario.
> - El campo 2 representa la contraseña.
> - El campo 3 representa el nombre.
> - El campo 4 representa su primer apellido.
> - El campo 5 representa su correo electrónico

Ademas se ha establecido que la fecha de expiracion de las cuentas sea el 30-06-2024. 
<br>

### Funcion del menu:
````
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
````
Funcion que imprime el menu y tiene todas las funciones que se ejecutan en el script
<br>

### 1- Crear Usuario

````
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
````
Asigna a las variables (usuario, contrasena, nombre, apellido y correo) valores obtenidos del archivo usuarios.csv que se encuentra en /root/usuario.csv 
<br>
El comando "sudo useradd -m -s /bin/bash -p $contrasena -c "$nombre $apellido" -e "2024-06-30" $usuario > /dev/null 2>&1" crea todos los usuarios contenidos en el archivo.csv
<br>
Por ultimo hay una verificacion para saber si se han podido crear los usuarios o no.
<br>
### 2- Borrar usuarios
````
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
En un bucle while read coge los nombres de usuarios del archivo usuarios.csv, con el comandos "sudo userdel -r $usuario > /dev/null 2>&1" elimina los usuarios.
