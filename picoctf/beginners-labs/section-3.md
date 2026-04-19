# Section 3

en esta seccion seguiremos con general skills , ya que tocaremos algunos comandos basicos de linux .

empezaremos con el primer reto de esta seccion

### Wave a Flag

como primera instancia descargaremos el archivo que no da el reto, por lo que nos dice parece ser un archivo binario ejecutable

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

colocamos el comando "file" para verificar con que tipo de archivo estamos trabajando y para corrobarar que sea un jecutable.

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

como vemos efectivamente es un archivo ejecutable . por lo que procederemos a darle permisos de ejecucion y ejecutarlo

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

oh! que paso , lo que nos dice basicamente es que le coloquemos su flag, parameto -h para ver que puede hacer .

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

y walaaa , una vez colocado la flag -h podemos ver que nos dice que no sabe muchox pero nos regala la flag xd .



### Tab,Tab,Attack

siguiendo con este reto , pensaremos un poco en como llegar a la flag por la cantidad de informacion que tenemos en pantalla

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

descargamos el zip que nos da el reto y lo descomprimimos con el comando unzip

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

nos dejara una serie de carpetas , lo podemos ver con el comando tree para ver las subcarpetas&#x20;

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

nos dice que hay 7 directorios y 2 archivos , por lo que podemos hay 2 formas de optener la flag

una es haciendole un cat directamente hasta los archivos y ver el contenido&#x20;

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

en este caso hicimos un cat al archivo con la extencion .c que es nos quiere decir que es programa escrito en el lenguaje de programacion C , y si vemos dentro del codigo veremos la flag del reto , por otro lado esto nos intuye que es un programa ejecutable  por ende ejecutaremos el otro archivo&#x20;

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

y como vemos nos devuelve la flag de igual forma.



### Insp3ct0r

en este reto  se sale un poquito mas al analizis de codigo , pero no es tan complejo , empezamos desplegando el reto

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

una vez desplegado el reto , no dara una url , al que debemos ingresar por lo que nos da la siguiente web

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

a primera vista parece una web simple , pero nos dice inspecioname , asi que abrimos las opciones de desarrollador con atajo de teclado ctrl + shift + i  , al abrirse las herramientas de desarrollador podremos inspeccionar un poco el codigo de la pagina web , dandonos cuenta que hay un comentario&#x20;

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

no dice el comentario que html es genial XD , pero que nos da 1 de 3 partes de la flag , por lo que si nos vamos al apartado de source  veremos otros dos archivos con extencions .js y .css , que vendrian siendo el complemento de construccion de un sitio web.&#x20;

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

luego al analizar estos archivos , vemos que tambien tiene parte de las flag en comentarios&#x20;

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

entonces uniendo todas las partes tendremos flag dandonos como resultado la resolucion de este reto.

este reto me gusto mucho ya que es algo que podriamos hacer con paginas reales y quisas detectar comentarios que no deberian estar a la vista de todo mundo :O



### Strings it

en este reto no dice que si podemos encontrar la flag dentro de este archivo sin ejecutarlo

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

bien una vez descargado hacemos un file al archivo para ver de que se trata&#x20;

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

com vemos es un archivo binario ejecutable , por lo que si te creias listo y ejecutabas el programa como yo lo hice xd , te saldra un mensaje diciendote  "quisas puedas probar con 'strings'" lo cual nos dice que lo busquemos en el pagina del manual con "man" , lo se quisas esto sea nuevo , peeero quedate con que es un comando para mostrarte caracteres legibles dentro de un archivo ,.

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

lo que hice fue usar el comando strings sobre el archibo y con su ouput contabilizar cuantas lineas mostraria por pantalla y como vemos son 19243 lineas que se mostrarian en la pantlla lo cual nos demorariamos un monton en buscar la flag , es aqui donde entra el comando magico "grep" con grep buscaremos por palabras clave que en este caso usaremos "pico" xd como la flags en si empiezan por eso pues fue lo que se me ocurrio,&#x20;

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

y como vemos nos filtra por esa palabra magica y boom la flag xd y ya .



### First Grep

bien en este reto nos dice lo mismo si podemos encontrar la flag dentro del archivo , nos dice que podria ser tedioso hacerlo manualmente , pero siempre hay mejores maneras de hacerlos .&#x20;

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

bueno al hacerle un strings al archivo tiene muchos caracteres sin sentido.

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Buscar la flag manualmente sería tedioso dado el volumen de datos, por eso recurrimos a `grep` — pero esta vez explorando parámetros más específicos.

Si ejecutamos simplemente `grep "picoCTF" file` no obtenemos nada útil, el output sigue siendo ruido sin sentido. Esto ocurre porque `grep` trabaja línea por línea y el contenido binario mezclado con texto rompe la detección. La solución es combinar dos flags clave:

**`-o`** → Muestra únicamente la parte del texto que coincide con el patrón, descartando el resto de la línea.

**`-E`** → Activa las _Extended Regular Expressions_, necesario para que símbolos como `{` y `}` funcionen correctamente en el patrón.

Y aquí entra **regex** por primera vez. El patrón `.*` se compone de dos elementos:

* **`.`** → cualquier carácter (letra, número, símbolo)
* **`*`** → el elemento anterior puede repetirse 0 o más veces

Combinado todo, el comando final queda:

```
strings file | grep -oE "picoCTF{.*}"
```

`strings` extrae el texto legible del archivo binario, y `grep` captura exactamente la flag sin ruido. 🎯

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

dandonos la flag completa.



### Where are the Robots

aqui tocamos un poquito de web explotation ,  el reto nos dice ¿puedes encontrar los robots?

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

una vez desplegado el reto , nos da un url , al ingresar , nos muestra esta pagina&#x20;

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

y nos dice  ¿donde estan los robots? xd , bueno aqui debemos de saber que existen archivos ocultos importantes por ejemplo El archivo `robots.txt` es un documento de texto plano situado en la raíz de un sitio web que funciona como una "guía de instrucciones" para los buscadores (Google, Bing). Indica a los robots qué páginas **no** deben rastrear o visitar, ayudando a gestionar el presupuesto de rastreo y mantener zonas privadas.&#x20;

por lo cual no deberian de verse en una web comun con seguridad .  ya que puede ser un vector critico&#x20;

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

intentamos ingresar a ese archivo desde el url.  y oh sorpresa nos encontramos con que esta ocultando un archivo .html&#x20;

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

entonces que pasa si colocamos ese archivo en el url ya accedemos al recurso.

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

y boom encontramos la flag ,  basicamente encontramos el archivo de robots.txt que le dice a los buscadores que no indexen sitios webs que esten dentro de ese archivo de texto , lo cual es ironico por que hay desarrolladores que guardan contenido sensible ahi haciendo que cualquier persona haciedno reconocimiento basico lo encuentre.
