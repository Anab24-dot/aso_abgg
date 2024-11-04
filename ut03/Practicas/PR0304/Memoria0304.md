# PRÁCTICA 0304
## EJERCICIOS ENTRADA Y SALIDA DE DATOS
### Buscar palabra en archivo
```bash
#!/bin/bash
read -p "Escribe el nombre del archivo" archivo
if [[ -f $archivo ]];
        then 
        read -p "Escribe la palabra clave:" palabra
        grep "$palabra" "$archivo"
else
        echo "Archivo desconocido"
fi
```
```bash
vagrant@ubuntu2204:~$ ./buscar-palabra.sh
Escribe el nombre del archivoana.txt
Escribe la palabra clave:luna
la luna es un globo que se le escapó a un niño bobo
al sol le llaman Lorenzo y a la luna Catalina
```

### Contar palabras
```bash
#!/bin/bash
read -p "Escribe el nombre del archivo:" archivo
if [[ -f $archivo ]];
         then
         num_palabras=$(wc -w < "$archivo")
        echo "El archivo tiene $num_palabras palabras."
else
        echo "Archivo desconocido."
fi
```
```bash
vagrant@ubuntu2204:~$ ./contar-palabra.sh
Escribe el nombre del archivo:ana.txt
El archivo tiene 47 palabras.
```
### Suma de números
```bash
#!/bin/bash
read -p "Escribe el nombre del archivo de texto:" archivo
suma=0
if [[ -f $archivo ]];
         then
         while IFS= read -r numero;     
         do
                 suma=$((suma + numero))
         done < "$archivo"
  echo "La suma es: $suma"
else
  echo "Archivo desconocido."
fi
```
```bash
vagrant@ubuntu2204:~$ ./suma-numeros.sh
Escribe el nombre del archivo de texto:ananumeros.txt
La suma es: 78
  GNU nano 6.2                                                                  ananumeros.txt                                                                           2
4
6
8
10
12
11
9
7
5
3
1
```
### Datos de usuario

Creamos el archivo datos-usuario.csv
```bash
  GNU nano 6.2                                                                datos-usuario.csv *                                                                        
10100100X, victor, gonzález rodríguez, asir, aso, 6
12345678A, pepe, fernández fernández, asir, aso, 8
10100100X, victor, gonzález rodríguez, asir, iso, 5
```
```bash
  GNU nano 6.2                                                                  datos-user.sh                                                                            #!/bin/bash
read -p "Escribe el nombre del archivo que se desea analizar:" archivo
read -p "Escribe el NIF del alumno: " nif

if [[ -f $archivo ]];
         then
                 grep "$nif" "$archivo" | while IFS=,
                 read -r nif nombre apellidos ciclo modulo nota;
                 do
                         echo "El alumno $nombre $apellidos tiene una calificación de $nota puntos en el módulo $modulo."
                 done
        else
                 echo "El archivo $archivo no existe."
fi
```
```bash
   vagrant@ubuntu2204:~$ ./datos-user.sh
Escribe el nombre del archivo que se desea analizar:datos-usuario.csv
Escribe el NIF del alumno: 12345678A
El alumno  pepe  fernández fernández tiene una calificación de  8 puntos en el módulo  aso.
```            
### Líneas con mas de N caracteres
```bash
#!/bin/bash
read -p "Escribe un nombre de archivo:" archivo
read -p "Indica el número mínimo de caracteres:" n

if [[ -f $archivo ]];
         then
         while IFS= 
                 read -r linea; 
                 do
                         if [[ ${#linea} -gt $n ]];     
                         then
                                 echo "$linea"
                         fi
                 done < "$archivo"
        else
                 echo "Archivo desconocido."
fi
```
```bash
vagrant@ubuntu2204:~$ ./linea-caracter.sh
Escribe un nombre de archivo:ana.txt
Indica el número mínimo de caracteres:45
la luna es un globo que se le escapó a un niño bobo
no corta el mar sino vuela un velero bergantín
```
### Estadísticas de archivos
```bash
#!/bin/bash
for archivo in "$@";
         do
                if [[ -f $archivo ]];
                 then
                         num_lineas=$(wc -l < "$archivo")
                         num_palabras=$(wc -w < "$archivo")
                         num_caracteres=$(wc -m < "$archivo")
                                 echo "Archivo: $archivo"
                                 echo "Líneas: $num_lineas, Palabras: $num_palabras, Caracteres: $num_caracteres"
                                 echo "--------------------------------------"
                 else
                         echo "El archivo $archivo no existe."
                 fi
        done
```
```bash

vagrant@ubuntu2204:~$ ./estadistica-archivo.sh ana.txt ananumeros.txt
Archivo: ana.txt
Líneas: 6, Palabras: 47, Caracteres: 236
--------------------------------------
Archivo: ananumeros.txt
Líneas: 13, Palabras: 12, Caracteres: 28
--------------------------------------
```

