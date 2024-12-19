# Configuración de la red
# Configurar el segundo adaptador de la máquina cuyo identificador es enp0s8 para que pertenezca a la red de clase B 172.21.0.0. Esto te debería permitir ver el servidor de recursos.
## Vagrant box list
## Vagrant init generic/ubuntu2204
## vagrant up
## vagrant ssh
## Primero listamos las interfaces de red disponibles para confirmar que existe enp0s8 con el comamdo IP A, en mi casa voy a cambiarlo por eth0
## Configuramos enp0sj8 con una IP en la red 172.21.0.0/16. Podemos asignar IPs desde 172.21.0.1 hasta 172.21.255.254. Asignamos una válida, por ejemplo 172.21.0.10 al adaptador enp0s8
```bash
sudo ip addr add 172.21.0.10/16 dev enpos8
```
### Si la interfaz enp0s8 está desactivada la levantamos con: 
```bash
sudo ip link set enp0s8 up
```
## Verificamos que se haya asignado bien la IP con 
```bash
ip a | grep enp0s8
Deberiamos ver algo como:
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 ...
    inet 172.21.0.10/16 brd 172.21.255.255 scope global enp0s8
```
## Hacemos ping a la red 172.21.200.255
## Para hacer permanentes los cambios de las ip y que no desaparezcan al reinicio: 
```bash
sudo nano /etc/netplan/01-netcfg.yaml
network:
  version: 2
  ethernets:
    enp0s8:
      dhcp4: no
      addresses:
        - 172.21.0.10/16
sudo netplan apply (guardamos y aplicamos los cambios)
ip a show enp0s8 (para ver que se ha configurado correctdamente)
```
## Configuración manual universal sería
```bash
sudo nano /etc/network/interfacces
auto enp0s8
iface enp0s8 inet static
    address 172.21.0.10
    netmask 255.255.0.0
    network 172.21.0.0
    broadcast 172.21.255.255
sudo systemctl restart networking (guardar y reiniciar la red)
ip a show enp0s8 (comprobar la configuración)
También podemos añadir la ip en el vagrantfile como en la práctica 0202
```
# Ejercicio 2. Conexión SSH para el profesor
## Crear un usuario llamado profesor con clave paso
```bash
sudo useradd -m profesor
sudo passwd profesor
# Introduce 'paso' como contraseña
```
```bash
pero lo haremos mejor con el comando
sudo adduser profesor
y nos pedirá la contraseña que introducimos
```
## Configurar las claves públicas SSH
```bash
accedemos a la  carpeta del usuario profesor
sudo -u profesor mkdir /home/profesor/.ssh
sudo -u profesor chmod 700 /home/profesor/.ssh
ahora copiamos la clave pública al archivo authorized keys
sudo cp /path/to/id_rsa.pub /home/profesor/.ssh/authorized_keys
sudo chown profesor:profesor /home/profesor/.ssh/authorized_keys
sudo chmod 600 /home/profesor/.ssh/authorized_keys
```
## Prohibir la conexión por contraseña:
```bash
editar el archivo de configuración de ssh
sudo nano /etc/ssh/sshd_config
modifica o añade
PasswordAuthentication no
reiniciar el servicio
sudo systemctl restart ssh
```
# Ejercicio 3. Carpeta colaborativa
```bash
Utilizamos el comando ls -ld /docs para comprobar si la carpeta existe. 
Si existe mostrará información como permisos, dueño y grupo. En el caso de que no exista mostrará un mensaje de error
creamos la carpeta con:
sudo mkdir /docs
Vamos a configurar los permisos de la carpeta, que deben permitir que los tres usuarios puedan trabajar en ella, lo mejor es hacerlo mediante un grupo común.
Creamos un grupo para los tres usuarios si no existe
sudo groupadd colaborativo
Añadimos los usuarios al grupo
sudo usermod -aG colaborativo itorvals, bgates, sjobs (en el caso de que no se puedan hacer en un solo comando, hacerlo de tres veces)
Asignar el grupo colaborativo a la carpeta /docs:
sudo chown root: colaborativo /docs
Configuramos los permisos para que el grupo pueda leer, escribir y ejecutar:
sudo chmod 770 /docs (de esta forma el dueño tiene todos los permisos y el grupo también pero los otros no).
Activamos el bit SGID en la carpeta para que los archivos creados dentro hereden el grupo colaborativo:
sudo chmod g+s /docs
```
```bash
Vamos a hacer comprobaciones:
ls -ld /docs (deberíamos ver algo como: drwxrws--- 2 root colaborativo 4096 fecha /docs)
```
# Ejercicio 4. Programación de tareas con cron. 
```bash
Creamos un script llamado backup_logs.sh en la ubicación /usr/local/bin/ (se requieren permisos de superusuario)
#!/bin/bash

# Directorio donde se guardará el backup
BACKUP_DIR="/backup"

# Fecha actual en formato AAAAMMDD
FECHA=$(date +"%Y%m%d")

# Ruta completa del subdirectorio de backup
subdirectorio="${BACKUP_DIR}/${FECHA}"

# Verificar si el directorio /backup existe; si no, crearlo
if [ ! -d "$BACKUP_DIR" ]; then
    mkdir -p "$BACKUP_DIR"
fi

# Crear el subdirectorio con la fecha actual
mkdir -p "$subdirectorio"

# Copiar todos los ficheros y subdirectorios de /var/log al destino
cp -r /var/log/* "$subdirectorio"

# Mensaje de confirmación
echo "Backup completado en ${subdirectorio}"
```
```bash
Creado el script tenemos que darle permisos de ejecución
sudo chmod +x /usr/local/bin/backup_logs.sh
Para programar la tarea en cron abrimos el fichero crontab del usuario root
sudo crontab -e
0 0 */15 9-6 * /usr/local/bin/backup_logs.sh
Para comprobar que el crontab se ha añadido correctamente:
sudo crontab -l
Ejecutamos el script para verificar el funcionamiento:
sudo /usr/local/bin/backup_logs.sh
Comprobamos el contenido de /backup para confirmar que el directorio se creo con la fecha:
ls -l /backup/$(date +"%Y%m%d")
``` 
# BASH SCRIPTING
#!/bin/bash

while true; do
  echo "### Menú de Gestión de Usuarios ###"
  echo "1. Mostrar un listado de usuarios"
  echo "2. Agregar un usuario"
  echo "3. Eliminar un usuario"
  echo "4. Miembros de un grupo"
  echo "5. Creación de usuarios en bloque"
  echo "6. Salir"
  read -p "Elige una opción: " opcion

  case $opcion in
    1)
      echo "Listado de usuarios:"
      cut -d: -f1 /etc/passwd
      ;;
    2)
      read -p "Nombre del usuario: " usuario
      read -p "Contraseña: " pass
      sudo useradd -m $usuario
      echo $usuario:$pass | sudo chpasswd
      echo "Usuario $usuario creado."
      ;;
    3)
      read -p "Nombre del usuario a eliminar: " usuario
      sudo userdel -r $usuario && echo "Usuario $usuario eliminado."
      ;;
    4)
      read -p "Nombre del grupo: " grupo
      if grep -q "^$grupo:" /etc/group; then
        echo "Miembros del grupo $grupo:"
        getent group $grupo | awk -F: '{print $4}'
      else
        echo "El grupo no existe."
      fi
      ;;
    5)
      read -p "Ruta del fichero de usuarios: " fichero
      if [ -f "$fichero" ]; then
        while IFS= read -r usuario; do
          sudo useradd -m $usuario
          echo "Usuario $usuario creado."
        done < $fichero
      else
        echo "El fichero no existe."
      fi
      ;;
    6)
      echo "Saliendo del programa."
      break
      ;;
    *)
      echo "Opción no válida. Intenta de nuevo."
      ;;
  esac
done
```bash
Ahora el ejemplo corto desde Copilot:
#!/bin/bash

# Función para añadir un usuario
añadir_usuario() {
    echo "Introduce el nombre del nuevo usuario:"
    read nombre_usuario
    sudo adduser "$nombre_usuario"
}

# Función para eliminar un usuario
eliminar_usuario() {
    echo "Introduce el nombre del usuario a eliminar:"
    read nombre_usuario
    sudo deluser "$nombre_usuario"
}

# Función para cambiar la contraseña de un usuario
cambiar_contraseña() {
    echo "Introduce el nombre del usuario:"
    read nombre_usuario
    sudo passwd "$nombre_usuario"
}

# Función para añadir un usuario a un grupo
añadir_a_grupo() {
    echo "Introduce el nombre del usuario:"
    read nombre_usuario
    echo "Introduce el nombre del grupo:"
    read nombre_grupo
    sudo usermod -aG "$nombre_grupo" "$nombre_usuario"
}

# Función para mostrar la información de un usuario
mostrar_info_usuario() {
    echo "Introduce el nombre del usuario:"
    read nombre_usuario
    id "$nombre_usuario"
}

# Función para mostrar el menú
mostrar_menu() {
    echo "Selecciona una opción:"
    echo "1. Añadir usuario"
    echo "2. Eliminar usuario"
    echo "3. Cambiar contraseña de usuario"
    echo "4. Añadir usuario a un grupo"
    echo "5. Mostrar información de usuario"
    echo "6. Salir"
}

# Bucle principal
while true; do
    mostrar_menu
    read opcion
    case $opcion in
        1)
            añadir_usuario
            ;;
        2)
            eliminar_usuario
            ;;
        3)
            cambiar_contraseña
            ;;
        4)
            añadir_a_grupo
            ;;
        5)
            mostrar_info_usuario
            ;;
        6)
            echo "Saliendo del programa..."
            break
            ;;
        *)
            echo "Opción no válida. Por favor, selecciona una opción del 1 al 6."
            ;;
    esac
done
chmod +x gestion_usuarios.sh
./gestion_usuarios.sh
```