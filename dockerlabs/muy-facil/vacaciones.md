# Vacaciones

desplegamos la maquina

<figure><img src="../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

ejecutamos un escaneo con nmap

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

idenficamos dos puertos el 80 y el 22 , tipico que ya ehmos visto hasta ahora  entonces vallamos primero por la web.&#x20;

de primeras no encontramos nada es una pagina en blanco pero si analizamos el codigo fuente tenemos lo siguiente

<figure><img src="../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

un mensaje de un tal juan que le escribe a camilo , tenemos dos nombres que podrian ser tranquilamente usuarios del servidor , por lo que pasamos a la fase de explotacion y ejeuctamos una fuerza bruta contra un nombre.

<figure><img src="../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

con el usuario de juan no encontro nada asi que probe con camilo y vemos que si encontro una contraseña , nos conectamos al puerto

y como nos dice que nos han enviado un correo indagamos en la carpeta mail y esto encontramos:

<figure><img src="../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

vemos que el correo tiene una contraseña que pensandolo puede ser de juan probemos !

<figure><img src="../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

funciono si era la contraseña de juan , ahora bien el si tiene permisos de ejuctar un binario con sudo que es ruby , lo podemos usar para escalar privilegios y ser root.

<figure><img src="../../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

entonces ejetuamos ruby con la ejecucion de un shell bash y no da acceso root.
