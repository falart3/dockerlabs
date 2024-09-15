
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

SI!<br>
camilo es un nombre de usuario y probablemente juan tambien lo sea!<br>
Hydra ha tenido éxito y ha encontrado la contraseña para el usuario Camilo en el servicio SSH del host 172.17.0.2. La credencial descubierta es:
<br>
Usuario: camilo<br>
Contraseña: password1<br>
<br>
Conexión SSH:<br>
Ahora puedemos usar estas credenciales para conectarnos al servidor SSH en 172.17.0.2.<br>
Usaremos el siguiente comando para iniciar sesión:<br>
```
ssh camilo@172.17.0.2
```
Cuando se te solicite la contraseña, ingresamos password1.

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_005.png)

Recordemos que en el archivo web encontramos un mensaje oculto sobre un "correo"<br>
El comentario sugiere que puede haber información confidencial o relevante en algún archivo o servicio relacionado con correos electrónicos. Podemos buscar más información en directorios para ver si hay rutas ocultas, servicios adicionales disponibles omensajes.<br>

```
find / -name "*.txt" 2>/dev/null
```
/ :<br>
Como no se donde puedo encontrar, mi punto inicial sera el directorio raíz desde donde se inicia la búsqueda.<br>
-name "*.txt" :<br>
Esto especifica que estmos buscando archivos que terminen en .txt.<br>

2>/dev/null :<br>
Esto oculta los mensajes de error relacionados con la falta de permisos en algunos directorios.<br>

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_006.png)

En el listado podemos ver dentro de estos directorios info relevante:<br>
/var/mail/camilo/correo.txt<br>
Con la siguiente instruccion podemos ver que dice el texto<br>


```
cat /var/mail/camilo/correo.txt
```
![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_007.png)

😮 😊<br>
No solo podemos acceder con el usuario camilo, sino que ahora tambien con juan.<br>
Dentro de este usuario intentaremos escalar a root 🤞 <br>

![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_008.png)

Parece que hemos logrado cambiar de usuario a Juan, pero no tenemos permisos para usar sudo su para escalar privilegios a root.<br>
Sin embargo, hay varias estrategias que podríamos intentar en función de las vulnerabilidades del sistema y de los permisos disponibles.<br>
Podríamos verificar si Juan tiene permisos para ejecutar otros comandos con sudo.<br>
Tambien buscar archivos con permisos SUID, ver si hay algún cron job mal configurado, buscar archivos con permisos de escritura, etc<br>
Para ello, primero utilizaremos el comando sudo -l para ver la lista de comandos permitidos:<br>
Esto nos mostrará si el usuario Juan tiene permisos para ejecutar ciertos comandos como root sin necesidad de contraseña.<br>
```
sudo -l
```
Parece que el usuario Juan tiene permisos para ejecutar el comando /usr/bin/ruby como root sin necesidad de proporcionar una contraseña.<br>
Esto es una gran oportunidad para escalar privilegios, ya que puedes usar Ruby para ejecutar código como root.<br>
Utilizaremos el siguiente comando para iniciar un shell interactivo con permisos de root usando Ruby<br>
```
sudo /usr/bin/ruby -e 'exec "/bin/bash"'
```
![Vacaciones](https://github.com/falart3/dockerlabs/blob/main/vc_009.png)

Lo hemos conseguido! 🎉🥳🎊

<h4>Recomendaciones</h4>
<h1>Seguridad y Ética:</h1>

Pruebas en Entorno Controlado: Asegúrate de que todo el trabajo se realice en un entorno de pruebas autorizado y controlado, como por ejemplo maquinas virtuales de dokerlabs. Ejecutar atauqes en sistemas no autorizados es ilegal y poco ético.
