### Cabecera
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
````
#Funciones
> [!NOTE]
> Hemos elegido por no usar funciones, ya que al tratarse de parametros preferimos no tener que pasarselos a la funcion, para evitar fallos.

### Bloque Principal 
````
#BloquePrincipal:
clear 

  for i in $(seq 1 $2);
                  do
                          nombreUsuario="$nombre$i"
                        
                          sudo useradd -m -p $(echo -n "password" | openssl passwd -l -stidin) "nombreUsuario"
                          sudo chage -d 0 $nombreUsuario
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

  for i in $(seq 1 $2);
                  do
                          nombreUsuario="$nombre$i"
                        
                          sudo useradd -m -p $(echo -n "password" | openssl passwd -l -stidin) "nombreUsuario"
                          sudo chage -d 0 $nombreUsuario
                          echo "$nombreUsuario:$nombreUsuario" >> $informeUsuario
                  done

echo "Usuarios creados y contraseñas: "
cat $informeUsuario
````
