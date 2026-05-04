---
description: >-
  Cuarta sección de la playlist para principiantes de picoCTF.   ¡Ahora sí viene
  lo bueno! Pasamos a programación en Python y cracking.
---

# 🐍  seccion 4 (python)

{% hint style="info" %}
_**Bien, ¡ahora sí viene lo realmente bueno!**_ Pasamos a programación. Hasta este punto tendrías que tener nociones básicas de programación, al menos en el lenguaje de entrada más fácil como lo es **Python**. Si no, pues un video de 8 horas de Python en YouTube es suficiente para entrenar la mente xd. 🧠🔥
{% endhint %}

***

## 🐍 Python Wrangling

<details>

<summary><strong>Dificultad:</strong> 🟡 Media</summary>

Este reto es de nivel medio, pero la primera vez que lo resolví no tenía mucha idea de cómo abordarlo. Con la práctica todo va tomando forma — ¡al final es cuestión de repetición! 🛠️

### ❓ ¿Qué nos dice el reto?

Nos indica que los programas en Python se usan igual que cualquier comando en la terminal, lo que nos da la pista de que podemos **concatenar parámetros en una sola línea**.

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

### 📂 Archivos proporcionados

* 📄 `ende.py` — el programa principal
* 🔑 `password.txt` — la contraseña
* 🚩 `flag.txt.en` — la flag cifrada

### 🕵️‍♂️ Análisis

Lo primero es inspeccionar los archivos:

* `password.txt` → contiene una serie de números, que efectivamente es la **contraseña necesaria**.
* `flag.txt.en` → contenido cifrado en **Base64**, necesita el programa para descifrarse.

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

Si ejecutamos `ende.py` sin argumentos, el programa nos muestra su modo de uso:

```bash
python3 ende.py
```

<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

Nos indica que acepta dos flags:

* <kbd>-e</kbd> → encriptar 🔒
* <kbd>-d</kbd> → desencriptar 🔓

Como queremos descifrar la flag, usamos <kbd>-d</kbd>. El programa pedirá la contraseña, que copiamos directamente desde `password.txt`.

```bash
python3 ende.py -d flag.txt.en
```

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

Y listo — la flag aparece descifrada. ✅😎



</details>

***

## 🔐 PW Crack 1

<details>

<summary><strong>Dificultad:</strong> 🟢 Fácil</summary>

El reto nos pregunta si podemos crackear la contraseña para obtener la flag. Nos dan el programa Python que verifica la contraseña y la flag cifrada. Parece intimidante a primera vista... pero _neh_, no lo es. 😄

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

### 🕵️‍♂️ Análisis del código

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

Al leer el código encontramos la sección más relevante:

```python
flag_enc = open('level1.flag.txt.enc', 'rb').read()
```

Esta variable abre el archivo de la flag cifrada en modo lectura binaria (`rb`) y carga su contenido en memoria.

{% hint style="warning" %}
**¡Ojo!** Por eso ambos archivos deben estar estrictamente en el mismo directorio. 📂
{% endhint %}

Más abajo, el programa:

1. 🙋‍♂️ Pide al usuario que ingrese la contraseña.
2. 🔍 Verifica si coincide con la contraseña correcta.
3. 🎉 Si es correcta, descifra e imprime la flag.

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

### 🎯 El detalle clave

```python
if( user_pw == "1e1a"):
    print("Welcome back... your flag, user:")
```

La contraseña está **en texto plano dentro del código**. No se requiere fuerza bruta ni nada elaborado — solo leer el código con atención. 👀

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

**Contraseña:** `1e1a`

</details>

***

## 🔐 PW Crack 2

<details>

<summary><strong>Dificultad:</strong> 🟡 Fácil-Media</summary>

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

Misma mecánica que el anterior — necesitamos encontrar la contraseña para que el programa descifre la flag. Pero esta vez no está en texto plano.

### 🕵️‍♂️ Análisis del código

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

La sección de verificación ahora luce así:

```python
if( user_pw == chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65) ):
```

La función `chr()` convierte un valor numérico a su carácter Unicode equivalente. La contraseña se construye letra por letra usando valores hexadecimales — una forma simple de ofuscarla.

### 🧮 Conversión manual

Convertimos cada valor hexadecimal a decimal y buscamos su equivalente en la tabla ASCII:

| Hexadecimal 🔢 | Decimal 🧮 | ASCII 🅰️ |
| :------------: | :--------: | :-------: |
|     `0x33`     |     51     |  **`3`**  |
|     `0x39`     |     57     |  **`9`**  |
|     `0x63`     |     99     |  **`c`**  |
|     `0x65`     |     101    |  **`e`**  |

{% hint style="info" %}
Podemos hacerlo fácilmente y sin dolores de cabeza con [CyberChef](https://gchq.github.io/CyberChef/) 👨‍🍳 usando la operación _From Charcode_.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

**Contraseña:** `39ce`

</details>

***

## 🔐 PW Crack 3

<details>

<summary><strong>Dificultad:</strong> 🟡 Media</summary>

Aquí ya nos ensuciamos las manos y **escribimos nuestro propio código**. 🧑‍💻🔥

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

### 📜 El contexto

El reto nos dice que hay **7 posibles contraseñas** y debemos encontrar cuál es la correcta. El programa verifica la contraseña hasheándola y comparándola con un hash almacenado.

### 🕵️‍♂️ Análisis del código

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

Dentro de la función `level_3_pw_check()`:

```python
user_pw_hash = hash_pw(user_pw)

if( user_pw_hash == correct_pw_hash ):
    # descifra e imprime la flag
```

El programa hashea el input del usuario y lo compara con el hash correcto. Si coinciden, descifra la flag.

### 🛠️ La solución

En vez de probar las 7 contraseñas a mano, automatizamos con un bucle `for`:

```python
for p in pos_pw_list:
    h_encryp = hash_pw(p)
    if h_encryp == correct_pw_hash:
        decryption = str_xor(flag_enc.decode(), p)
        print(decryption)
```

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

El bucle itera la lista, hashea cada contraseña y la compara. Cuando hay coincidencia, descifra e imprime la flag directamente — sin tocar `level_3_pw_check()` para nada. 🎯🍽️

</details>

***

## 🔐 PW Crack 4

<details>

<summary><strong>Dificultad:</strong> 🟡 Media-facil??</summary>

Mismo concepto que el reto anterior, solo que ahora hay **100 posibles contraseñas** en vez de 7. 💀

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Suena más difícil... pero en realidad es súper fácil. El código del programa es prácticamente idéntico. La lista es más larga, pero el exploit es exactamente el mismo&#x20;

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

— copiamos el bucle del reto anterior y listo. 😄♻️ ¡Reutilizar código es de sabios!

```python
for p in pos_pw_list:
    h_encryp = hash_pw(p)
    if h_encryp == correct_pw_hash:
        decryption = str_xor(flag_enc.decode(), p)
        print(decryption)
```

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

</details>

***

## 🔐 PW Crack 5

<details>

<summary><strong>Dificultad:</strong> 🔴 Media-Alta</summary>

Este reto añade un giro: las posibles contraseñas ya no están dentro del código del programa, sino en un archivo externo llamado `dictionary.txt`. 📖

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

### 🕵️‍♂️ Análisis

El código del programa es el mismo de siempre — la diferencia es de dónde vienen las contraseñas a probar.

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

### 🛠️ La solución

Necesitamos leer `dictionary.txt` línea por línea, hashear cada entrada y compararla. Aquí está el script matador:

```python
with open('dictionary.txt', 'r') as archivo:
    for p in archivo:
        h_encryp = hash_pw(p.strip())
        if h_encryp == correct_pw_hash:
            decryption = str_xor(flag_enc.decode(), p.strip())
            print(decryption)
```

### 🧠 ¿Por qué `with` y `.strip()`?

{% hint style="info" %}
**Desglosando la magia:**

* 📂 **`with open(...)`** — garantiza que el archivo se cierre correctamente cuando terminemos, sin hacerlo manualmente. Python siendo responsable. 🧹
* ✂️ **`.strip()`** — cada línea del archivo viene con un `\n` al final (salto de línea). Si hasheamos `"contraseña\n"` en vez de `"contraseña"`, el hash nunca va a coincidir con nada. `.strip()` elimina esos caracteres invisibles molestos antes de procesar. ✨
{% endhint %}

{% hint style="warning" %}
**Ojo:** hay que usar `p.strip()` **tanto** al hashear como al descifrar. Si usas `p` sin strip en el `str_xor()`, la contraseña lleva el `\n` pegado y la flag aparece corrupta aunque la contraseña sea la correcta. 😬 _(Me pasó, por eso aviso xd)_.
{% endhint %}



</details>

***

_Writeup by spoonki 🖤_
