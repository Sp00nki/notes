---
description: >-
  en esta primera seccion tendremos retos de general skills para entender el
  entorno
---

# seccion 1 (sanity)



### Obedient Cat

Este es un reto bastante sensillo si ya sabes bash o usar almenos la terminal de linux xd

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

bien como primera instancia no dice que la flag esta a simple vista, por lo que se me viene a la mente utilizar el comando cat , El comando `cat` (abreviatura de _catenate_ o concatenar) es una herramienta básica en la terminal de Linux y Unix que sirve para **leer, visualizar y combinar archivos de texto.**

entonces descargamos el archivo a nuestra maquina local(esto se puede hacer virtualmente desde la misma plataforma , pero lo hago asi para tener mas comodidad)

luego utilizamos el comando cat para leer el contenido que tiene dicho fichero

```
cat flag
```

por lo que nos da como resultado:

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

y ahi lo tenemos esa es la flag que necesitamos para completar el reto  , son comandos basicos de linux.



### Súper SSH

continuamos resolviendo , aqui el reto es el siguiente:

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

nos dice que habra mas detalles del reto despues de iniciar la instancia , le damos al boton celeste.

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

obtemos la siguiente informacion , nos dice que debemos de conectar por el protocolo seguro de shell SSH , para encontrar la flag , y que si al conectarnos nos pide una clave sera la siguiente <mark style="background-color:$primary;">1db87a14.</mark>

entonces nos conectamos de la siguiente manera

```bash
SSH ctf-player@titan.picoctf.net -p 61368
```

ese comando hace que nos conectemeos con el usuario "ctf-player" acompañado de un "@" para delimitar el usuario del host o ip al que nos queremos conectar de forma remota y el host seria "titan.picoctf.net" le especificamos el puerto de coneccion mediante el parametro "-p" acompañado del numero de puerto que en este caso es "61368" , que la ejecutarse no da lo siguiente

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

nos pide que coloquemos la contraseña anterorior mente mostrada:

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

y como ven ya nos dara la flag para terminar el reto .



### what's a net cat?

aqui mas de lo mismo , iniciamos la instancia para que nos de los demas detalles

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

bien aqui nos dice que utilizemos el comando Netcat , El comando **netcat** (abreviado como `nc`) es conocido como la "navaja suiza" de las redes. En términos muy simples: es una herramienta que te permite **enviar y recibir datos** entre computadoras a través de una red.

basicamente un cat , pero remotamente xd , entonces continuando utilizaremos  el host "fickle-tempest.picoctf.net" en el puerto "60695" para optener la flag.

entonces ejecutamos lo siguiente:

```
nc fickle-tempest.picoctf.net 60695
```

lo que nos dara como resultado:

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

haciendo esta coneccion atraves de netcat , nos dara la flag.

con esto estariamo terminando la primera seccion de esta playlist para prinpipiantes de la plataforma de picoctf .

