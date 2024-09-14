![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_001.png)
<center>
![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_002.png)
</center>
<h3>nmap -p- -sS -sCV -T4 -n -Pn 172.17.0.2</h3>

<h1>Desglose del Comando</h1>
nmap: Es la herramienta que estoy utilizando para realizar el escaneo de red y puertos.

-p-: Este parámetro le indica a nmap que escanee todos los puertos posibles (del 1 al 65535). Si quisieras especificar un rango de puertos, podrías usar algo como -p 1-1000 para escanear solo los primeros 1000 puertos.

-sS: Esta opción realiza un escaneo de puertos SYN, también conocido como escaneo "stealth" o sigiloso. nmap envía paquetes SYN a los puertos y espera respuestas. Este tipo de escaneo es menos probable que sea detectado por sistemas de detección de intrusiones en comparación con un escaneo TCP completo.

-sCV: Esta opción le dice a nmap que use scripts de la categoría "default" (por defecto) para la detección de servicios (-sC) y para realizar la detección de versiones de los servicios (-sV).

-sC habilita los scripts predeterminados de nmap, que realizan una serie de pruebas estándar en los servicios detectados.
-sV realiza una detección de versiones, intentando identificar la versión exacta del servicio que está escuchando en cada puerto abierto.
-T4: Esta opción ajusta la velocidad del escaneo a un nivel más agresivo. nmap tiene perfiles de tiempo (T0 a T5), donde T4 proporciona un equilibrio entre velocidad y precisión, haciéndolo adecuado para la mayoría de los entornos de red.

-n: Indica que nmap no debe realizar la resolución de nombres DNS para las direcciones IP. Esto puede acelerar el escaneo y evitar la resolución de nombres innecesarios.

-Pn: Esta opción le dice a nmap que no realice el escaneo de hosts (descubrimiento de hosts) y asuma que el host está activo. Esto es útil si estás seguro de que el host está en línea o si estás escaneando una red donde el descubrimiento de hosts podría ser bloqueado por un firewall.

172.17.0.2: Es la dirección IP del objetivo que estás escaneando. Reemplaza esta dirección con la IP del host o rango de hosts que desees investigar.


![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_003.png)
![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_004.png)
![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/fh_005.png)
