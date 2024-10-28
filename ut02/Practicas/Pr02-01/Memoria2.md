Abrimos una máquina(Ubuntu Server 22.04 LTS) en VirtualBox con Vagrant, una vez que se ha iniciado escribimos "vagrant ssh" para tener acceso a la línea de comandos de la máquina virtual.
Para crear el directorio usamos el comando "mkdir"
```bash
PS C:\GIT\aso_abgg\ut02\Practicas\Pr02-01> vagrant ssh
vagrant@ubuntu2204:~$ mkdir pr0201
vagrant@ubuntu2204:~$ cd pr0201
vagrant@ubuntu2204:~/pr0201$ mkdir dir1 dir2
vagrant@ubuntu2204:~/pr0201$ 
```
Los permisos del dir1:
- el propietario tiene permiso de lectura, escritura y ejecución (al ser un directorio es permiso de acceso a él)
- el grupo tiene permisos de lectura, escritura y ejecución (acceso)
- los otros (el resto) tiene permisos de lectura y ejecución (acceso)
Para quitar los permisos de escritura utilizamos el comando chmod
```bash
vagrant@ubuntu2204:~/pr0201$ chmod a-w dir2
vagrant@ubuntu2204:~/pr0201$ ls -l
total 8
drwxrwxr-x 2 vagrant vagrant 4096 Oct  1 07:11 dir1
dr-xr-xr-x 2 vagrant vagrant 4096 Oct  1 07:11 dir
```
Para eliminar permisos de lectura en el resto de usuarios en modo octal usamos este tipo de notación, el número resultante sería 551
```bash

vagrant@ubuntu2204:~/pr0201$ ls -l
total 8
drwxrwxr-x 2 vagrant vagrant 4096 Oct  1 07:11 dir1
dr-xr-x--x 2 vagrant vagrant 4096 Oct  1 07:11 dir2
```
En estos momentos los permisos del directorio dir2 son:
- lectura y ejecución para el propietario y para el grupo
- ejecución solamente para el resto
Es imposible crear el directorio dir21 dentro de dir2, ya que no tenemos permiso de escritura
```bash
vagrant@ubuntu2204:~/pr0201/dir2$ mkdir dir21
mkdir: cannot create directory ‘dir21’: Permission denied
```
En notación octal creo permiso de escritura para el propietario
```bash
vagrant@ubuntu2204:~/pr0201$ chmod 751 dir2
vagrant@ubuntu2204:~/pr0201$ ls -l
total 8
drwxrwxr-x 2 vagrant vagrant 4096 Oct  1 07:11 dir1
drwxr-x--x 2 vagrant vagrant 4096 Oct  1 07:11 dir2
vagrant@ubuntu2204:~/pr0201$ cd dir2
vagrant@ubuntu2204:~/pr0201/dir2$ mkdir dir21
```
Comprobación positiva de la creación del directorio
```bash
vagrant@ubuntu2204:~/pr0201$ cd dir2
vagrant@ubuntu2204:~/pr0201/dir2$ ls -l
total 4
drwxrwxr-x 2 vagrant vagrant 4096 Oct  1 07:44 dir21
vagrant@ubuntu2204:~/pr0201/dir2$ 
```
<<<<<<< HEAD
NOTACIÓN OCTAL Y SIMBÓLICA: Partimos desde los permisos rw-r--r--
-rwxrwxr-x : a+x,g+w
rwxr--r-- : u+x
r--r----- : u-w,o-r
rwxr-xr-x : a+x
rwxr-xr-x : a+x
r-x--x--x : u-w,go-r,a+x
-w-r----x : uo-r,o+x
-----xrwx : ug-r,u-w,o+w,go+x
r---w---x : go-r,u-w,g+w,o+x
-w------- : a-r
rw-r----- : o-r
rwx--x--x : a+x,go-r

rwxrwxrwx : 777
--x--x--x : 111
r---w---x : 421
-w------- : 200
rw-r----- : 640
rwx--x--x : 711
rwxr-xr-x : 755
r-x--x--x : 511
-w-r----x : 241
-----xrwx : 017

Ejercicio 3. El bit setgid
Con la máquina levantada y en su shell creamos el grupo y los usuarios.
```bash
vagrant@ubuntu2204:~$ sudo groupadd asir
vagrant@ubuntu2204:~$ sudo useradd  -g asir agg1
vagrant@ubuntu2204:~$ sudo useradd  -g asir agg2
```
Creamos el directorio y le asignamos propietario
```bash
vagrant@ubuntu2204:/$ mkdir compartido
mkdir: cannot create directory ‘compartido’: Permission denied
vagrant@ubuntu2204:/$ sudo mkdir compartido
vagrant@ubuntu2204:/$ sudo chown root:asir /compartido
```
Comprobaciones:
```bash
drwxr-xr-x   2 root asir       4096 Oct  3 08:24 compartido
```
Asignamos permisos al usuario y al grupo propietario:
```bash
vagrant@ubuntu2204:/$ sudo chmod 770 /compartido
vagrant@ubuntu2204:/$ sudo ls -ld /compartido
drwxrwx--- 2 root asir 4096 Oct  3 08:24 /compartido
```
Establecemos el bit SetGid en el directorio
```bash
vagrant@ubuntu2204:/$ sudo chmod g+s /compartido
vagrant@ubuntu2204:/$ sudo ls -ld /compartido
drwxrws--- 2 root asir 4096 Oct  3 08:24 /compartido
```
Iniciamos sesión con el usuario agg1, accedemos al directorio y creamos el fichero1. Comprobamos los permisos. Como hemos creado los usuarios con useradd no hemos asignado contraseñas, por lo que hemos de hacerlo antes de iniciar sesión.
Para el usuario agg1 la contraseña es 1234
Para el usuario agg2 la contraseña es abcd
```bash
$ cd /compartido
$ pwd
/compartido
$
```
Al cambiar de usuario y movernos hasta el directorio compartido, tenemos el problema de no ver claramente el usuario y el directorio; el comando pwd nos ayuda a ver en que directorio nos encontramos
```bash
$ echo "Creamos un fichero para el usuario 1" > fichero1
$ ls -l fichero1
-rw-r--r-- 1 agg1 asir 37 Oct 27 17:07 fichero1
```
El archivo sí tiene como grupo propietario asir, esto es debido al bit setgid en el directorio
Cambiamos ahora de usuario para comprobar si podemos ver el fichero1 creado en el usuario anterior.
```bash
$ su agg2
Password: 
$ cd /compartido
$ ls -l
total 4
-rw-r--r-- 1 agg1 asir 37 Oct 27 17:07 fichero1
```
Añadimos contenido al fichero1, pero en este caso no se me permite porque no tengo permiso
PREGUNTAS:
- ¿Qué ventajas tiene usar el bit setgid en entornos colaborativos?: da la oportunidad de que todos los miembros de un grupo puedan tener acceso a los archivos y ficheros de otros usuarios del mismo grupo sin tener que dar más permisos
- ¿Qué sucede si no se aplica el bit setgid en entornos colaborativos?: será necesario dar permisos cada poco, y habría limitaciones en el acceso y los cambios en los archivos por parte de otros usuarios del mismo grupo
Para la eliminación de los usuarios, grupo y el directorio he tenido problemas, 
no era posible eliminarlos. Después de varios intentos infructuosos reinicié la máquina y sí se habían eliminado los usuarios. Por tanto he  eliminado el resto
```bash 
vagrant@ubuntu2204:~$ sudo userdel -r agg1
userdel: agg1 mail spool (/var/mail/agg1) not found
userdel: agg1 home directory (/home/agg1) not found
vagrant@ubuntu2204:~$ sudo userdel -r agg2
userdel: agg2 mail spool (/var/mail/agg2) not found
userdel: agg2 home directory (/home/agg2) not found
vagrant@ubuntu2204:~$ sudo groupdel asir
vagrant@ubuntu2204:~$ sudo rm -rf /compartido
vagrant@ubuntu2204:~$ cat /etc/passwd
```
4. EL STICKY BIT
```bash
vagrant@ubuntu2204:~$ sudo mkdir /compartido
vagrant@ubuntu2204:~$ sudo chmod 777 /compartido
vagrant@ubuntu2204:~$ sudo adduser agg1
Adding user `agg1' ...
Adding new group `agg1' (1001) ...
Adding new user `agg1' (1001) with group `agg1' ...
Creating home directory `/home/agg1' ...
Copying files from `/etc/skel' ...
Is the information correct? [Y/n] y
vagrant@ubuntu2204:~$ sudo adduser agg2
Adding user `agg2' ...
Adding new group `agg2' (1002) ...
Adding new user `agg2' (1002) with group `agg2' ...
Creating home directory `/home/agg2' ...
Copying files from `/etc/skel' ...
```
En este caso creamos los usuarios con el comando adduser y vemos como resulta mas sencillo para ver en el usuario desde el que trabajamos.
```bash
vagrant@ubuntu2204:~$ su - agg1
Password: 
agg1@ubuntu2204:~$ cd /compartido
agg1@ubuntu2204:/compartido$ touch fichero1
agg1@ubuntu2204:/compartido$ echo "Que bien resulta ahora ver todo mas claro" > fichero1
agg1@ubuntu2204:/compartido$ su - agg2
Password: 
agg2@ubuntu2204:~$ rm /compartido/fichero1
rm: remove write-protected regular file '/compartido/fichero1'? y
agg2@ubuntu2204:~$
agg2@ubuntu2204:~$ ls -l
total 0
agg2@ubuntu2204:~$ ls /compartido
agg2@ubuntu2204:~$ find /compartido -name "fichero1"
agg2@ubuntu2204:~$ su - agg1
Password: 
agg1@ubuntu2204:~$ ls -l
total 0
agg1@ubuntu2204:~$
```
Vemos como el segundo usuario ha podido eliminar el fichero1, ya que todos los 
usuarios del grupo tienen todos los permisos dentro de ese directorio.
```bash
vagrant@ubuntu2204:~$ sudo chmod +t /compartido
vagrant@ubuntu2204:~$ ls -ld /compartido
drwxrwxrwt 2 root root 4096 Oct 27  2024 /compartido
```
Vemos como se ha activado el Sticky bit, porque en los permisos del directorio
se ha añadido la letra t que indica que el bit está habilitado
```bash
vagrant@ubuntu2204:~$ su - agg1
Password:
agg1@ubuntu2204:~$ cd /compartido
agg1@ubuntu2204:/compartido$ touch fichero2
agg1@ubuntu2204:/compartido$ echo "Vamos a comprobar ahora su funcionamiento" > fichero2

agg1@ubuntu2204:/compartido$ su - agg2
Password:
agg2@ubuntu2204:~$ rm /compartido/fichero2
rm: remove write-protected regular file '/compartido/fichero2'? y
rm: cannot remove '/compartido/fichero2': Operation not permitted
```
Vemos ahora como cambiando el usuario "no" es posible la eliminación del fichero2
PREGUNTAS:
- ¿Qué efecto tiene el sticky bit en un directorio?: Se utiliza para evitar que usuarios con directorios compartidos puedan eliminar o renombrar archivos si no son propietarios de ellos o por supuesto el administrador
- Si tienes habilitado el sticky bit, ¿cómo tendrías que hacer para eliminar un fichero dentro de un directorio?: siendo el administrador o el propietario del archivo
FICHERO /ETC/SHADOW
Creamos un usuario con adduser y mostramos la línea del fichero /etc/shadow donde podemos ver el hash del usuario creado
```bash
vagrant@ubuntu2204:~$ sudo adduser agg
vagrant@ubuntu2204:~$ sudo grep agg /etc/shadow
agg:$y$j9T$f6b1X7kva2f5wTwVE3agQ.$Lz8F8wLNKiVSOJkIJYdXolZUreXkdxf/lIDU85fv7qC:20024:0:99999:7:::
```
¿Cuáles son los tipos de hash soportados por el fichero /etc/shadow?:
- MD5: usa $1$ al principio
- Blowfish: usa $2a$
- Eksblowfish: $2y$
- SHA-256: $5$
- SHA-512: $6$
¿Cuál es el tipo de hash usado en este sistema?: Revisando las respuestas de la cuestión anterior, podemos decir que es un Eksblowfish (aunque no tengamos el número 2), consultando en internet es un hash generado por un algoritmo bcrypt, el cual está diseñado para hacer más resistente el sistema a los ataques de fuerza bruta.
¿Para que sirve el campo sal?: una sal de contraseña es un bit aleatorio de datos que se añade a la contraseña antes de pasarla por el algoritmo hash. Es diferente para cada usuario. Previene ataques de diccionario y tablas rainbow haciendo que para una misma contraseña se generen diferentes hashes.
¿Qué son los ataques de diccionario y tablas rainbow?: Un ataque de diccionario es un método para intentar acceder a un sistema o un dispositivo protegidos por contraseña que consiste en ir probando combinaciones de palabras hasta dar con la contraseña correcta.
Las tablas rainbow, son tablas que contienen hashes de contraseñas más o menos comunes y sus valores de texto plano. Esto facilita a un atacante buscar de forma fácil y rápida un hash y encontrar su contraseña original. Es como la gúía telefónica antigua pero con contraseñas y hashes.
Para ver el hash de la contraseña asir2:
```bash 
vagrant@ubuntu2204:~$ echo -n asir2 |sudo sha512sum
e5f11255a95fef13990981b3bdcce42671243f34e3aa88560027092715219dbed0b80e8639f91b71eea4d420a1dff683c1e5f613136241da2cd31d1e5fdc501a  -
```


