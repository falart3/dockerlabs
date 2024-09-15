
![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_001.png)

Realizamos el escaneo con Nmap sobre la dirección IP 172.17.0.2 para revelar resultados.
```
nmap -p- -sS -sCV -T4 -n -Pn 172.17.0.2
```
Si quieres un desglose de este comando puedes ver [FirstHacking](https://github.com/falart3/dockerlabs/blob/main/firsthacking.md)

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_002.png)

<h3>Análisis de los Servicios Abiertos</h3>
SSH (Puerto 22):<br>
  La versión de OpenSSH detectada es relativamente antigua (7.6p1), lo que podría ser vulnerable si no está debidamente actualizada.
<br><br>

HTTP (Puerto 80):<br>
  El servidor web Apache 2.4.29 también es una versión que podría tener vulnerabilidades, ya que ha habido actualizaciones importantes desde entonces. 
<br><br>

Lista a seguir:<br>
  investigar si existen vulnerabilidades para el puerto 22<br>
  investigar posibles exploits o revisar configuraciones incorrectas en el puerto 80<br>
<br>
Lo mas simple y rapido sera ver primero ver la ip en el puerto 80 http://172.17.0.2:80 <br>
Pero tambien puedes utilizar curl para ver el codigo fuente del html en la consola. <br>
<br>
![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_0021.png)

Como vemos hay un comentario en html (un mensaje oculto) que indica la presencia de una comunicación interna.<br>
Esto puede ser interesante desde una perspectiva de enumeración de información.<br>
Si bien Juan y Camilo son los nombres involucrados en la comunicacion, podemos usar esto pensando que quizas sean tambien nombres de usuarios.<br>
Es decir que son dos posibilidades mas a parte de admin y root<br>
Antes de otros ataques mas profundos a los puertos 22 y 80, como busqueda de directorios o exploits.<br>
Usaremos un ataque de fuerza bruta con hydra utilizando estos dos nuevos posibles usuarios.<br>
```
hydra -l juan -P /ruta/a/diccionario.txt ssh://172.17.0.2
```

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_003.png)

No hemos encontrado nada para este supuesto usuario "juan"<br>
Ahora haremos lo mismo con el supuesto usuario "camilo"<br>

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
