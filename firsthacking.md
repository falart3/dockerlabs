![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_001.png)
```
nmap -p- -sS -sCV -T4 -n -Pn 172.17.0.2
```
![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_002.png)

<h3>Desglose del Comando</h3>

nmap: Esta herramienta se utiliza para realizar el escaneo de red, puertos y servicios.

-p-: Este parámetro le indica a nmap que escanee todos los puertos posibles (del 1 al 65535). Si quisieras especificar un rango de puertos, podrías usar algo como -p 1-1000 para escanear solo los primeros 1000 puertos.

-sS: Esta opción realiza un escaneo de puertos SYN. nmap envía paquetes SYN a los puertos y espera respuestas.

-sCV: Esta opción le dice a nmap que use scripts de la categoría "default" (por defecto) para la detección de servicios (-sC) y para realizar la detección de versiones de los servicios (-sV).

-sC: habilita los scripts predeterminados de nmap, que realizan una serie de pruebas estándar en los servicios detectados.

-sV: realiza una detección de versiones, intentando identificar la versión exacta del servicio que está escuchando en cada puerto abierto.

-T4: Esta opción ajusta la velocidad del escaneo a un nivel más agresivo. nmap tiene perfiles de tiempo (T0 a T5), donde T4 proporciona un equilibrio entre velocidad y precisión, haciéndolo adecuado para la mayoría de los entornos de red.

-n: Indica que nmap no debe realizar la resolución de nombres DNS para las direcciones IP. Esto puede acelerar el escaneo y evitar la resolución de nombres innecesarios.

-Pn: Esta opción le dice a nmap que no realice el escaneo de hosts (descubrimiento de hosts) y asuma que el host está activo. Esto es útil si estás seguro de que el host está en línea o si estás escaneando una red donde el descubrimiento de hosts podría ser bloqueado por un firewall.

172.17.0.2: Es la dirección IP de dockerlabs.es que cargamos con bash auto_deploy.sh firsthacking.tar, es el objetivo que estamos escaneando.

PORT STATE SERVICE VERSION:

21/tcp open ftp vsftpd 2.3.4:

21/tcp: El puerto 21 está abierto y usa el protocolo TCP.

open: El puerto está abierto y aceptando conexiones.

ftp: El servicio en el puerto es FTP (File Transfer Protocol).
  
vsftpd 2.3.4: La versión del servicio FTP detectado es vsftpd 2.3.4.

![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_003.png)
![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_004.png)
![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_005.png)
