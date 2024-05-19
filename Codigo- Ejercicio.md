## Cabecera: 
```
#!/bin/bash
#Author:  Juan Jose Campos Gomez, Jose Manuel Lamprea, Ruben Ramirez Garcia
#Version: 1.0 
#Descripcion: Scrip que imprime un menu y ofrece las siguientes opciones. (1) Una lista de los usuarios bloqueados en el sistema (2) La posibilidad de bloquear un usuario (3) La posibilidad de desbloquear un usuario (4) Cerrar la sesion de un usuario (5)Salir del script
#Parámetros/Variables:
		tiempo=$(date -d "$(who | grep $usuario | awk '{print $4}')" +%s)
		tiempo_activo=$(date +%s)
		tiempo_inactivo=$((tiempo_activo - tiempo ))
#Comentarios: 
```
## Funciones 
```
#Funciones

listabloqueado () 
			{
				echo "Usuarios bloqueados: "
				awk -F: '$3 >= 1000 && $3 < 2000 {print $1}' /etc/passwd > /home/josemanuel/boletinscript1/informe.txt
				sudo passwd -S -a | grep " L " | cut -d " " -f1 > /home/josemanuel/boletinscript1/bloqueo.txt
				lista=$(grep -f /home/josemanuel/boletinscript1/informe.txt /home/josemanuel/boletinscript1/bloqueo.txt)
				echo $lista
				
				
			}
	
bloquearusuario () 
			{
				read -p "Ingrese el nombre del usuario para bloquear: " usuario
					`sudo usermod -L $usuario`
					echo "Usuario $usuario bloqueado"
			}

			
desbloquearusuario () {
				read -p "Ingrese un usuario bloqueado: " usuario
					`sudo usermod -U $usuario`
					echo "Usuario $usuario desbloqueado"
			}

cerrarSesion () {
			read -p "Ingrese el nombre del usuario para cerrar su sesion: " usuario
			if who | grep -q $usuario ; then
				$tiempo
				$tiempo_activo
				$tiempo_inactivo
				if [ $tiempo_inactivo -gt 1800 ]; then 
					sudo pkill -KILL -u $usuario
					echo "Sesion de $usuario cerrada por inactividad."
				else 
					echo "El usuario $usuario ha estado conectado recientemente."
				fi 
			else 
				echo "El usuario $usuario no esta conectado."
			fi
		}





menu () {
		clear 
		while true; do
			echo "Menu Principal"
			echo "1. Lista de Bloqueados"
			echo "2. Bloquear Usuario"
			echo "3. Desbloquear Usuario"
			echo "4. Cerrar sesion usuario"
			echo "5. Salir."
			
			read -p "Seleccione una opcion: " opcion 
			
			case $opcion in 
				1) listabloqueado ;;
				2) bloquearusuario ;;
				3) desbloquearusuario ;;
				4) cerrarSesion;;
				5) clear
				exit ;;
				*) echo "Opcion incorrecta" 
				menu 
			esac
		done
	}
````
### Bloque Principal del script
````
#BloquePrincipal
clear
menu
````
### Script completo
````
#!/bin/bash
#Author:  Juan Jose Campos Gomez, Jose Manuel Lamprea, Ruben Ramirez Garcia
#Version: 1.0 
#Descripcion: Scrip que imprime un menu y ofrece las siguientes opciones. (1) Una lista de los usuarios bloqueados en el sistema (2) La posibilidad de bloquear un usuario (3) La posibilidad de desbloquear un usuario (4) Cerrar la sesion de un usuario (5)Salir del script
#Parámetros/Variables:
		tiempo=$(date -d "$(who | grep $usuario | awk '{print $4}')" +%s)
		tiempo_activo=$(date +%s)
		tiempo_inactivo=$((tiempo_activo - tiempo ))
#Comentarios:
#Funciones

listabloqueado () 
			{
				echo "Usuarios bloqueados: "
				awk -F: '$3 >= 1000 && $3 < 2000 {print $1}' /etc/passwd > informe.txt
				sudo passwd -S -a | grep " L " | cut -d " " -f1 > bloqueo.txt
				lista=$(grep -f informe.txt bloqueo.txt)
				echo $lista
				
				
			}
	
bloquearusuario () 
			{
				read -p "Ingrese el nombre del usuario para bloquear: " usuario
					`sudo usermod -L $usuario`
					echo "Usuario $usuario bloqueado"
			}

			
desbloquearusuario () {
				read -p "Ingrese un usuario bloqueado: " usuario
					`sudo usermod -U $usuario`
					echo "Usuario $usuario desbloqueado"
			}

cerrarSesion () {
			read -p "Ingrese el nombre del usuario para cerrar su sesion: " usuario
			if who | grep -q $usuario ; then
				$tiempo
				$tiempo_activo
				$tiempo_inactivo
				if [ $tiempo_inactivo -gt 1800 ]; then 
					sudo pkill -KILL -u $usuario
					echo "Sesion de $usuario cerrada por inactividad."
				else 
					echo "El usuario $usuario ha estado conectado recientemente."
				fi 
			else 
				echo "El usuario $usuario no esta conectado."
			fi
		}





menu () {
		clear 
		while true; do
			echo "Menu Principal"
			echo "1. Lista de Bloqueados"
			echo "2. Bloquear Usuario"
			echo "3. Desbloquear Usuario"
			echo "4. Cerrar sesion usuario"
			echo "5. Salir."
			
			read -p "Seleccione una opcion: " opcion 
			
			case $opcion in 
				1) listabloqueado ;;
				2) bloquearusuario ;;
				3) desbloquearusuario ;;
				4) cerrarSesion;;
				5) clear
				exit ;;
				*) echo "Opcion incorrecta" 
				menu 
			esac
		done
	}
#BloquePrincipal
clear
menu
````
