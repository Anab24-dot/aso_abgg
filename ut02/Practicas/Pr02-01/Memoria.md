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

```
ls


