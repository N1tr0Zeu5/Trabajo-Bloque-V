### Cabecera
````
#!/bin/bash
#Author: Juanjo, Ruben, Jose Manuel
#Version:
#Descripcion: crea ususarios de forma masiva
#Variables/Parametros:
nombre=$1
fecha=`date +%d-%m-%Y`
informeUsuario="usuarioscreados-$fecha.tmp"
#Comentarios:
#Funciones
````
> [!NOTE]
> Hemos elegido por no usar funciones, ya que al tratarse de parametros preferimos no tener que pasarselos a la funcion, para evitar fallos.

### Bloque Principal 
````
#BloquePrincipal:
clear 

  for i in $(seq 1 1 $2)
                  do
                          nombreUsuario="$nombre$i"
                          sudo useradd -m -p $(echo -n "$nombreUsuario" | openssl passwd -1 -stidin) "$nombreUsuario"
                          sudo chage -d 0 "$nombreUsuario"
                          echo "$nombreUsuario:$nombreUsuario" >> $informeUsuario
                  done

echo "Usuarios creados y contraseñas: "
cat $informeUsuario
````
### Script Completo
````
#!/bin/bash
#Author: 
#Version:
#Descripcion: 
#Variables/Parametros:
nombre=$1
fecha=`date +%d-%m-%Y`
informeUsuario="usuarioscreados-$fecha.tmp"

#Comentarios:
#Funciones
#BloquePrincipal:
clear 

  for i in $(seq 1 1 $2);
                  do
                          nombreUsuario="$nombre$i"
                          sudo useradd -m -p $(echo -n "$nombreUsuario" | openssl passwd -1 -stidin) "nombreUsuario"
                          sudo chage -d 0 "$nombreUsuario"
                          echo "$nombreUsuario:$nombreUsuario" >> $informeUsuario
                  done

echo "Usuarios creados y contraseñas: "
cat $informeUsuario
````

> [!CAUTION]
>en este script nos encontramos con varios problemas pese a ser un codigo simple sin funciones, a la hora de conseguir que el nombre funcionase tambien como contraseña teniamos
> problemas ya que durante la creacion del script no leia la letra "ñ" y charlando con varios compañeros de otros grupos, todos llegamos a la misma conclusion despues de un tiempo




