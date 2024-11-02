# PRÁCTICA 0302a
## EJERCICIOS CON EL COMANDO CASE
### - Menú de operaciones matemáticas
```bash
#!/bin/bash

echo "Elige una operación matemática:"
echo "1. Suma"
echo "2. Resta"
echo "3. Multiplicación"
echo "4. División"
read -p "Introduce una opción (1-4): " opcion

read -p "Introduce el primer número: " num1
read -p "Introduce el segundo número: " num2

case $opcion in
 1) echo "Resultado: $(($num1 + $num2))" ;;
  2) echo "Resultado: $(($num1 - $num2))" ;;
  3) echo "Resultado: $(($num1 * $num2))" ;;
  4) 
    if [ $num2 -ne 0 ]; then
      echo "Resultado: $(($num1 / $num2))"
    else
      echo "La  división por cero no está permitida"
    fi
    ;;
  *) echo "La elección  no es correcta" ;;
  esac
  ```
  ```bash
  vagrant@ubuntu2204:~$ ./operaciones-matematicas.sh
Elige una operación matemática:
1. Suma
2. Resta
3. Multiplicación
4. División
Introduce una opción (1-4): 3
Introduce el primer número: 12
Introduce el segundo número: 4
Resultado: 48
vagrant@ubuntu2204:~$ ./operaciones-matematicas.sh
Elige una operación matemática:
1. Suma
2. Resta
3. Multiplicación
4. División
Introduce una opción (1-4): 4
Introduce el primer número: 56
Introduce el segundo número: 0
La  división por cero no está permitida
vagrant@ubuntu2204:~$ ./operaciones-matematicas.sh
Elige una operación matemática:
1. Suma
2. Resta
3. Multiplicación
4. División
Introduce una opción (1-4): 6
Introduce el primer número: 12
Introduce el segundo número: 3
La elección  no es correcta
```
### - Identificación de extensión de archivo
```bash
#!/bin/bash

read -p "Introduce el nombre del archivo: " archivo

case $archivo in
  *.txt) echo "Se corresponde con  un archivo de texto" ;;
  *.zip) echo "Se corresponde con  un archivo comprimido (.zip)" ;;
  *.tar.gz) echo "Se corresponde con un archivo comprimido (.tar.gz)" ;;
  *) echo "Otro tipo de archivo" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./extension-archivo.sh
Introduce el nombre del archivo: ana.txt
Se corresponde con  un archivo de texto
vagrant@ubuntu2204:~$ ./extension-archivo.sh
Introduce el nombre del archivo: ana.md
Otro tipo de archivo
```
### - Conversor de unidades
```bash
#!/bin/bash

echo "Que conversión quieres realizar:"
echo "1. Metros a kilómetros"
echo "2. Pies a metros"
echo "3. Kilómetros a millas"
echo "4. Pies a pulgadas"
echo "5. Millas a metros"
read -p "Introduce una opción (1-5): " opcion

read -p "Introduce la medida que quieres calcular:" medida

case $opcion in
  1) echo "Resultado: $(echo "$medida / 1000" | bc -l) km" ;;
  2) echo "Resultado: $(echo "$medida * 0.3048" | bc -l) metros" ;;
  3) echo "Resultado: $(echo "$medida * 0.621371" | bc -l) millas" ;;
  4) echo "Resultado: $(echo "$medida * 12" | bc -l) pulgadas" ;;
  5) echo "Resultado: $(echo "$medida * 1609.34" | bc -l) metros" ;;
  *) echo "Opción no permitida" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./conversor-unidades.sh
Que conversión quieres realizar:
1. Metros a kilómetros
2. Pies a metros
3. Kilómetros a millas
4. Pies a pulgadas
5. Millas a metros
Introduce una opción (1-5): 1
Introduce la medida que quieres calcular:1000
Resultado: 1.00000000000000000000 km
vagrant@ubuntu2204:~$ ./conversor-unidades.sh
Que conversión quieres realizar:
1. Metros a kilómetros
2. Pies a metros
3. Kilómetros a millas
4. Pies a pulgadas
5. Millas a metros
Introduce una opción (1-5): 4
Introduce la medida que quieres calcular:25
Resultado: 300 pulgadas
```
### - Menú de configuración del sistema
```bash
#!/bin/bash

echo "Elige que deseas hacer:"
echo "1. Apagar el sistema"
echo "2. Reiniciar el sistema"
echo "3. Cerrar sesión"
read -p "Introduce una opción (1-3): " opcion

case $opcion in
  1) sudo shutdown -h now ;;
  2) sudo reboot ;;
  3) pkill -KILL -u $USER ;;
  *) echo "No se puede realizar" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./configuracion.sh
Elige que deseas hacer:
1. Apagar el sistema
2. Reiniciar el sistema
3. Cerrar sesión
Introduce una opción (1-3): 2
Connection to 127.0.0.1 closed by remote host.
vagrant@ubuntu2204:~$ ./configuracion.sh
Elige que deseas hacer:
1. Apagar el sistema
2. Reiniciar el sistema
3. Cerrar sesión
Introduce una opción (1-3): 5
No se puede realizar
```
### - Día de la semana
```bash
#!/bin/bash

read -p "Escribe un número entre 1 y 7: " dia

case $dia in
     1) echo "Lunes" ;;
     2) echo "Martes" ;;
     3) echo "Miércoles" ;;
     4) echo "Jueves" ;;
     5) echo "Viernes" ;;
     6) echo "Sábado" ;;
     7) echo "Domingo" ;;
     *) echo "El número no se encuentra dentro del parámetro solicitado" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./dia-semana.sh
Escribe un número entre 1 y 7: 5
Viernes
vagrant@ubuntu2204:~$ ./dia-semana.sh
Escribe un número entre 1 y 7: 8
El número no se encuentra dentro del parámetro solicitado
vagrant@ubuntu2204:~$ ./dia-semana.sh
Escribe un número entre 1 y 7: 2
Martes
```
### - Clasificación de notas
```bash
#!/bin/bash
read -p "Introduce la nota: " nota
case $nota in
  10|9) echo "Sobresaliente" ;;
  8|7) echo "Notable" ;;
  6|5) echo "Aprobado" ;;
  4|3|2|1|0) echo "Suspenso" ;;
  *) echo "Número no válido" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./clasificacion-notas.sh
Introduce la nota: 5
Aprobado
vagrant@ubuntu2204:~$ ./clasificacion-notas.sh
Introduce la nota: 9
Sobresaliente
```

Como curiosidad decir, que si introducimos una nota con decimales nos dará un Número no valido. Para poder introducir notas con decimales, debemos utilizar el comando if junto con la orden bc -l. 

Por ejemplo:

if (( $(echo "$calificacion >= 9" | bc -l) )); then echo "Sobresaliente".

### - Clasificación de números
```bash
#!/bin/bash
read -p "Escribe un número: " numero
case 1 in
  $(($numero > 0)))
         echo "El número es positivo" ;;
  $(($numero < 0)))
         echo "El número es negativo" ;;
  0) echo "Cero" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./clasificacion-numeros.sh
Escribe un número: 5
El número es positivo
vagrant@ubuntu2204:~$ ./clasificacion-numeros.sh
Escribe un número: -25
El número es negativo
```
### - Control de servicios en Linux
```bash
#!/bin/bash
read -p "Escribe el nombre del servicio: " servicio
echo "Decide la acción del servicio:"
echo "1. Iniciar"
echo "2. Detener"
echo "3. Reiniciar"
read -p "Introduce una opción (1-3): " opcion

case $opcion in
  1) sudo systemctl start $servicio ;;
  2) sudo systemctl stop $servicio ;;
  3) sudo systemctl restart $servicio ;;
  *) echo "Opción no válida" ;;
esac

if [ $? -eq 0 ];
         then
                 echo "La operación se realizó correctamente"
else
                 echo "No se ha podido ejecutar la operación"
fi
```
```bash
vagrant@ubuntu2204:~$ ./control-servicios.sh
Escribe el nombre del servicio: ssh.service
Decide la acción del servicio:
1. Iniciar
2. Detener
3. Reiniciar
Introduce una opción (1-3): 1
La operación se realizó correctamente
vagrant@ubuntu2204:~$ ./control-servicios.sh
Escribe el nombre del servicio: cron.service
Decide la acción del servicio:
1. Iniciar
2. Detener
3. Reiniciar
Introduce una opción (1-3): 3
La operación se realizó correctamente
```



