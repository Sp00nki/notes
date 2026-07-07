# HedgeHog

empezamos desplegando la maquina&#x20;

<figure><img src="../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>

luego pasamos a la fase de reconocimiento y le metemos nmap a lo kamikase&#x20;

<figure><img src="../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

entonces nos damos cuenta de que tiene 2 puertos abiertos el ssh y el 80 , entonces primero hechamos un vistazo al website

de primeras no encontramos nada muy relevante solo un simple texto xd

<figure><img src="../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

bueno lo primero que asimilaria es investigar el codigo fuente para ver si tene algun comentado etc.. pero no no hay mucho que ver por ese lado , tambien la enumeracion de directorios no funciona , entonces lo unico que se me ocurre es que es un posible usuario para el ssh.

<figure><img src="../../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>

bien utilize hydra para hacer el ataque de fuerza bruta , pero no encontro nada , esta raro , pero tails esa palabra no das una ligera pista tail en ingres significa cola xd , por lo que si inferimos puede significar la parte baja de una archivo , que en este caso seria nuestro diccionario , pero como hariamos para que hydra empiese a leer de abajo y no desde el inicio del archivo?...

<figure><img src="../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

existe una herramienta llamada tac para esto:  basicamente volveta toda las cadenas de texto de un archivo , por lo que le damos la ruta del archivo que deseemos volterar , pero aqui viene un punto importante ya que en el archivo original del rockyou sus ultimas lineas vienes com espacios de por medio o caracteres raros separados , esto al principio no lo habia pensado y por supuesto me tarde mucho pensando que no funcionada xd , pero no tenemos que eliminar esos espacios es por eso que usamos el otro comando tr -d ' '  el tr sirve para **traducir, reemplazar o eliminar caracteres** en un flujo de texto , por lo que con su flag -d le decimos que queremos eliminar los espacios vacios , y luego > mandarlo a un nuevo archivo con el nombre rev\_rocky.txt&#x20;

<figure><img src="../../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

vale entonces ahora si despues de unos segundos encontramos su contraseña

luego ingresamos por ese puerto  y pasamos a la fase de escalada de privilegios

<figure><img src="../../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

vemos que el usuario sonic puede ejecutar cualquier cosa con sudo , pero actualmente somos el usuario tail , por lo que analizandolo bien , podriamos hacer el siguiente comando ejecutar sudo con el usuario sonic y que el usuario sonic ejecute una shell con root&#x20;

<figure><img src="../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

y como vemos ya tenemos acceso a root . easy en su defecto podriamos haber cambiado a l usuario sonic solo ejecutando una shell para ese usuario y luego ejecutar sudo su desde su usuario para tener root , pero es mucha cosa para algo tan simple xd .
