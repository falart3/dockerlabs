![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/F_FirstHacking/fh_001.png)
```
nmap -p- -sS -sCV -T4 -n -Pn 172.17.0.2
```
![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/F_FirstHacking/fh_002.png)

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

<h3>PORT STATE SERVICE VERSION:</h3>

21/tcp open ftp vsftpd 2.3.4:

21/tcp: El puerto 21 está abierto y usa el protocolo TCP.

open: El puerto está abierto y aceptando conexiones.

ftp: El servicio en el puerto es FTP (File Transfer Protocol).
  
vsftpd 2.3.4: La versión del servicio FTP detectado es vsftpd 2.3.4.

![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/F_FirstHacking/fh_003.png)

El comando searchsploit vsftpd 2.3.4 ha encontrado dos exploits.

Exploit Title: vsftpd 2.3.4 - Backdoor Command Execution

Path: unix/remote/49757.py

Este exploit se refiere a una vulnerabilidad en vsftpd 2.3.4 que permite la ejecución remota de comandos a través de una puerta trasera. Esta vulnerabilidad es bien conocida y puede permitir a un atacante ejecutar comandos arbitrarios en el servidor FTP afectado.

Archivo: 49757.py es un script en Python que explota esta vulnerabilidad. Puedes encontrar este exploit en el directorio unix/remote/ dentro de la base de datos de Exploit-DB.


Path: unix/remote/17491.rb

Similar al anterior, este exploit también explota la vulnerabilidad de puerta trasera en vsftpd 2.3.4, pero está diseñado específicamente para ser utilizado con Metasploit, una plataforma de pruebas de penetración muy popular.

Archivo: 17491.rb es un script en Ruby que forma parte del framework Metasploit y está diseñado para explotar la vulnerabilidad en vsftpd 2.3.4. Se encuentra en el directorio unix/remote/.

![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/F_FirstHacking/fh_004.png)

CVE: CVE-2011-2523 es el identificador de la vulnerabilidad específica que el exploit aprovecha. Esta vulnerabilidad se relaciona con la puerta trasera en vsftpd 2.3.4.

![FirstHacking](https://github.com/falart3/dockerlabs/blob/main/F_FirstHacking/fh_005.png)

<h3>Ejecucion y Salida del Exploit</h3>

Mensaje: /root/49757.py:11: DeprecationWarning: 'telnetlib' is deprecated and slated for removal in Python 3.13

Este mensaje indica que el módulo telnetlib utilizado en el script de Python está en desuso y se eliminará en una versión futura de Python (3.13). Aunque esta advertencia no detiene la ejecución, es algo a tener en cuenta si planeas actualizar Python en el futuro.

Mensaje: Success, shell opened

El exploit se ha ejecutado con éxito y ha abierto una shell en el servidor objetivo.

Comando: whoami

Resultado: root

El comando whoami muestra el usuario actual en la shell. En este caso, muestra root, lo que significa que has obtenido acceso como usuario root en el sistema objetivo.

Mensaje Final:

Mensaje: Send 'exit' to quit shell
Descripción: Indica cómo salir de la shell abierta. Debes enviar el comando exit para cerrar la sesión de shell y terminar la conexión.

<h4>Recomendaciones</h4>
<h1>Seguridad y Ética:</h1>

Pruebas en Entorno Controlado: Asegúrate de que todo el trabajo se realice en un entorno de pruebas autorizado y controlado, como por ejemplo maquinas virtuales de dokerlabs. Ejecutar exploits en sistemas no autorizados es ilegal y poco ético.
