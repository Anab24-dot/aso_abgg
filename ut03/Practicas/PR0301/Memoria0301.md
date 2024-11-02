# Práctica 0301
## Ejercicios con el comando  if
### - Comprobación de número par o impar:
```bash
  GNU nano 6.2                                                                                             par-impar.sh *                                                                                                    
#!/bin/bash
echo "Introduce un número:"
read numero
if ((numero % 2 == 0));
        then
                echo "El número $numero es par."
        else
                echo "El número $numero es impar."
fi
```
```bash
vagrant@ubuntu2204:~$ ./par-impar.sh
-bash: ./par-impar.sh: Permission denied
vagrant@ubuntu2204:~$ chmod +x par-impar.sh
vagrant@ubuntu2204:~$ ./par-impar.sh
Introduce un número:
2
El número 2 es par.
vagrant@ubuntu2204:~$ ./par-impar.sh
Introduce un número:
5
El número 5 es impar.
```
### - Verificación de archivo

```bash

#!/bin/bash
echo "Introduce  la ruta del archivo:"
read ruta
if [[ -e "$ruta" ]];
        then
        if [[ -r "$ruta" ]];
                then
                        echo "El archivo  si existe y si tiene permisos de lectura."
                else 
                        echo "El archivo si existe pero no tiene permisos de lectura."
        fi
        else
                echo "El archivo no existe."
```
```bash
vagrant@ubuntu2204:~$ ./verificacion.sh
Introduce  la ruta del archivo:
/home
El archivo  si existe y si tiene permisos de lectura.
vagrant@ubuntu2204:~$ ./verificacion.sh
Introduce  la ruta del archivo:
/casa
El archivo no existe.
```
### - Comparación de dos números
```bash
#!/bin/bash
echo "Introduce el primer número:"
read nume1
echo "Introduce el segundo número:"
read nume2

if ((nume1 > nume2));
        then
                echo "$nume1 es mayor que el $nume2."
elif ((nume1 < nume2)); 
        then
                echo "$nume2 es mayor que el $nume1."
else
        echo "Los dos números son iguales"
fi
```
```bash
vagrant@ubuntu2204:~$ ./comparacion.sh
Introduce el primer número:
4
Introduce el segundo número:
6
6 es mayor que el 4.
vagrant@ubuntu2204:~$ ./comparacion.sh
Introduce el primer número:
14
Introduce el segundo número:
5
14 es mayor que el 5.
vagrant@ubuntu2204:~$ ./comparacion.sh
Introduce el primer número:
5
Introduce el segundo número:
5
Los dos números son iguales
```
### - Validación de contraseña
```bash
  GNU nano 6.2                                                                                            contrasena.sh *                                                                                                    
#!/bin/bash
contrasena-predefinida=" contraseña-siempre"
echo "Introduce una contraseña:"
read -s contrasena_usuario
if [[ "$contrasena_usuario" == "$contrasena-predefinida" ]];
        then
                echo "La contraseña introducida es correcta."
        else
                echo "La contraseña introducida NO es correcta."
fi
```
```bash
vagrant@ubuntu2204:~$ ./contrasena.sh
./contrasena.sh: line 2: contrasena-predefinida= contraseña-siempre: command not found
Introduce una contraseña:
La contraseña introducida NO es correcta.
```
### - Comprobación de directorio

```bash
#!/bin/bash
echo "Introduce el nombre del directorio:"
read directorio

if [[ -d "$directorio" ]];
        then
                if [[ -w "$directorio" ]];
                        then
                                echo "El directorio $directorio si existe y si tiene permisos de escritura"
                else
                        echo  "El directorio $direcdtorio si existe pero no tiene permisos de escritura."
                fi
        else 
                echo "El directorio  $directorio  no existe por tanto vamos a crearlo"
                mkdir "$directorio"
                echo "El directorio ha sido creado."
fi
```
```bash
vagrant@ubuntu2204:~$ chmod +x directorio.sh
vagrant@ubuntu2204:~$ ./directorio.sh
Introduce el nombre del directorio:
head
El directorio  head  no existe por tanto vamos a crearlo
El directorio ha sido creado.
vagrant@ubuntu2204:~$ ls -l
total 24
-rwxrwxr-x 1 vagrant vagrant  292 Oct 31 17:40 comparacion.sh
-rwxrwxr-x 1 vagrant vagrant  296 Oct 31 17:56 contrasena.sh
-rwxrwxr-x 1 vagrant vagrant  463 Oct 31 18:09 directorio.sh
drwxrwxr-x 2 vagrant vagrant 4096 Oct 31 18:10 head
-rwxrwxr-x 1 vagrant vagrant  166 Oct 31 17:20 par-impar.sh
-rwxrwxr-x 1 vagrant vagrant  299 Oct 31 17:33 verificacion.sh
```
### - Verificar si el usuario es root
```bash
  GNU nano 6.2                                                                verificar-root.sh *                                                                        
#!/bin/bash
if [[ "$USER" -ne 0 ]];
        then
                echo "El script no se está ejecutando por el usuario root."
        else
                echo  "El scriot si está siendo  ejecutado por el usuario root."
fi
```
```bash
vagrant@ubuntu2204:~$ ./verificar-root.sh
El script si está siendo ejecutado por el usuario root.
```
### - Calificación de un examen
```bash
#!/bin/bash
echo "Introduce la nota del examen (de 0 a 10):"
read nota

if ((nota >=5 ));
        then
                echo "El examen está aprobado"
        else 
                echo "El examen está suspenso"
fi
```
```bash
vagrant@ubuntu2204:~$ chmod +x examen.sh
vagrant@ubuntu2204:~$ ./examen.sh
Introduce la nota del examen (de 0 a 10):
3
El examen está suspenso
vagrant@ubuntu2204:~$ ./examen.sh
Introduce la nota del examen (de 0 a 10):
8
El examen está aprobado
```
### - Comprobación del espacio en disco
```bash
#!/bin/bash
espacio-libre=$(df / | grep '/' | awk '{print $5}' | sed 's/%//' )

if  (( espacio-libre < 10 ));
        then
                echo "CUIDADO!!: El espacioi del disco es menor al 10%"
        else
                echo "Tiene suficiente espacio en el disco"
fi
```
### - Menú de opciones
```bash
  GNU nano 6.2                                                                 menu-opciones.sh                                                                          
#!/bin/bash
echo "Elige un número:"
echo "1."
echo "2."
echo "3."
read numero
if [ "$numero" -eq 1 ];
        then
                echo "Has elegido el número 3"
elif [ "$numero" -eq 2 ];
        then
                echo "Has elegido el número 5"
elif [ "$numero" -eq 3 ];
        then
                echo "Has elegido el número 7"
else
                echo "Número incorrecto. Elige otro número"
fi
```
```bash
vagrant@ubuntu2204:~$ ./menu-opciones.sh
Elige un número:
1.
2.
3.
2
Has elegido el número 5
```
### - Evaluación edad
```bash
#!/bin/bash
echo "Introduce tu edad:"
read edad
if (( edad < 18 ));
        then
                echo "Eres menor de edad"
elif (( edad >= 18 && edad <= 65 ));
        then
                echo "Eres adulto"
else
                echo "Eres mayor de 65 años"
fi
```
```bash
vagrant@ubuntu2204:~$ ./evaluacion-edad.sh
Introduce tu edad:
54
Eres adulto
vagrant@ubuntu2204:~$ ./evaluacion-edad.sh
Introduce tu edad:
15
Eres menor de edad
vagrant@ubuntu2204:~$ ./evaluacion-edad.sh
Introduce tu edad:
70
Eres mayor de 65 años
```
### - Contar líneas de un archivo
```bash
#!/bin/bash
echo "Introduce un nombre de archivo:"
read archivo

if [ -e "$archivo" ];
        then
                linea=$(wc -l  < "$archivo")
                echo "El archivo $archivo consta de $linea lineas"
else
                echo "El archivo $archivo no existe."
fi
```
```bash
vagrant@ubuntu2204:~$ ./contar-lineas.sh
Introduce un nombre de archivo:
evaluacion-edad.sh
El archivo evaluacion-edad.sh consta de 12 lineas
vagrant@ubuntu2204:~$ ./contar-lineas.sh
Introduce un nombre de archivo:
edad.sh
El archivo edad.sh no existe.
```
