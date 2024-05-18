
### Ejercicio 2

Realiza un script llamado usuariosBloqueados.sh, que nos muestre un menú:
- 1- Usuarios Bloqueados.
- 2- Bloquear un usuario.
- 3- Desbloquear usuario.
- 4-- Cerrar sesión usuario
- 5- Salir
 <br>
 
>[!NOTE]
>Cada opción del menú corresponde con una función:<br>
>UsuariosBloqueados → nos muestra en pantalla los usuarios (uid>1000 y <2000) que tengan la cuenta bloqueada. <br>
>BloquearUsuario → Nos pregunta el nombre de un usuario y lo bloqueamos. <br>
>DesbloquearUsuario → Nos pregunta el nombre de un usuario y lo desbloqueamos. <br>
>CerrarSesion → Nos pregunta el nombre de un usuario, y si el usuario lleva más de 30 minutos (1800 seg) sin actividad, se le cierra la sesión.
<br>
<br>

Este era el script que se nos solicitaba y a continuación explicaremos un poco paso a paso;
### 1- Usuario bloqueados
````
listabloqueado () 
			{
				echo "Usuarios bloqueados: "
				awk -F: '$3 >= 1000 && $3 < 2000 {print $1}' /etc/passwd > /home/josemanuel/boletinscript1/informe.txt
				sudo passwd -S -a | grep " L " | cut -d " " -f1 > /home/josemanuel/boletinscript1/bloqueo.txt
				lista=$(grep -f /home/josemanuel/boletinscript1/informe.txt /home/josemanuel/boletinscript1/bloqueo.txt)
				echo $lista
			}
````

En esta función nos crea dos tipos de archivos, en uno de ellos los usuarios ccon su UID comprendidos entre 1000 y 2000  y lo redirige a una informe.txt
luego mostramos el estado de las cuentas y nos filtra los usuarios con la  "L" de locked y redirige toda esa informacion al archivo bloqueo.txt.
En cuanto se tienen ambos archivos se comparan en una lista y la impreme mostrando los usuarios que estan bloqueados.
<br>
### 2- Bloquear un Usuario
````
bloquearusuario () 
			{
				read -p "Ingrese el nombre del usuario para bloquear: " usuario
					`sudo usermod -L `$usuario`
					echo "Usuario $usuario bloqueado"
			}
````
 Aqui primero preguntamos por el nombre del usuario que queramos bloquear y luego mediante el comando usermod -L bloqueamos dicho usuario y nos imprime por pantalla que el usuario seleccionado ha sido bloqueado.
<br>
### 3- Desbloquear un usuario
````
 desbloquearusuario ()
  			{
				read -p "Ingrese un usuario bloqueado: " $usuario
					`sudo usermod -U `$usuario`
					echo "Usuario $usuario desbloqueado"
			}
````
   Como en el ejercicio anterior, primero preguntamos por un usuario bloqueado y lo desbloqueamos con el comando usermod -U y nos imprime por pantalla el usuario desbloqueado.


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
				echo "El usuario $susuario no esta conectado."
			fi
		}


  En esta funcion primero preguntamos el ususario, luego comprobamos si esta conectado, para luego calcular el tiempo de inactividad, mas tarde con un "if" verificamos si ese usuario ha sobrepaso el limite de inactividad y proceder a cerrar su sesion.
  la funcion termina segun su tiempo inactivo te impreme por pantalla que el ususario ha estado conectado recientemente o por el contrario que su sesion ha sido cerrada.


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

 En esta funcion mediante un while true y un case hemos creado un bucle de un menu con las diferentes opciones donde cada opcion llama a una diferente funcion.
> [!CAUTION]
>Modifica esto.
