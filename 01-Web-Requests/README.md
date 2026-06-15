# 🌐 Web Requests

![HTB](https://img.shields.io/badge/Hack%20The%20Box-Academy-9FEF00?style=for-the-badge\&logo=hackthebox\&logoColor=black)
![HTTP](https://img.shields.io/badge/HTTP-Web%20Requests-blue?style=for-the-badge)
![cURL](https://img.shields.io/badge/cURL-Command%20Line-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow?style=for-the-badge)

---

## 📌 Descripción

Este módulo contiene notas del tema **Web Requests** de Hack The Box Academy.

El objetivo es entender cómo funciona la comunicación entre un cliente y un servidor web mediante **HTTP/HTTPS**, analizar peticiones web y utilizar herramientas como **cURL** y **Browser DevTools** para interactuar con páginas, formularios, cookies y APIs.

---

## 🎯 Objetivo del módulo

Comprender los fundamentos de las peticiones web para poder analizar aplicaciones desde una perspectiva de pentesting web.

Al finalizar este módulo, se debe entender:

* Cómo funciona HTTP y HTTPS.
* Cómo se estructura una URL.
* Qué son las requests y responses.
* Cómo funcionan los métodos HTTP.
* Cómo interpretar códigos de estado.
* Cómo manejar headers, cookies y JSON.
* Cómo interactuar con APIs.
* Cómo repetir peticiones usando `curl`.
* Cómo analizar tráfico desde DevTools.

---

## 🧠 Conceptos clave

### 🔹 HTTP

HTTP es el protocolo que permite que un cliente, como el navegador o `curl`, se comunique con un servidor web.

```text
Cliente → HTTP Request → Servidor
Cliente ← HTTP Response ← Servidor
```

Ejemplo:

```text
El navegador pide una página.
El servidor responde con HTML, JSON, imágenes o algún error.
```

---

### 🔹 HTTPS

HTTPS es la versión segura de HTTP. Usa cifrado mediante TLS/SSL para proteger datos sensibles como credenciales, cookies y formularios.

| Protocolo | Descripción              | Puerto |
| --------- | ------------------------ | ------ |
| HTTP      | Comunicación sin cifrado | 80     |
| HTTPS     | Comunicación cifrada     | 443    |

> HTTPS protege los datos en tránsito, pero no significa que una aplicación sea segura por completo.

---

## 🔗 Estructura de una URL

Ejemplo:

```text
http://admin:password@inlanefreight.com:80/dashboard.php?login=true#status
```

| Parte        | Ejemplo             | Significado                 |
| ------------ | ------------------- | --------------------------- |
| Scheme       | `http://`           | Protocolo usado             |
| User Info    | `admin:password@`   | Credenciales opcionales     |
| Host         | `inlanefreight.com` | Dominio o IP                |
| Port         | `:80`               | Puerto del servicio         |
| Path         | `/dashboard.php`    | Recurso solicitado          |
| Query String | `?login=true`       | Parámetros enviados         |
| Fragment     | `#status`           | Sección dentro de la página |

---

## 📤 HTTP Request

Una **request** es la petición que envía el cliente al servidor.

Puede incluir:

* Método HTTP.
* Path.
* Headers.
* Cookies.
* Parámetros.
* Body.

Ejemplo:

```http
GET /search.php?search=london HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Cookie: PHPSESSID=abc123
```

---

## 📥 HTTP Response

Una **response** es la respuesta del servidor al cliente.

Puede incluir:

* Código de estado.
* Headers.
* Cookies.
* Body.

Ejemplo:

```http
HTTP/1.1 200 OK
Content-Type: text/html
Set-Cookie: PHPSESSID=abc123

<html>
  <h1>Hello</h1>
</html>
```

---

## 🧾 Métodos HTTP

| Método    | Uso principal                   |
| --------- | ------------------------------- |
| `GET`     | Leer información                |
| `POST`    | Enviar o crear información      |
| `PUT`     | Actualizar información completa |
| `PATCH`   | Actualizar información parcial  |
| `DELETE`  | Eliminar información            |
| `HEAD`    | Obtener solo headers            |
| `OPTIONS` | Ver métodos permitidos          |

---

## 🚦 Códigos HTTP comunes

| Código                      | Significado                |
| --------------------------- | -------------------------- |
| `200 OK`                    | Petición exitosa           |
| `301 / 302`                 | Redirección                |
| `400 Bad Request`           | Petición mal formada       |
| `401 Unauthorized`          | Falta autenticación        |
| `403 Forbidden`             | Acceso denegado            |
| `404 Not Found`             | Recurso no encontrado      |
| `500 Internal Server Error` | Error interno del servidor |

---

## 🧩 Headers importantes

| Header          | Uso                           |
| --------------- | ----------------------------- |
| `Host`          | Indica el dominio solicitado  |
| `User-Agent`    | Identifica el cliente         |
| `Cookie`        | Envía cookies al servidor     |
| `Set-Cookie`    | El servidor asigna una cookie |
| `Authorization` | Envía credenciales o tokens   |
| `Content-Type`  | Indica el formato del body    |
| `Location`      | Indica redirección            |

---

## ⚔️ GET vs POST

| Característica | GET                   | POST                          |
| -------------- | --------------------- | ----------------------------- |
| Datos          | Van en la URL         | Van en el body                |
| Uso común      | Consultas y búsquedas | Formularios, login y creación |
| Visibilidad    | Visible en URL        | No visible en URL             |
| Tamaño         | Más limitado          | Permite más datos             |

> POST no es automáticamente seguro. Para proteger datos sensibles se debe usar HTTPS.

---

## 🍪 Cookies

Las cookies permiten mantener sesiones.

El servidor puede responder con:

```http
Set-Cookie: PHPSESSID=abc123
```

Luego el cliente envía esa cookie al servidor:

```http
Cookie: PHPSESSID=abc123
```

Una cookie válida puede permitir que el servidor reconozca a un usuario autenticado.

---

## 🧱 JSON

JSON es un formato común para enviar datos en aplicaciones web y APIs.

```json
{
  "search": "london"
}
```

Cuando se envía JSON, normalmente se usa:

```http
Content-Type: application/json
```

---

## 🔄 APIs y CRUD

Una API permite interactuar con datos de una aplicación.

| Operación | Método HTTP   |
| --------- | ------------- |
| Create    | `POST`        |
| Read      | `GET`         |
| Update    | `PUT / PATCH` |
| Delete    | `DELETE`      |

Ejemplo de endpoint:

```text
/api.php/city/london
```

---

## 🛠️ Browser DevTools

DevTools permite ver lo que el navegador envía y recibe.

| Acción         | Atajo                      |
| -------------- | -------------------------- |
| Abrir DevTools | `F12` / `CTRL + SHIFT + I` |
| Network        | `CTRL + SHIFT + E`         |
| Console        | `CTRL + SHIFT + K`         |

La pestaña **Network** permite analizar:

* URLs solicitadas.
* Métodos HTTP.
* Status codes.
* Headers.
* Cookies.
* Body.
* Responses.

---

## 🧪 Flujo recomendado para analizar una web

```text
1. Abrir la web en el navegador.
2. Abrir DevTools.
3. Ir a Network.
4. Interactuar con la página.
5. Identificar requests importantes.
6. Copiar request como cURL.
7. Probarla desde terminal.
8. Modificar parámetros, headers o cookies.
9. Analizar la respuesta.
10. Documentar hallazgos y comandos.
```

---

## 📂 Archivos del módulo

```text
01-Web-Requests/
├── README.md
└── Commands.md
```

| Archivo       | Contenido                            |
| ------------- | ------------------------------------ |
| `README.md`   | Teoría resumida del módulo           |
| `Commands.md` | Comandos útiles y ejemplos prácticos |

---

## 📚 Referencias

* Hack The Box Academy - Web Requests
* Mozilla Developer Network
* OWASP Web Security Testing Guide
* RFC 7231

---

## 🧑‍💻 Autor

Repositorio personal de estudio para fortalecer habilidades en **Web Pentesting**, **HTTP**, **cURL**, **APIs** y análisis de tráfico web.
