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
NOTACIÓN OCTAL Y SIMBÓLICA
-


