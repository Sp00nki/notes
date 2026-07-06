# BreakMySSH

bien desplegamos este reto

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

luego pasamos a la fase de reconocimiento con el mismo comando

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

vale identificamos que solo tiene un puerto abierto el ssh , entonces podriamos invetigar su servicio y version en busca de vulnerabilidades conocidas.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

encontramos que si tiene una vulnerabilidad la version del servicio corriendo , por lo que  nos dice se trata de una enumeracion de usuarios para el puerto ssh , por lo tanto usaremos la herramienta hydra para la enumeracion de usuario con un diccionario y junto en la misma oneliner la enumeracion de password con otro diccinonario dandonos como resultado esto: &#x20;

<figure><img src="../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

entonces lo que hicimos solo fue automatizar la enumeracion , pero si quisieramos crear nuestro propio exploit para esa vulnerabilidad tendriamos que entender esto.

la vulnerabilidad de enumeración en SSH ocurre porque el servidor procesa las solicitudes de forma asimétrica según la existencia del usuario; si introduces un usuario **falso** junto con un paquete de datos malformado, el servidor rechaza la conexión de inmediato al no encontrar el nombre en el sistema, mientras que si introduces un usuario **verdadero**, el servidor valida el nombre y luego intenta procesar el paquete malformado, lo que genera un error interno detectable o un retraso en el tiempo de respuesta.

como vemos estamos dentro :p&#x20;

<figure><img src="../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>
