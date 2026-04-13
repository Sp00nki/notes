# Section 2 (CyberChef)

en esta segunda seccion , tendremos lo que un poco de criptografia y motodos de encryptado comunes, de igual forma estos ejercicios de esta seccion pueden resolverse con [CyberChef](https://gchq.github.io/CyberChef/)

### Mod26

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

en este primer reto tendremos que hallar la contraseña cifrada en ROT13 , ROT13 es un cifrado súper simple que cambia cada letra por la que está 13 lugares después en el abecedario. Si llegas al final (Z), vuelves al principio (A). Lo curioso es que, como el abecedario tiene 26 letras, **aplicar ROT13 dos veces devuelve el mensaje original**, por lo que sirve para cifrar y descifrar.

descargamos el archivo que nos propociona el reto , luego lo inspeccionamos con cat.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

como vemos nos devuelve la flag o se intuye eso, solo que esta con letras sin sentido , puesto que esta en ROT13 , debemos desifrarlo , podemos hacerlo con la web cyberchef o de forma local utilizando el siguiente comando .

```bash
cat values.txt| tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>



### Warmed UP

en este reto tendremos que hacer una conversion de bases , en este caso sera de base16(hexadecimal) a base10(decimal).

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

nuevamente lo puedes hacer a travez de la web o de forma local el valor 0x3D

hay 2 comandos en particular que me gusta usar que son lo siguiente.

```zsh
printf "%d\n" 0x[valor_hex] 
```

```bash
echo "ibase=16; [valor_hex]" | bc ## colocar el valor sin el 0x
```

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>



### 2warm

aqui el reto es igual , debemos de pasar de base 10 (decimal) a base 2 (binario)

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

por lo que usaremos los siguientes comandos de forma local para el numero correspondiente 42.

```zsh
echo "obase=2; 42" | bc
```

```zsh
dc -e "2o 42p"
```

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

### Bases

en este reto tendremos que decrifar un texto que esta crifado en base64 este cifrado es muy comun.

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

Base64 es un método para convertir datos binarios (imágenes, archivos, documentos) en una cadena de texto (letras, números y símbolos) legible y segura, diseñada para transportarse por internet sin corromperse. Básicamente, "traduce" archivos complejos a un formato ASCII seguro que cualquier sistema puede manejar sin errores.

por lo que podemos usar este comando de forma local para mostrar el texto original.

```zsh
echo "texto"| base64 -d
```

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

como vemos nos da la flag , con delimitador % todo lo anterior es la flag.

