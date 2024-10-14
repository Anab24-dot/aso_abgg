Una vez que nos encontremos en la carpeta donde realizaremos la práctica, abrimos en el buscador vagrantbox para buscar el sistema operativo requerido. Añadimos la dirección con vagrant box add <dirección del sistema operativo>, una vez instalado iniciamos vagrant con el objetivo de crear el archivo correspondiente.
Ahora nos movemos en el vagrantfile para hacer los cambios oportunos.
```ruby
Vagrant.configure("2") do |config|
  config.vm.define "win2019" do |w19|
  w19.vm.box = "StefanScherer/windows_2019"
  w19.vm.provider "virtualbox" do |vb|
    vb.memory=4192
    vb.cpus=4
  w19.vm.network "private.network", ip:"172.19.0.2"  
end
```
Incorporamos en el archivo la configuración de la segunda máquina correspondiente a Windows 10 para que al levantar la máquina, directamente se inicien las dos máquinas
