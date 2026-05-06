---
coverY: 0
coverHeight: 394
layout:
  width: default
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Trust

vale en este primer reto o maquina , no nos dan una descripcion , por lo que tendremos que ver que se nos presenta en el camino hasta hayar la flag.

como primer paso seria desplegar la maquina , es un contenedor docker , su desplegue es super simple dejare una guia corta en la seccion de dockerlabs , si no igual puede ver la documentacion de la misma plataforma.

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

vale una vez desplegado nos da una direccion ip , por lo que empezariamos con la fase de reconocimiento .

```
nmap -sVC -Pn 172.18.0.2
```

usamos la herramienta nmap acompañado con la flag -sVC y -Pn , la primera flag del comando nmap nos ayudara a  encontrrar posibles vulnerabilidades en los puertos y servicios que estan corriento y que nos mostrara mas informacion detllada. y el segundo flag nos ayuda a evitar la resolucion dns o mejor dicho a qu no haga el ping al host por que sabemos que ya esta activo.

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

podemos   ver que hay 2 puerto abiertos , el puerto 22 y el 80 , el puerto 22 siendo ssh , y 80 http , por lo que se me ocurre es ingresar por ssh al servidor , pero no conocemos ni un usuario ni contraseña , revisemos el puerto 80.

<figure><img src="../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

solo nos sale informacion default del servidor ,  pero aqui entra otra posibilidad , y si buscamos directorios o archivos ocultos que esten en el servidor?.. probemos

```
gobuster dir -u http://172.18.0.2/ -w /usr/share/seclists/Discovery/Web-Content/common.txt 
-x php,html,txt -t 50
```

usamos la herramienta gobuster , que es para hacer fuerza bruta de directorios o archivos , usamos sus parametros dir -u para decirle que haga un tipo de ataque de fuerza bruta de directorios  y con el -u es para indicare el url , luego -w para pasarle la lista de palabras almacenados en un diccionario para probar , y aqui viene lo importante .   la primera vez que ejecute esto fue asi sin el  -x php,html,txt , cosa que no me aparecia el archivo oculto que se necesitaba encontrar para continuar con el reto ,  luego entendi que gobuster en su peticiones busca tal que asi  host/secret  , busca las palabras del diccionario directamente sin extenciones , por lo que si quisieramos encontrar archivos ocultos con extenciones , gobuster no nos lo mostraria lo ingnoraria , es por eso que usamos el -x para decirle que haga una doble peticion sin extencion host/secret y con extencion host/secret.php , con esto claro pude dar con el archivo oculto necesario.

<figure><img src="../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

como vemos nos aparece directorios y archivos con sus extenciones , pero nos interesa una en especial que es  "secret.php"  nos da un estatus 200 que significa que esta operativa la pagina, accedemos al archivo desde la url del host.

<figure><img src="../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

y como vemos se encuentra un mensaje para nosotros , y nos dice  que el sitio web no se puede hackear xd , y es aqui cuando decimos , que carajos hago ahora xd , como novato la primera vez que lo resolvi , pense que era el fin y no sabia a donde avanzar , pero luego entendi que hay que ser muy minusioso y detalles . si vemos bien nos dice "hola Mario" , y si recordamos al principo queriamos entrar por ssh , pero no sabiamos ni un usuario ni contraseña , pero ahora este mensaje en esta pagina nos da un nombre.. podria ser un usuario o no?...

```
hydra -l mario -P /usr/share/dict/rockyou.txt ssh://172.18.0.2
```

como tenemos un posible usuario utilizamos la herramienta hydra , que nos sirve para hacer fuerza bruta con diccionario , en este paso para el servicio ssh , entonces colocamos la flag -l para expecificar el usuario y -P para seleccionar el diccionario con las posibles contraseña luego ssh:/host , para realizar la conexion con ese intento de logueo .

<figure><img src="../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

y como vemos en segundos nos muestra la contraseña de ese usuario que fue valido , entonces ahora si podemos entrar al servidor por ese servicio.

<figure><img src="../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

y asi es como estamos dentro del servidor!!! increible no? , pero eso no es todo xd si queremos el control total tenemos que ser el usuario administrador , o mas conocido en el mundo de hacking como root  , esta es una fase de la metodologia de pentesting llamada post explotacion / escalada de privilegios , lo veremos mucho en este tipo de retos donde entramos a un servidor o maquina objetivo y como logramos eso?.. aqui tambien me perdi al comienzo pero luego entendi que podemos ir revisando cosas poco a poco hasta hayar con algun fallo del sistema que nos permita ser el usuario maximo.

<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

se me ocurrio usar el comando sudo  -l  que lista los comandos que puedo ejecutar con permisos de superusuario root ,  entonces vemos una linea en especial que nos dice que podemos usar el comando sudo con el binario vim , vim es un editor de texto por lo que dentro de vim podemos ejecutar comandos del sistema , entonces siguiendo un analogia seria  ejecuto vim con sudo con permisos de usuario maximo y dentro de vim coloco un comando para que me de una shell de root .

```
sudo vim -c ':!/bin/bash'
```

si ejecutamos esta linea , basicamente estamos metiendo una bash dentro de vim y al ejecutarse nos retornara una shell pero con el usuario root

<figure><img src="../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

y asi es como optenemos el control total del sistema ! , mucho texto , pero creo que me hubiera gustado una resolucion asi para aprender.

