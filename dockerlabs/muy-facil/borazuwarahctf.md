# BorazuwarahCTF

vale empezamos desplegando el entorno , la verda este fue un reto muy facil .

<figure><img src="../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

una vez desplegado la maquina , pasamos a la fase de reconocimiento.

ya sabe siempre con nmap -sVC -Pn 172.17.0.2  , lo cual nos devuelve lo siguiente:

<figure><img src="../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

a primera vista vemos que tiene 2 puertos abiertos el ssh con el puerto 22 y el 80 con http , como tiene un puerto http significa que posiblemente tenga un sitio web.

y oh sorpresa nos encontramos con esto en el sitio web:

<figure><img src="../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

un maldito huebo jaja , bueno como primera instancia lo que haria es ver el codigo fuente para ver si esconde algun comentario o dato que nos de mas pistas:

<figure><img src="../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

vemos que se trata de una sola imagen la del huevito , por lo que podria probar herramientas para ver su metadata y ver si encontramos algo , por lo que lo descargamos.

<figure><img src="../../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

una ves descargado podremos ver su metadata con una herramienta llamada exiftool  , es un programa que sirve para leer, escribir y editar metadatos (informacion oculta) en una gran variedad de archivos como fotos , videos , documentos etc...

<figure><img src="../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

y wala , ahi esta una credencial para ingresar al servidor , borazuwarah , entonces lo que hariamos a continuacion ya  que no nos da la contraseña directamente ahi , es usar fuerza bruta para tratar de encontrar la contraseña .

<figure><img src="../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

usamos hydra con el diccionario de rockyou , y bam encontramos su contraseña que nada menos ni nada mas que era 123456 xd , bueno entonces ahora que tenemos claves podremos entrar por ssh al servidor .

<figure><img src="../../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

vale ya entramos ahora tenemos que apoderarnos del sistema completo , por lo que necesitamos escalar privilegios , colocamos nuestro comando magico siempre , para ver que podemos ejecutar con permisos de root.&#x20;

<figure><img src="../../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

usamos el comando sudo -l  para listar los binarios  o comandos que podriamos ejecutar con permisos sudo  y oh sorpresa pudemos ejecutar /bin/bash con sudo sin que nos pida contraseña el NOPASSWD.

<figure><img src="../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

ahora ya somos root y  para darle un toque mas de hacker de nosotros colocamos un dafacemet como nuestra marca ! , buscamos el directorio www/  y modificamos el html

<figure><img src="../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

e injectamos nuestro html personal ....

<figure><img src="../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>
