
#!/bin/bash
#Author: 
#Version:
#Descripcion: 
#Variables/Parametros:
nombre=$1
numeroUsuario=$2
fechaactual=$(date +%d-%m-%Y)
archivousuario="usuarioscreados-fechaactual.tmp"

#Comentarios:
#Funciones
#BloquePrincipal:
clear 

  for i in $(seq 1 $numeroUsuario);
                  do
                          nombreUsuario="$nombre$i"
                          password="$nombreUsuario"
                          sudo useradd -m -p $(echo -n "password" | openssl passwd -l -stidin) "nombreUsuario"
                          sudo chage -d 0 $nombreUsuario
                          echo "$nombreUsuario:$password" >> "$archivousuario"
                  done

                  echo "Usuarios creados y contraseñas: "
                  cat "$archivousuario"
