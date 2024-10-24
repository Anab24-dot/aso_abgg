REDES EN VAGRANT
Creamos un Vagranfile para la creación de una máquina 
con unas características dadas.
```bash
Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2204"
  config.vm.hostname="ubuntuserver"
  config.vm.network "public_network",ip:"10.99.0.1"
  config.vm.network "private_network",ip:"172.16.0.1"
  config.vm.provision "shell", inline:"apt update && apt install apache 2 -y"
  config.vm.provider "virtualbox" do |vb|
    vb.name="web server"
    vb.cpus=2
    vb.memory=3072
  end
end
```
Iniciamos 
