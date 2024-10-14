La máquina ya estaba creada en un ejercicio anterior. Por lo tanto, abrimos una nueva carpeta Pr0203 e iniciamos vagrant para crear un archivo.
```bash
PS C:\GIT\aso_abgg\ut02\Practicas\Pr0203> vagrant init generic/ubuntu2204
```
Nos dirigimos a Virtualbox y con la máquina apagada añadimos un nuevo adaptador: "Adaptador puente"
Arrancar la máquina desde Virtualbox y una vez que está, nos pide contraseña. En este momento escribir vagrant ssh en el terminal para tomar el control.
Para configurar el adaptador puente y darle una ip(tiene que estar en el rango de ip privadas), aplicamos la configuración y comprobar que está creado y hacer un ping con el resto de pc conectados en la red
```bash
vagrant@ubuntu2204:~$ sudo nano /etc/netplan/00-installer-config.yaml      
vagrant@ubuntu2204:~$ sudo netplan apply
vagrant@ubuntu2204:~$ ping 172.18.0.1
```
Ahora crear un usuario para cada uno de los componentes de la red con el comando Adduser
```bash
vagrant@ubuntu2204:/etc/netplan$ sudo adduser ernesto
vagrant@ubuntu2204:/etc/netplan$ sudo adduser alvaro
vagrant@ubuntu2204:/etc/netplan$  sudo adduser raul
```
Crear claves públicas y privadas. Lo primero es tener cuidado con el usuario desde el que estamos conectados. Puedo crear mi propio usuario (sería lo mas apropiado) con ese usuario conectado se generan las claves (poner 1024). Una vez que las tenemos hay que enviar la clave al resto de equipos con "scp"y lo guardo en authorized keys.
También las puedo poner disponibles en mi máquina, creando un directorio personal y ejecutar la orden: python3 -m http.server; y guardo aquí la clave pública. 
Creamos el usuario ana
```bash
vagrant@ubuntu2204:/etc$ sudo adduser ana
```
Me conecto con mi usuario "ana"
```bash
vagrant@ubuntu2204:/etc$ su ana
```
Para generar la clave utilizamos el comando
```bash
ana@ubuntu2204:/$ ssh-keygen -t rsa -b 1024
```
El resultado se muestra:
```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ana/.ssh/id_rsa): 
Created directory '/home/ana/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ana/.ssh/id_rsa
Your public key has been saved in /home/ana/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:MJY1Uyli6WeepE5VuEd0uUoT5LoWULIGlUL3OPDxr50 ana@ubuntu2204.localdomain
The key's randomart image is:
+---[RSA 1024]----+
|   .+.=o==+...   |
|    .==@o+=..    |
|     +%.o=.. .   |
|     o.=*o+ .    |
|       BS+.o     |
|      o o=..     |
|     o  + E      |
|      ..         |
|                 |
+----[SHA256]-----+
```
Para enviar la clave pública a otra máquina, desde MI usuario escribir el siguiente comando:
```bash
ana@ubuntu2204:/$ scp /home/ana/.ssh/id_rsa.pub ana@172.18.0.3:/home/ana
En la segunda parte de la sentencia el nombre de usuario coincide con MI usuario, pero vemos que la ip es diferente (coincidente con la máquina de Ernesto).
ana@172.18.0.3's password: 
id_rsa.pub                                           100%  240    82.2KB/s   00:00  
```
```bash
ana@ubuntu2204:~$ ls
id_rsa.pub
ana@ubuntu2204:~$ mkdir .ssh
ana@ubuntu2204:~$ mv id_rsa.pub .ssh/authorized_keys
ana@ubuntu2204:~$ cd .ssh
ana@ubuntu2204:~/.ssh$ ls -l
total 4
-rw-r--r-- 1 ana ana 240 Oct 14 11:40 authorized_keys
```
Lo siguiente es salir e ingresar de nuevo en MI usuario para al conectarme de nuevo desde otro ordenador no se me pida la contraseña.
```bash
ana@ubuntu2204:/etc$ ssh ana@172.18.0.3
Last login: Mon Oct 14 11:44:36 2024 from 172.18.0.2
```
