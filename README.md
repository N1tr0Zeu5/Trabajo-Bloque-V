#!/bin/bash
#Author: Jose Manuel Lamprea
#Version: 1.0 
#Descripcion: usuariosBloqueados
#Parámetros/Variables:
		tiempo=$(date -d "$(who | grep $usuario | awk '{print $4}')" +%s)
		tiempo_activo=$(date +%s)
		tiempo_inactivo=$((tiempo_activo - tiempo ))
#Comentarios: 
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
				if grep -q  "^$usuario: " /etc/shadow; then
					sudo usermod -L "$usuario"
					echo "Usuario $usuario bloqueado"
				fi
			}
			
desbloquearusuario () {
				read -p "Ingrese un usuario bloqueado: " $usuario
				if grep -q "^$usuario: " /etc/shadow; then
					sudo usermod -U "$usuario"
					echo "Usuario $usuario desbloqueado"
				fi
			}

cerrarSesion () {
			read -p "Ingrese el nombre del usuario para cerrar su sesion: " usuario
			if who | grep -q $usuario ; then
				$tiempo
				$tiempo_activo
				$tiempo_inactivo
				if [ $tiempo_inactivo -gt 1800 ]; then 
					sudo pkill -KILL -u $usuario
					echo "Sesion de %usuario cerrada por inactividad."
				else 
					echo "El usuario $usuario ha estado conectado recientemente."
				fi 
			else 
				echo "El usuario $susuario no esta conectado."
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
