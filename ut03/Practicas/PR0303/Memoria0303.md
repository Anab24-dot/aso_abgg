# PRÁCTICA 0303
## EJERCICIOS SOBRE LOS COMANDOS WHILE, UNTIL Y FOR
### - Contar hasta 10 con for
```bash
#!/bin/bash
for n in {1..10};
 do
  echo $i
done
```
```bash
vagrant@ubuntu2204:~$ ./contar-diez.sh
1
2
3
4
5
6
7
8
9
10
```
### - Sumar los primeros 50 números
```bash
#!/bin/bash
suma=0
for n in {1..50}; 
 do
  suma=$((suma + n))
done
echo "La suma de los primeros 50 números es: $suma"
```
```bash
vagrant@ubuntu2204:~$ ./sumar-cincuenta.sh
La suma de los primeros 50 números es: 1275
```
### - Tabla de multiplicar
```bash
#!/bin/bash
read -p "Introduce un número: " num
for n in {1..10}; 
 do
  echo "$num x $i = $((num * n))"
done
```
```bash
vagrant@ubuntu2204:~$ ./tabla-multiplicar.sh
Introduce un número: 14
14 x 1 = 14
14 x 2 = 28
14 x 3 = 42
14 x 4 = 56
14 x 5 = 70
14 x 6 = 84
14 x 7 = 98
14 x 8 = 112
14 x 9 = 126
14 x 10 = 140
```
### - Imprimir cada letra
```bash
#!/bin/bash
read -p "Escribe una palabra: " palabra
for letra in $(echo $palabra | grep -o .); 
 do
  echo $letra
done
```
El comando grep -o hace que grep muestre solo las coincidencias exactas encontradas.
El comando "grep -o ." busca cada caracter individual en el texto y lo imprime por separado. Cada caracter tiene su propia línea. 
```bash
vagrant@ubuntu2204:~$ ./imprimir-letra.sh
Escribe una palabra: night
n
i
g
h
t
vagrant@ubuntu2204:~$ ./imprimir-letra.sh
Escribe una palabra: noche
n
o
c
h
e
```
### - Contar números pares del 1 al 20 con while
```bash
#!/bin/bash
n=2
while [ $n -le 20 ];
 do
  echo $n
  n=$((n + 2))
done
```
```bash
vagrant@ubuntu2204:~$ ./contar-pares.sh
2
4
6
8
10
12
14
16
18
20
```
### - Suma de dígitos
```bash
#!/bin/bash
read -p "Escribe un número: " num
suma=0
while [ $num -gt 0 ]; 
 do
  digito=$((num % 10))
  suma=$((suma + digito))
  num=$((num / 10))
done
echo "La suma de los dígitos es: $suma"
```
```bash
vagrant@ubuntu2204:~$ ./suma-digitos.sh
Escribe un número: 528
La suma de los dígitos es: 15
vagrant@ubuntu2204:~$ ./suma-digitos.sh
Escribe un número: 9111
La suma de los dígitos es: 12
```
### - Cuenta regresiva
```bash
#!/bin/bash
read -p "Escribe un número: " num
until [ $num -lt 0 ]; 
 do
  echo $num
  num=$((num - 1))
done
```
```bash
vagrant@ubuntu2204:~$ ./cuenta-regresiva.sh
Escribe un número: 6
6
5
4
3
2
1
0
vagrant@ubuntu2204:~$ ./cuenta-regresiva.sh
Escribe un número: 2
2
1
0
```
### - Imprimir solo archivos .txt
```bash
#!/bin/bash
echo "Escribe el nombre del directorio:"
read directorio
if [ -d "$directorio" ];
        then
for archivo in *;
 do
  if [[ $archivo == *.txt ]];
         then
         echo $archivo
  fi
done
else
```
### - Factorial de un número
```bash
#!/bin/bash
read -p "Escribe un número: " num
factorial=1
for ((n=1; n<=num; n++));
 do
  factorial=$((factorial * n))
done
echo "El factorial de $num es: $factorial"
```
```bash
vagrant@ubuntu2204:~$ ./factorial-numero.sh
Escribe un número: 5
El factorial de 5 es: 120
vagrant@ubuntu2204:~$ ./factorial-numero.sh
Escribe un número: 2
El factorial de 2 es: 2
```
### - Verificar contraseña
```bash
#!/bin/bash
password="1234"
input=""
until [ "$input" == "$password" ];
 do
  read -sp "Introduce la contraseña: " input
  echo
done
echo "Contraseña correcta"
```
```bash
vagrant@ubuntu2204:~$ ./verificar-contrasena.sh
Introduce la contraseña:
Introduce la contraseña:
Introduce la contraseña:
Introduce la contraseña:
Contraseña correcta
```
### - Adivinar un número
```bash
#!/bin/bash
numero=$((RANDOM % 10 + 1))
intento=0
while [ $intento -ne $numero ];
 do
  read -p "Adivina el número (1-10): " intento
  if [ $intento -eq $numero ];
         then
        echo "¡Correcto!"
  else
         echo "Vuelve a jugar"
  fi
done
```
```bash
vagrant@ubuntu2204:~$ ./adivinar-numero.sh
Adivina el número (1-10): 2
Vuelve a jugar
Adivina el número (1-10): 5
Vuelve a jugar
Adivina el número (1-10): 1
Vuelve a jugar
Adivina el número (1-10): 3
Vuelve a jugar
Adivina el número (1-10): 4
Vuelve a jugar
Adivina el número (1-10): 6
Vuelve a jugar
Adivina el número (1-10): 7
Vuelve a jugar
Adivina el número (1-10): 8
¡Correcto!
```
### - Mostrar la fecha n veces
```bash
#!/bin/bash
read -p "¿Dime un número?: " n
for ((i=1; i<=n; i++)); 
 do
  date
done
```
```bash
vagrant@ubuntu2204:~$ ./mostrar-fecha.sh
¿Dime un número?: 5
Sun Nov  3 04:02:16 PM UTC 2024
Sun Nov  3 04:02:16 PM UTC 2024
Sun Nov  3 04:02:16 PM UTC 2024
Sun Nov  3 04:02:16 PM UTC 2024
Sun Nov  3 04:02:16 PM UTC 2024
```
### - Promedio de números ingresados
```bash
#!/bin/bash
suma=0
contar=0
while true;
 do
  read -p "Introduce un número (o 'fin' para terminar): " primero
  if [ "$primero" == "fin" ];
         then
         break
  fi
  suma=$((suma + primero))
  contar=$((contar + 1))
done
if [ $contar -ne 0 ];
         then
         promedio=$(echo "$suma / $contar" | bc -l)
         echo "El promedio es: $promedio"
else
         echo "No dijiste números"
fi
```
```bash
vagrant@ubuntu2204:~$ ./promedio-numero.sh
Introduce un número (o 'fin' para terminar): 2
Introduce un número (o 'fin' para terminar): 5
Introduce un número (o 'fin' para terminar): fin
El promedio es: 3.50000000000000000000
vagrant@ubuntu2204:~$ ./promedio-numero.sh
Introduce un número (o 'fin' para terminar): 2
Introduce un número (o 'fin' para terminar): 2
Introduce un número (o 'fin' para terminar): 2
Introduce un número (o 'fin' para terminar): fin
El promedio es: 2.00000000000000000000
```
### - Contar palabras en una cadena
```bash
#!/bin/bash
read -p "Escribe una frase: " frase
num_palabra=$(echo $frase | wc -w)
echo "La frase tiene $num_palabra palabras"
```
```bash
vagrant@ubuntu2204:~$ ./contar-palabra.sh
Escribe una frase: la luna es un globo
La frase tiene 5 palabras
```
### - Juego de adivinar con límites dinámicos
```bash
#!/bin/bash
numero=$((RANDOM % 100 + 1))
intento=0
while [ $intento -ne $numero ];
 do
  read -p "Adivina el número (1-100): " intento
  if [ $intento -lt $numero ];
         then
         echo "El número es mayor"
  elif [ $intento -gt $numero ];
         then
         echo "El número es menor"
  else
    echo "¡Correcto!"
  fi
done
```
```bash
vagrant@ubuntu2204:~$ ./adivinar-limites.sh
Adivina el número (1-100): 23
El número es menor
Adivina el número (1-100): 15
El número es menor
Adivina el número (1-100): 8
El número es mayor
Adivina el número (1-100): 10
El número es mayor
Adivina el número (1-100): 12
El número es menor
Adivina el número (1-100): 11
¡Correcto!
```
### - Archivo con nombres de directorios
```bash
#!/bin/bash
ruta=$(pwd)
for f in $ruta/; 
         do
          if [ -d $f ]
          then 
          echo $f >> ./directorios.txt
          fi
done
```
```bash
vagrant@ubuntu2204:~$ ./nombres-directorios.sh
vagrant@ubuntu2204:~$ ls
adivinar-limites.sh  contar-palabra.sh    directorios.txt      imprimir-txt.sh         promedio-numero.sh  tabla-multiplicar.sh
adivinar-numero.sh   contar-pares.sh      factorial-numero.sh  mostrar-fecha.sh        suma-digitos.sh     verificar-contrasena.sh
contar-diez.sh       cuenta-regresiva.sh  imprimir-letra.sh    nombres-directorios.sh  sumar-cincuenta.sh
```
### - Generar archivos de texto numerados
```bash
#!/bin/bash
read -p "¿Número de  archivos?: " n
for ((x=1; x<=n; x++)); 
         do
         touch "archivo$i.txt"
done
echo "$n archivos creados"
```
```bash
#!/bin/bash
read -p "¿Número de  archivos?: " n
for ((x=1; x<=n; x++)); 
         do
         touch "archivo$x.txt"
done
echo "$n archivos creados"
```
```bash
vagrant@ubuntu2204:~$ ./generar-archivos.sh
¿Número de  archivos?: 2
2 archivos creados
vagrant@ubuntu2204:~$ ls -l
total 72
-rwxrwxr-x 1 vagrant vagrant 318 Nov  3 16:34 adivinar-limites.sh
-rwxrwxr-x 1 vagrant vagrant 240 Nov  3 15:57 adivinar-numero.sh
-rw-rw-r-- 1 vagrant vagrant   0 Nov  3 16:58 archivo1.txt
-rw-rw-r-- 1 vagrant vagrant   0 Nov  3 16:58 archivo2.txt
-rwxrwxr-x 1 vagrant vagrant  49 Nov  3 08:18 contar-diez.sh
```
### - Conteo de vocales en una cadena
```bash
#!/bin/bash
read -p "Escribe una cadena: " cadena
vocales=0
for letra in $(echo $cadena | grep -o .); 
         do
         if [[ $letra =~ [aeiouAEIOU] ]]; 
                 then
                 vocales=$((vocales + 1))
         fi
         done
echo "La cadena tiene $vocales vocales"
```
```bash
vagrant@ubuntu2204:~$ ./conteo-vocales.sh
Escribe una cadena: ana
La cadena tiene 2 vocales
vagrant@ubuntu2204:~$ ./conteo-vocales.sh
Escribe una cadena: murcielago
La cadena tiene 5 vocales
```
### - Validación de entrada
```bash
#!/bin/bash
numero=0
until [[ $numero -ge 1 && $numero -le 10 ]]; 
 do
  read -p "Introduce un número entre 1 y 10: " numero
done
echo "Número válido: $numero"
```
```bash
vagrant@ubuntu2204:~$ ./validar-entrada.sh
Introduce un número entre 1 y 10: 2
Número válido: 2
vagrant@ubuntu2204:~$ ./validar-entrada.sh
Introduce un número entre 1 y 10: 5
Número válido: 5
```
### - Script de copia de seguridad
```bash
#!/bin/bash
mkdir -p backup
for archivo in *.txt; 
 do
  if [ -f "$archivo" ]; 
         then
         cp "$archivo" backup/
  fi
done
echo "Archivos .txt copiados a la carpeta backup"
```
```bash
vagrant@ubuntu2204:~$ ./copia-seguridad.sh
Archivos .txt copiados a la carpeta backup
vagrant@ubuntu2204:~$ ls -l
total 88
-rwxrwxr-x 1 vagrant vagrant  318 Nov  3 16:34 adivinar-limites.sh
-rwxrwxr-x 1 vagrant vagrant  240 Nov  3 15:57 adivinar-numero.sh
-rw-rw-r-- 1 vagrant vagrant    0 Nov  3 16:58 archivo1.txt
-rw-rw-r-- 1 vagrant vagrant    0 Nov  3 16:58 archivo2.txt
drwxrwxr-x 2 vagrant vagrant 4096 Nov  3 17:08 backup
```





