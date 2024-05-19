### Ejercicio 4

Buscamos crear masivamente usuarios mediante parametros.
<br>
El primer parametro $1 sera el nombre comun de todos los usuarios, y el segundo parametro $2 sera la cantidad de usuarios que deseamos crear.
<br>
> [!NOTE]
> Hemos elegido por no usar funciones, ya que al tratarse de parametros preferimos no tener que pasarselos a la funcion, para evitar fallos.
<br>
Utilizamos un bucle for, para poder crear el numero de usuarios igual al valor del parametro $2


````

for i in $(seq 1 1 $2);
                  do
                          nombreUsuario="$nombre$i"
                          sudo useradd -m -p $(echo -n "$nombreUsuario" | openssl passwd -1 -stdin) "$nombreUsuario" > /dev/null 2>&1
                          sudo chage -d 0 "$nombreUsuario"
                          echo "$nombreUsuario:$nombreUsuario" >> $informeUsuario
                  done
````
<br>

> [!CAUTION]
> En este script nos encontramos con varios problemas pese a ser un codigo simple sin funciones, a la hora de conseguir que el nombre funcionase tambien como contraseña teniamos
> problemas ya que durante la creacion del script no leia la letra "ñ" y charlando con varios compañeros de otros grupos, todos llegamos a la misma conclusion despues de un tiempo
