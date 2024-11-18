# PROYECTO DE LA PRIMERA EVALUACIÓN
## Realizado por: Ana B. García
## ANÁLISIS DE REDES
### Crearemos un script en Bash para permitir analizar una red local para detectar equipos conectados, identificar puertos abiertos y tratar de obtener el sistema operativo de cada equipo. 
### Funcionalidades del proyecto:
#### solicitar la dirección IP y luego hacemos un ping a cada una  de las direcciones IP de la red para conocer si hay algún equipo con esa IP o no, se indicará con la resolución del ping: satisfactorio o fallido.

```bash
#!/bin/bash
read -p "Introduce la dirección IP en formato CIDR" ip
read -p "Escribir el nombre de archivo para el almacenamiento de los d>touch "$archsalida"
echo "Ping to $ip"
ping -c 1 -w 1 "$ip" &>/dev/null
if [$? -eq 0]; then
        echo "Equipo localizado: $ip" >> "$archsalida"
fi
```

