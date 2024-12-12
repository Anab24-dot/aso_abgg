# ADMINISTRACIÓN REMOTA DEL SERVIDOR
## Práctica 0404

### 1. Entorno Virtualizado: Se necesita la siguiente configuración de máquinas virtuales:
### - Windows Server 2019 con experiencia de escritorio
### - Windows Server 2016 en modo Core, que tendrá dos adaptadores de red, uno en modo NAT y otro en modo solo-anfitrión
![alt text](image-1.png)
### Vamos a aprovechar la misma red que preparamos el otro día (172.25.0.0/16) para añadir el nuevo equipo a la misma a través de su adaptador en modo solo-anfitrión.
![alt text](image-3.png)
![alt text](image-4.png)
### 2. Preparación de las máquinas
### - Añade el nuevo equipo a la red, comprueba que tiene visibilidad con los tres equipos que ya tienes en ella (las dos máquinas virtuales y el equipo anfitrión)
### - Asigna nombres a los equipo, estos nombres serán:
### Windows Server 2019 con entorno gráfico: {INICIALES}-2019
### Windows Server 2019 en modo core: {INICIALES}-CORE-2019
### Windows Server 2016 en modo core: {INICIALES}-CORE-2016
![alt text](image-2.png)
![alt text](image-5.png)
![alt text](image-6.png)
### Desactivamos el Firewall para comprobar la conectividad entre ellos
![alt text](image-7.png)
![alt text](image-8.png)
![alt text](image-9.png)
### 3. Configuración del acceso remoto al nuevo equipo
### - Realizar los pasos necesarios para poder usar PowershellDirect sobre el nuevo equipo desde el servidor principal (AGG-2019)
#### En la máquina de WS2016 ejecutamos el comando: "Enable-PSRemoting -Force" para habilitar la comunicación remota
![alt text](image-10.png)
#### Comprobamos los hosts confiables, como vemos en la imagen inferior WS2016 está incluido en la lista de confiables. En el caso de que no fuera afirmativo, tendríamos que utilizar el comando Set-Item WSMan:\localhost\Client\TrustedHosts -Value "ipv4"
![alt text](image-11.png)
### -Asegúrate de que sigas pudiendo administrar el otro equipo en modo Core
### -Para comprobarlo, crear de forma remota en ambos equipos en modo Core un usuario con privilegios de administrador llamado AGG. 
![alt text](image-12.png)
