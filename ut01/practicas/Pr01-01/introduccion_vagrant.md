# INTRODUCCIÓN A VAGRANT

## Objetivos:

Preparar un proyecto Vagrant que permita levantar una máquina virtual con una serie de características

## Realización:

Descargamos un sistema operativo Ubuntu Server 20.04  de Vagrant Boxes, recurso dado en el módulo. Simplemente debemos escribir en la casilla de búsqueda el nombre del sistema operativo y luego descargarlo
Una vez que seleccionamos el sistema operativo, podemos ver como en la parte derecha de la pantalla tenemos unas instrucciones de como usar “la caja” con Vagrant.

En nuestra terminal escribimos  vagrant box add (control + v) para copiar el nombre de la imagen en este caso se corresponde con el nombre (gusztavvargadr/ubuntu-server-2004-lts)

Comprobamos que tenemos el sistema operativo e inicializamos, de esta forma creamos un Vagrantfile,  desde donde podemos realizar modificaciones.

Para cambiar el nombre de la máquina, debemos abrir el Vagrantfile y desde aquí, y debajo de la línea Vagrant.configure("2") do |config|.
```bash
Vagrant.configure("2") do |config|
 
  config.vm.box = "gusztavvargadr/ubuntu-server-2004-lts"
  config.vm.hostname = "server-abgg"
  config.vm.provider "virtualbox" do |vb|
    vb.name = "ubuntu server"
    vb.memory = 2048
    vb.cpus = 2
  config.vm.synced_folder ".compartida/",
   "/data", create:true
  end
  
  
end
```
Lo siguiente que debemos hacer es levantar la máquina con el comando “vagrant up”, de esta forma la máquina se inicia en VirtualBox con los datos dados.

Para realizar la última parte (Tendrá el directorio /data de la máquina virtual sincronizado con una carpeta que crearás en el directorio donde está el Vagrantfile), primero creamos una carpeta en el directorio del ordenador donde está el Vagrantfile, como se muestra en la imagen anterior.

Ejecutamos con la orden: vagrant up. 
```bash
PS C:\GIT\aso_abgg\ut01\practicas\Pr01-01> vagrant ssh
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-169-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
 ```
Entramos en la máquina virtual con: vagrant ssh
```bash
vagrant@server-abgg:~$ 
```

## Recursos adicionales

[**Fichero Vagrantfile**](./Vagrantfile)