# Section 5 (analizis y explotacion)

bien en esta ultima seccion veremos un poco de forensis , ingenieria inversa y explotacion de binario , esta seccion podria ser un poco mas dificil que las demas , pero aprenderemos en el camino , siempre hackeando nunca webiando&#x20;



### Enhance!

en este primer reto , nos da una imagen y debemos de encontrar la flag dentro. el diablo!! xd

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

bien como primer vistado tiene extension .svg , lo cual es un archivo en xml . no una imagen como tal , lo abrimos desde el navegador o con cat

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

como vemos dentro del codigo xml , encontramos la flag dispersa , la agrupamos con este comando

```zsh
grep -oE 'id="tspan[0-9]+">[^<]+' tu_archivo.svg | sed 's/id="tspan[0-9]*">//' | tr -d '\n' | sed 's/ //g'
```

#### **Explicación del Comando**

1. **`grep -oE 'id="tspan[0-9]+">[^<]+'`:**
   * `-o`: Muestra solo la parte que coincide con el patrón.
   * `-E`: Habilita expresiones regulares extendidas.
   * `'id="tspan[0-9]+">[^<]+'`: Busca todas las etiquetas `<tspan>` y extrae el texto dentro de ellas.
2. **`sed 's/id="tspan[0-9]*">//'`:**
   * Elimina la parte `id="tspanXXXX">` de cada línea.
3. **`tr -d '\n'`:**
   * Elimina los saltos de línea para unir todo el texto en una sola línea.
4. **`sed 's/ //g'`:**
   * Elimina los espacios en blanco para dejar solo la flag.



### Big Zip

en este reto , tenemos un directorio lleno de archivos de texto , por lo que se nos haria imposible dar con la flag manual mente , por lo que podremos usar el comando grep.

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

usamos el siguiente comando para encontrar la flag dentro de toda esa cantidad de archivos de texto.

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

***

**2. `-r` (o `--recursive`)**

* **Función:** Busca **en todos los subdirectorios** a partir del directorio actual.

***

**3. `--include="*.txt"`**

* **Función:** **Filtra los archivos** para que `grep` solo busque en archivos con la extensión `.txt`.
* **Ejemplo:** Ignorará archivos como `.py`, `.sh`, `.log`, etc., y solo buscará en `.txt`.
*   **Alternativa:** Si quisieras buscar en archivos `.log` y `.txt`, podrías usar:

    ```
    bashCopygrep -r --include="*.txt" --include="*.log" -E "picoCTF" .
    ```

***

**4. `-E`**

* **Función:** Activa el modo de **expresiones regulares extendidas** (ERE).
* **¿Por qué usarlo aquí?** Aunque en este caso no es estrictamente necesario (porque `"picoCTF"` es un texto literal), es útil si quieres buscar patrones más complejos, como:
  * `picoCTF{.*}` (para encontrar flags completas, ej: `picoCTF{abc123}`).
  * `[Pp]ico[Cc][Tt][Ff]` (para buscar variaciones como `PicoCTF`, `picoctf`, etc.).
* **Alternativa:** Si solo quieres buscar texto literal (sin expresiones regulares), usa `-F`.

***

**5. `"picoCTF"`**

* **Función:** Es el **patrón de búsqueda**. `grep` buscará este texto exacto en los archivos.
*   **Ejemplo:** Si un archivo `.txt` contiene:

    ```
    textCopyLa flag es picoCTF{123}
    ```

    Esta línea será mostrada en el resultado.BENNETT

***

**6. `.`**

* **Función:** Indica el **directorio donde buscar**. El `.` representa el **directorio actual** (donde estás ejecutando el comando).



### Vault-door-training

#### **📌 Descripción del Reto**

El reto consiste en un programa en Java que pide una contraseña al usuario. El objetivo es **encontrar la contraseña correcta** para obtener el mensaje _"Access granted"_.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

en este reto nos da una mini historia , para analizar el codigo fuente de un programa , por lo que vemos esta escrito en java .

&#x20;![](<../../.gitbook/assets/image (5).png>)

como vemos a simple vista no  estan dificil encontrar la flag , por que si no enfocamos en una parte del codigo veremos que hace lo siguiente:

#### **🔍 Análisis del Código**

El programa hace lo siguiente:

1. **Pide al usuario que ingrese una contraseña.**
2. **Procesa la entrada** para extraer el texto entre `picoCTF{` y `}`.
3. **Compara** el texto extraído con una contraseña oculta en el código.
4. **Si coincide**, imprime _"Access granted"_. Si no, imprime _"Access denied!"_.

***

#### **💡 Solución**

**1. Encontrar la Contraseña Oculta**

Al revisar el código, vemos que la contraseña está **directamente en el método `checkPassword`**:

```java
javaCopypublic boolean checkPassword(String password) {    return password.equals("w4rm1ng_Up_w1tH_jAv4_000uMfhzBuS");}
```

* **La contraseña es:** `w4rm1ng_Up_w1tH_jAv4_000uMfhzBuS`.

**2. Formato de la Entrada**

El programa espera que la entrada del usuario esté en el formato:

```
picoCTF{contraseña}
```

* **Contraseña completa:** `picoCTF{w4rm1ng_Up_w1tH_jAv4_000uMfhzBuS}`

***

#### **🎯 Explotación**

1. **Ejecuta el programa** (si tienes el archivo `.java`, compílalo con `javac VaultDoorTraining.java` y ejecútalo con `java VaultDoorTraining`).
2.  **Ingresa la contraseña completa:**

    ```
    Enter vault password: picoCTF{w4rm1ng_Up_w1tH_jAv4_000uMfhzBuS}
    ```
3.  **Resultado:**

    ```
    Access granted.
    ```

***

#### **📌 Flag**

La flag para este reto es:

```
picoCTF{w4rm1ng_Up_w1tH_jAv4_000uMfhzBuS}
```

***

#### **💭 Lección Aprendida**

* **Nunca guardes contraseñas en el código fuente** de forma visible. En este caso, el comentario del desarrollador (`// The password is below...`) ya nos da una pista de que la contraseña está en el código.
* **Revisar el código fuente** es una de las primeras cosas que debes hacer en retos de programación.

***

**¡Y listo!** El reto se resuelve simplemente **leyendo el código** y entendiendo cómo procesa la entrada del usuario. 😊🔥



### Keygenme-py

### Descripción <a href="#descripcin" id="descripcin"></a>

Se nos proporciona un programa Python que actúa como una calculadora con licencia. Para obtener la flag debemos encontrar la **license key** correcta que desencripta la versión completa.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### Análisis del código <a href="#anlisis-del-cdigo" id="anlisis-del-cdigo"></a>



Al leer el código identificamos tres variables clave al inicio:

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

```python
key_part_static1_trial = "picoCTF{1n_7h3_kk3y_of_"
key_part_dynamic1_trial = "xxxxxxxx"   # 8 caracteres desconocidos
key_part_static2_trial  = "}"
```

La licencia completa es la concatenación de las tres partes. Las dos partes estáticas ya las tenemos — el reto es encontrar los **8 caracteres dinámicos**.

### Función check\_key() <a href="#funcin-checkkey" id="funcin-checkkey"></a>

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

La función verifica carácter por carácter que la parte dinámica coincida con posiciones específicas del SHA256 del username `"BENNETT"`:

```
if key[i] != hashlib.sha256(username_trial).hexdigest()[4]:
```

Los índices utilizados en orden son: `[4, 5, 3, 6, 2, 7, 1, 8]`

### Solución <a href="#solucin" id="solucin"></a>

Escribimos un script que calcula el SHA256 de `b"BENNETT"`, extrae los caracteres en esos índices y arma la flag completa:

```python
pythonimport hashlib

result_hash = hashlib.sha256(b"BENNETT").hexdigest()
indices = [4, 5, 3, 6, 2, 7, 1, 8]

dinamico = "".join([result_hash[i] for i in indices])
flag = "picoCTF{1n_7h3_kk3y_of_" + dinamico + "}"
print(flag)
```

### Flag <a href="#flag" id="flag"></a>

```
picoCTF{1n_7h3_kk3y_of_<output_del_script>}
```

### Lección aprendida <a href="#leccin-aprendida" id="leccin-aprendida"></a>

Siempre mapear **todas las variables globales** al inicio del código antes de analizar la lógica — los datos clave suelen estar declarados ahí y es fácil pasarlos por alto



## buffer overflow 0

### Descripción <a href="#descripcin" id="descripcin"></a>

Se nos provee un binario, su código fuente en C y un servidor al que conectarse por `nc`. El objetivo es obtener la flag provocando un crash controlado en el programa.&#x20;

nota en si el binario que se nos da es el programa en si ejecutado localmente , por lo cual si queremos "practicar" explotando esa vulnerabilidad tendriamos que crear un archivo llamado flag.txt , lo dice directamente en el codigo fuente , para posteriormente realizarlo en el servidor por nc

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

### Análisis del código fuente <a href="#anlisis-del-cdigo-fuente" id="anlisis-del-cdigo-fuente"></a>

Al leer el `.c` identificamos dos vulnerabilidades:

```c
cchar buf1[100];
gets(buf1);        // acepta input sin límite ← VULNERABLE

void vuln(char *input){
  char buf2[16];
  strcpy(buf2, input);  // copia sin verificar tamaño ← VULNERABLE
}
```

`gets()` no limita el input y `strcpy()` lo copia en un buffer de solo **16 bytes**. Si mandamos más de 16 caracteres, los bytes extra desbordan la memoria adyacente provocando un **Buffer Overflow**.

### El truco del SIGSEGV <a href="#el-truco-del-sigsegv" id="el-truco-del-sigsegv"></a>

El programa tiene registrado un handler especial:

```c
cvoid sigsegv_handler(int sig) {
  printf("%s\n", flag);  // imprime la flag
}
signal(SIGSEGV, sigsegv_handler);
```

`SIGSEGV` es la señal que lanza el sistema operativo cuando un programa accede a memoria inválida (crash). El programa está diseñado para **imprimir la flag justo cuando crashea**.

### Flujo del exploit <a href="#flujo-del-exploit" id="flujo-del-exploit"></a>

```
Input enorme → buf2[16] se desborda → memoria inválida → SIGSEGV → flag impresa
```

aqui hay una pequeña forma de explotarlo , simplemente nos conectamos al servidor con los datos que se nos da , y dentro del servidor se nos mostrara un texto de input: donde debemos de colocar mas de 16 caracteres para desbordarlo y optener la flag , peeeero como queremos ahorrarnos ese tiempo digamos , o para tenerlo automatizado aparte que se ve mas pro , podriamos crear un exploit en python que haga eso por nosotros

### Exploit en Python <a href="#exploit-en-python" id="exploit-en-python"></a>

En vez de escribir caracteres a mano, automatizamos con sockets:

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

### Lección aprendida <a href="#leccin-aprendida" id="leccin-aprendida"></a>

`gets()` y `strcpy()` son funciones peligrosas en C porque no verifican el tamaño del input. Nunca deben usarse en código real — existen alternativas seguras como `fgets()` y `strncpy()`.





vale con esto ya abriamos terminado la lista de principiantes en pycogym ,  en este playlist , hemos tocado retos de cada categoria que hay en pycogym , con estos retos ya podriamos profundicar en alguna categoria o reto que no haya gustado y profuncisarlo mas , dentro de la plataforma habra mucho mas reto con mas niveles de dificultad para aprender . no olvides siempre divertite hackeando Happy H4ck1ng

spoonki .. siempre hackeando nunca webiando<br>
