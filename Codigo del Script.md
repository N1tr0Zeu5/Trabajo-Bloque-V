### Cabecera
````
#!/bin/bash
#Author: Juan Jose Campos Gomez, Jose Manuel Lamprea Demski, Rubén Ramírez García
#Version:
#Descripcion: crea ususarios de forma masiva
#Variables/Parametros:
nombre=$1
fecha=`date +%d-%m-%Y`
informeUsuario="usuarioscreados-$fecha.tmp"
#Comentarios:
#Funciones
````

### Bloque Principal 
````
#BloquePrincipal:


  for i in $(seq 1 1 $2);
                  do
                          nombreUsuario="$nombre$i"
                          sudo useradd -m -p $(echo -n "$nombreUsuario" | openssl passwd -1 -stdin) "$nombreUsuario" > /dev/null 2>&1
                          sudo chage -d 0 "$nombreUsuario"
                          echo "$nombreUsuario:$nombreUsuario" >> $informeUsuario
                  done

echo "Usuarios creados y contraseñas: "
cat $informeUsuario
````
### Script Completo
````
#!/bin/bash
#Author: Juan Jose Campos Gomez, Jose Manuel Lamprea Demski, Rubén Ramírez García
#Version: 1.0
#Descripcion: Crea ususarios de forma masiva
#Variables/Parametros: 
nombre=$1
fecha=`date +%d-%m-%Y`
informeUsuario="usuarioscreados-$fecha.tmp"
#Comentarios:
#Funciones
#BloquePrincipal:


  for i in $(seq 1 1 $2);
                  do
                          nombreUsuario="$nombre$i"
                          sudo useradd -m -p $(echo -n "$nombreUsuario" | openssl passwd -1 -stdin) "$nombreUsuario" > /dev/null 2>&1
                          sudo chage -d 0 "$nombreUsuario"
                          echo "$nombreUsuario:$nombreUsuario" >> $informeUsuario
                  done

echo "Usuarios creados y contraseñas: "
cat $informeUsuario
````




