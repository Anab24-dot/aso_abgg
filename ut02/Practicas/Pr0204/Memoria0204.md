# Práctica PR0204

## Programación de tareas con `cron


### Órdenes de contrab según los casos
   
La tarea se ejecuta cada hora: 0**** 

Los domingos cada 3 horas: 0*/3**0

A las 12 de la mañana los días pares del mes: 0 12 */2 **

El primer día de cada mes a las 8:00 y las 20:00: 0 8,20 1 **

Cada media hora de lunes a viernes: */30 ***1-5

Cada cuarto de hora, entre las 3 y las 8 de lunes a viernes, 
durante todo el mes de agosto: */15 3-8 * 8 1-5

Cada 90 minutos: 30 */1 ***

### Como se comprueba si el servicio se está ejecutando

"ps aux | grep cron | grep -v grep"

ps lista todos los procesos del sistema; -a muestra todos los procesos; 
-u muestra a los propietarios; -x muestra los procesos que no tienen un terminal controlado
grep se usa para buscar un patrón (palabra) y poder filtrar información.

También podemos usar el comando: "pgrep cron" para mostrar el ID de los procesos
cron que estén en ejecución.

```bash
vagrant@ubuntu2204:~$ ps aux | grep cron | grep -v grep
root         832  0.0  0.1   6892  3064 ?        Ss   07:51   0:00 /usr/sbin/cron -f -P
```
### ¿Cuál es el efecto de la siguiente línea crontab?:   */15 1,2,3 * * * who > /tmp/test

*/15= la tarea se ejecuta cada 15 minutos

1,2,3= la tarea se ejecuta a la 1,2 y 3 de la madrugada

***= todos las días del mes, todos los meses y todos los días de la semana

who= muestra quien está conectado  al archivo /tmp/test.

Por tanto, cada 15 minutos entre la 1 y las 3 de la mañana el archivo /tmp/test
se actualiza con las personas conectadas en ese momento

### Indicar la ruta del fichero crontab del sistema:

Ruta del fichero contrab del sistema: /etc/contrab
```bash
vagrant@ubuntu2204:~$ cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'       
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,   
# that none of the other crontabs do.
```
```bash
vagrant@ubuntu2204:~$ ls /etc/crontab
/etc/crontab
```
### ¿Qué ficheros controlan los usuarios que pueden utilizar el "crontab"?

Ficheros controlados por los usuarios que pueden usar el contrab: el 
fichero es: "cron.allow", sólo los usuarios que se encuentran en él pueden crear,
editar, mostrar o eliminar Ficheros contrab
```bash
vagrant@ubuntu2204:~$ cat /etc/cron.allow
cat: /etc/cron.allow: No such file or directory
vagrant@ubuntu2204:~$ cat /etc/cron.deny
cat: /etc/cron.deny: No such file or directory
```
### Excepcionalmente se debe iniciar una tarea llamada script.sh todos los lunes a las 07:30h antes de entrar en clase ¿Cómo lo harías?

Script.sh todos los lunes a las 07:30:  30 7 ** 1 /bin/
ejecutar/script.sh
1. Listar y cancelar tarea:  con el comando "ps" podemos ver
los procesos del sistema. Para suprimir el proceso usaremos el 
comando "kill -9 pid"con esta orden se "mata" o suprime el proceso
el 9 es el número de SIGKILL para matar el proceso y el pid
es el identificador del proceso
1. Ejecución comando ps -ef para root:  2**** root /tmp/ps_result
2. Verificar la lista de tareas en contrab: tenemos dos comandos
dependiendo de que usuario seamos:
para un usuario normal:  contrab -l
para el administrador: contrab -u (usuario) -l, de esta forma veremos
las tareas de cualquier usuario
1.  