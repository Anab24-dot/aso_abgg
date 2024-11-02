# PRÁCTICA 0302b
##  COMANDO CASE
### - Menú de operaciones matemáticas
```bash
#!/bin/bash
read -p "Introduce el primer operando: " num1
read -p "Introduce el segundo operando: " num2

echo "Elige una operación:"
echo "1. Suma"
echo "2. Resta"
echo "3. Multiplicación"
echo "4. División"
read -p "Introduce la eleccioón (1-4): " opcion

case $opcion in
    1) echo "Resultado: $(($num1 + $num2))" ;;
    2) echo "Resultado: $(($num1 - $num2))" ;;
    3) echo "Resultado: $(($num1 * $num2))" ;;
    4) 
    if [ $num2 -ne 0 ]; then
        echo "Resultado: $(($num1 / $num2))"
    else
        echo "División por cero no permitida"
    fi
    ;;
    *) echo "Opción invalidada" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./operaciones-matematicas.sh
Introduce el primer operando: 26
Introduce el segundo operando: 13
Elige una operación:
1. Suma
2. Resta
3. Multiplicación
4. División
Introduce la eleccioón (1-4): 4
Resultado: 2
vagrant@ubuntu2204:~$ ./operaciones-matematicas.sh
Introduce el primer operando: 3
Introduce el segundo operando: 6
Elige una operación:
1. Suma
2. Resta
3. Multiplicación
4. División
Introduce la eleccioón (1-4): 3
Resultado: 18
```
### - Verificar días de la semana
```bash
#!/bin/bash
read -p "Escribe un día de la semana: " dia

case $dia in
  lunes|martes|miércoles|jueves|viernes)
         echo "Es un día laboral" ;;
  sábado|domingo)
         echo "Es un día de fin de semana" ;;
         *) echo "Incorrecto" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./dias-semana.sh
Escribe un día de la semana: lunes
Es un día laboral
vagrant@ubuntu2204:~$ ./dias-semana.sh
Escribe un día de la semana: sábado
Es un día de fin de semana
vagrant@ubuntu2204:~$ ./dias-semana.sh
Escribe un día de la semana: Monday
Incorrecto
```
### - Clasificar calificaciones
```bash
#!/bin/bash
read -p "Introduce la calificación (0-10): " nota

case $nota in
  9|10) echo "Sobresaliente" ;;
  7|8) echo "Notable" ;;
  6) echo "Bien" ;;
  5) echo "Suficiente" ;;
  [0-4]) echo "Suspenso" ;;
  *) echo "Nota errónea" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ chmod +x clasificar-calificacion.sh
vagrant@ubuntu2204:~$ ./clasificar-calificacion.sh
Introduce la calificación (0-10): 3
Suspenso
vagrant@ubuntu2204:~$ ./clasificar-calificacion.sh
Introduce la calificación (0-10): 10
Sobresaliente
vagrant@ubuntu2204:~$ ./clasificar-calificacion.sh
Introduce la calificación (0-10): 2
Suspenso
```
### - Determinar la estación del año
```bash
#!/bin/bash
read -p "Escribe el mes: " mes
read -p "Escribe el día (opcional): " dia

case $mes in
  diciembre|enero|febrero) 
    if [[ $mes == "diciembre" && $dia -ge 21 ]] || [[ $mes == "marzo" && $dia -lt 21 ]];
         then
                 echo "La estación es invierno"
    else
                 echo "Es invierno"
    fi ;;
   marzo|abril|mayo) 
    if [[ $mes == "marzo" && $dia -ge 22 ]] || [[ $mes == "junio" && $dia -lt 20 ]];
         then
                 echo "La estación es primavera"
         else
                 echo "Es primavera"
    fi ;;
    junio|julio|agosto) 
    if [[ $mes == "junio" && $dia -ge 21 ]] || [[ $mes == "septiembre" && $dia -lt 20 ]];
         then
                 echo "La estación es verano"
    else
                 echo "Es verano"
   fi ;;
   septiembre|octubre|noviembre) 
    if [[ $mes == "septiembre" && $dia -ge 21 ]] || [[ $mes == "diciembre" && $dia -lt 20 ]];
         then
                 echo "La estación es otoño"
    else
                 echo "Es otoño"
    fi ;;
  *) echo "Mes no existente" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./estacion-año.sh
Escribe el mes: abril                                                                           
Escribe el día (opcional): 20
Es primavera
vagrant@ubuntu2204:~$ ./estacion-año.sh
Escribe el mes: abril
Escribe el día (opcional):
Es primavera
vagrant@ubuntu2204:~$ ./estacion-año.sh
Escribe el mes: septiembre
Escribe el día (opcional): 21
La estación es otoño
vagrant@ubuntu2204:~$ ./estacion-año.sh
Escribe el mes: septiembre
Escribe el día (opcional):
Es otoño
```
### - Identificar el tipo de archivo
```bash
#!/bin/bash
read -p "Introduce la extensión del archivo (no olvidar escribir el punto delante de la extensión): " extension

case $extension in
  .txt) echo "Archivo de texto" ;;
  .jpg|.jpeg|.png|.gif) echo "Archivo de imagen" ;;
  .pdf) echo "Archivo de documento PDF" ;;
  .zip|.tar|.gz) echo "Archivo comprimido" ;;
  *) echo "Archivo desconocido" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./identificar-archivo.sh
Introduce la extensión del archivo (no olvidar escribir el punto delante de la extensión): .jpg
Archivo de imagen
vagrant@ubuntu2204:~$ ./identificar-archivo.sh
Introduce la extensión del archivo (no olvidar escribir el punto delante de la extensión): .jpeg
Archivo de imagen
```
### - Convertir temperaturas
```bash
#!/bin/bash
echo "Elige una conversión :"
echo "1. Celsius a Fahrenheit"
echo "2. Fahrenheit a Celsius"
echo "3. Celsius a Kelvin"
read -p "Introduce una opción (1-3): " opcion
read -p "Escribe  la temperatura: " temp

case $opcion in
  1) echo "Resultado: $(echo "$temp * 1.8 + 32" | bc -l) °F" ;;
  2) echo "Resultado: $(echo "($temp - 32) / 1.8" | bc -l) °C" ;;
  3) echo "Resultado: $(echo "$temp + 273.15" | bc -l) K" ;;
  *) echo "Opción equivocada" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./convertir-temperatura.sh
Elige una conversión :
1. Celsius a Fahrenheit
2. Fahrenheit a Celsius
3. Celsius a Kelvin
Introduce una opción (1-3): 2
Escribe  la temperatura: 25
Resultado: -3.88888888888888888888 °C
vagrant@ubuntu2204:~$ ./convertir-temperatura.sh
Elige una conversión :
1. Celsius a Fahrenheit
2. Fahrenheit a Celsius
3. Celsius a Kelvin
Introduce una opción (1-3): 1
Escribe  la temperatura: -3.8888888888888
Resultado: 25.00000000000016 °F
```
### - Estado del servicio
```bash
#!/bin/bash
read -p "Escribe el nombre del servicio: " servicio
echo "Seleccionar la opción para el servicio:"
echo "1. Iniciar"
echo "2. Detener"
echo "3. Reiniciar"
read -p "Introduce una opción (1-3): " opcion

case $opcion in
  1) sudo systemctl start $servicio ;;
  2) sudo systemctl stop $servicio ;;
  3) sudo systemctl restart $servicio ;;
  *) echo "Opción equivocada" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./estado-servicio.sh
Escribe el nombre del servicio: mysql
Seleccionar la opción para el servicio:
1. Iniciar
2. Detener
3. Reiniciar
Introduce una opción (1-3): 1
Failed to start mysql.service: Unit mysql.service not found.
vagrant@ubuntu2204:~$ ./estado-servicio.sh
Escribe el nombre del servicio: user@1000.service
Seleccionar la opción para el servicio:
1. Iniciar
2. Detener
3. Reiniciar
Introduce una opción (1-3): 1
```
### - Conversión de unidades de longitud
```bash
#!/bin/bash
echo "Elige una conversión:"
echo "1. Metros a kilómetros"
echo "2. Metros a centímetros"
echo "3. Metros a milímetros"
read -p "Introduce una opción (1-3): " opcion
read -p "Introduce el número de  metros: " metros

case $opcion in
  1) echo "Resultado: $(echo "$metros / 1000" | bc -l) km" ;;
  2) echo "Resultado: $(echo "$metros * 100" | bc -l) cm" ;;
  3) echo "Resultado: $(echo "$metros * 1000" | bc -l) mm" ;;
  *) echo "Opción errónea" ;;
esac
```
```bash
vagrant@ubuntu2204:~$ ./conversion-longitud.sh
Elige una conversión:
1. Metros a kilómetros
2. Metros a centímetros
3. Metros a milímetros
Introduce una opción (1-3): 2
Introduce el número de  metros: 50
Resultado: 5000 cm
vagrant@ubuntu2204:~$ ./conversion-longitud.sh
Elige una conversión:
1. Metros a kilómetros
2. Metros a centímetros
3. Metros a milímetros
Introduce una opción (1-3): 3
Introduce el número de  metros: 50
Resultado: 50000 mm
```






