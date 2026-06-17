# 🌐 Web Applications Fundamentals

![HTB Academy](https://img.shields.io/badge/HTB%20Academy-Web%20Applications-9FEF00?style=for-the-badge\&logo=hackthebox\&logoColor=black)
![Web Security](https://img.shields.io/badge/Web%20Security-Fundamentals-blue?style=for-the-badge)
![OWASP](https://img.shields.io/badge/OWASP-Top%2010-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow?style=for-the-badge)

---

## 📌 Descripción

Este módulo introduce los fundamentos de las **aplicaciones web**, su arquitectura, componentes principales y riesgos de seguridad.
El objetivo es comprender cómo funciona una aplicación web desde el navegador hasta el servidor, para luego poder analizar vulnerabilidades como **XSS**, **CSRF**, **SQL Injection**, **File Upload**, **Broken Access Control**, **Sensitive Data Exposure** y otras fallas comunes en entornos reales y laboratorios de Hack The Box.

Una aplicación web no es solo una página visual. Es un sistema compuesto por:

* Frontend
* Backend
* Servidor web
* Base de datos
* APIs
* Frameworks
* Infraestructura
* Lógica de negocio
* Controles de autenticación y autorización

---

## 🧠 Idea principal

Una aplicación web funciona como un restaurante:

```text
Usuario / Navegador  →  Cliente que hace un pedido
Frontend             →  Menú, mostrador y diseño visible
Servidor web         →  Mesero que recibe y enruta pedidos
Backend              →  Cocina donde se procesa la lógica
Base de datos        →  Almacén donde se guardan datos
API                  →  Ventanilla ordenada para pedir información
```

Cuando un usuario visita una aplicación web, el navegador envía una petición al servidor.
El servidor procesa la solicitud, consulta datos si es necesario y devuelve una respuesta que el navegador interpreta y muestra.

---

## 🏗️ Aplicaciones web vs sitios web

### Sitio web tradicional

Un sitio web tradicional suele mostrar información estática.

```text
Usuario entra → Lee información → No hay mucha interacción
```

Ejemplos:

* Página informativa
* Blog simple
* Landing page estática

---

### Aplicación web

Una aplicación web permite interacción dinámica.

```text
Usuario entra → Inicia sesión → Busca → Compra → Comenta → Sube archivos → Modifica datos
```

Ejemplos:

* Gmail
* Amazon
* Google Docs
* Hack The Box
* Banca online
* Paneles administrativos

---

## 🖥️ Frontend vs Backend

## 🎨 Frontend

El **frontend** es la parte visible de la aplicación web. Se ejecuta en el navegador del usuario.

Incluye:

* HTML
* CSS
* JavaScript
* Botones
* Formularios
* Tablas
* Menús
* Animaciones
* Diseño UI/UX

```text
Frontend = lo que el usuario ve e interactúa
```

### Analogía

```text
Frontend = fachada y mostrador de una tienda
```

---

## ⚙️ Backend

El **backend** es la parte que se ejecuta en el servidor. Procesa la lógica real de la aplicación.

Incluye:

* Autenticación
* Autorización
* Lógica de negocio
* Conexión a base de datos
* Gestión de sesiones
* APIs
* Procesamiento de formularios
* Validaciones críticas

```text
Backend = lo que procesa, valida y decide
```

### Analogía

```text
Backend = cocina y administración de la tienda
```

---

## ⚠️ Regla importante

Nunca se debe confiar únicamente en el frontend.

El usuario puede modificar:

* Requests
* Parámetros
* Cookies
* Headers
* JavaScript
* Validaciones del navegador

Por eso, la seguridad real debe implementarse en el **backend**.

---

## 🌳 HTML y DOM

## HTML

HTML define la estructura de una página web.

Ejemplo básico:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
  </head>
  <body>
    <h1>A Heading</h1>
    <p>A Paragraph</p>
  </body>
</html>
```

HTML funciona como el esqueleto de la página.

```text
HTML       = estructura
CSS        = diseño visual
JavaScript = comportamiento e interacción
```

---

## DOM

DOM significa **Document Object Model**.

Es la representación en forma de árbol que el navegador crea a partir del HTML.

```text
document
└── html
    ├── head
    │   └── title
    └── body
        ├── h1
        └── p
```

El DOM permite que JavaScript modifique la página en tiempo real.

Por ejemplo:

* Cambiar texto
* Agregar elementos
* Eliminar nodos
* Modificar estilos
* Leer o modificar contenido
* Insertar nuevos formularios

### Importancia en seguridad

Si una aplicación inserta datos controlados por el usuario directamente en el DOM sin sanitización, puede aparecer una vulnerabilidad como **DOM XSS**.

---

## 🔐 URL Encoding

La codificación URL, también llamada **percent encoding**, convierte caracteres especiales en un formato seguro para URLs.

Algunos caracteres tienen significado especial dentro de una URL, por ejemplo:

| Carácter | Codificación |
| -------- | ------------ |
| espacio  | `%20`        |
| `!`      | `%21`        |
| `"`      | `%22`        |
| `#`      | `%23`        |
| `$`      | `%24`        |
| `%`      | `%25`        |
| `&`      | `%26`        |
| `'`      | `%27`        |
| `(`      | `%28`        |
| `)`      | `%29`        |

Ejemplo:

```text
hola mundo → hola%20mundo
```

### ¿Por qué importa?

En pruebas web, muchos payloads, parámetros o caracteres especiales pueden romperse si no están codificados correctamente.

---

## 🧱 Arquitectura de aplicaciones web

Las aplicaciones web pueden organizarse de diferentes formas.

---

## Cliente - Servidor

Modelo básico de la web:

```text
Cliente → Request HTTP → Servidor
Cliente ← Response HTTP ← Servidor
```

El navegador pide recursos y el servidor responde con HTML, JSON, archivos o errores.

---

## Un solo servidor

Toda la aplicación se ejecuta en un único servidor:

```text
Servidor web
Aplicación
Base de datos
Archivos
Servicios
```

### Ventajas

* Fácil de implementar
* Menor costo
* Arquitectura simple

### Desventajas

* Si el servidor cae, cae todo
* Si se compromete el servidor, se compromete todo
* No hay buena segmentación

```text
All eggs in one basket
```

---

## Muchos servidores - Una base de datos

Varios servidores web comparten una sola base de datos.

```text
Servidor Web 1 ┐
Servidor Web 2 ├── Base de Datos
Servidor Web 3 ┘
```

### Ventajas

* Mejor disponibilidad
* Permite balanceo de carga
* La base de datos está separada
* Si cae un servidor web, otros pueden seguir funcionando

---

## Muchos servidores - Muchas bases de datos

Cada aplicación o servicio puede tener su propia base de datos.

```text
App 1 → DB 1
App 2 → DB 2
App 3 → DB 3
```

### Ventajas

* Mejor segmentación
* Mejor aislamiento
* Mayor resiliencia
* Menor impacto si un componente se compromete

### Desventaja

* Mayor complejidad
* Más administración
* Requiere mejor diseño de infraestructura

---

## 🧩 Arquitectura de tres capas

Una arquitectura web común se divide en tres capas:

| Capa               | Función                                     |
| ------------------ | ------------------------------------------- |
| Presentation Layer | Interfaz visible: HTML, CSS, JavaScript     |
| Application Layer  | Lógica, autorización, validaciones y reglas |
| Data Layer         | Base de datos y almacenamiento              |

```text
Usuario → Presentación → Aplicación → Datos
```

---

## 🧬 Microservicios

Los microservicios dividen una aplicación en servicios pequeños e independientes.

Ejemplo en una tienda online:

* Registro
* Búsqueda
* Pagos
* Reseñas
* Inventario
* Notificaciones

### Ventajas

* Escalabilidad
* Despliegue más rápido
* Código reutilizable
* Menor acoplamiento
* Mayor resiliencia

### Riesgos

* Más APIs expuestas
* Mayor complejidad
* Más puntos de autenticación
* Más superficie de ataque

---

## ☁️ Serverless

Serverless no significa que no existan servidores.
Significa que el proveedor cloud administra la infraestructura.

Ejemplos:

* AWS Lambda
* Azure Functions
* Google Cloud Functions

### Ventajas

* Escalado automático
* Menos administración
* Pago por uso
* Despliegue rápido

### Riesgos

* Permisos excesivos
* Mala configuración cloud
* Secretos expuestos
* Falta de logs
* Dependencia del proveedor

---

## 🖧 Servidores web

Un **servidor web** es el software que recibe peticiones HTTP/HTTPS y responde o las enruta hacia la aplicación.

Ejemplos:

* Apache
* NGINX
* IIS
* Apache Tomcat
* Node.js

Puertos comunes:

| Puerto | Protocolo |
| ------ | --------- |
| 80     | HTTP      |
| 443    | HTTPS     |

---

## ¿Qué hace un servidor web?

* Recibe requests
* Procesa rutas
* Entrega archivos estáticos
* Redirige peticiones al backend
* Devuelve códigos HTTP
* Maneja headers
* Puede funcionar como reverse proxy
* Puede balancear carga
* Puede aplicar reglas de seguridad

---

## Apache

Apache es uno de los servidores web más comunes, especialmente en entornos PHP.

Stack típico:

```text
LAMP = Linux + Apache + MySQL + PHP
```

### Características

* Muy documentado
* Modular
* Compatible con muchas tecnologías
* Usado en muchos entornos pequeños y medianos

---

## NGINX

NGINX es muy usado en aplicaciones de alto tráfico.

### Características

* Rápido
* Ligero
* Buen manejo de conexiones simultáneas
* Muy usado como reverse proxy
* Muy usado para balanceo de carga

```text
NGINX = recepcionista rápido que puede atender miles de solicitudes
```

---

## IIS

IIS es el servidor web de Microsoft.

Suele aparecer en entornos empresariales con:

* Windows Server
* Active Directory
* .NET
* SQL Server
* Windows Authentication

---

## 🚦 Códigos HTTP comunes

| Código                    | Significado                            |
| ------------------------- | -------------------------------------- |
| 200 OK                    | Petición exitosa                       |
| 301 / 302                 | Redirección                            |
| 400 Bad Request           | Petición mal formada                   |
| 401 Unauthorized          | Falta autenticación                    |
| 403 Forbidden             | Acceso denegado                        |
| 404 Not Found             | Recurso no encontrado                  |
| 405 Method Not Allowed    | Método HTTP no permitido               |
| 500 Internal Server Error | Error interno del servidor             |
| 502 Bad Gateway           | Respuesta inválida desde otro servidor |
| 504 Gateway Timeout       | Tiempo de espera agotado               |

---

## 🗄️ Bases de datos

Las aplicaciones web usan bases de datos para almacenar información como:

* Usuarios
* Contraseñas hasheadas
* Productos
* Posts
* Comentarios
* Pedidos
* Roles
* Permisos
* Tokens
* Configuraciones

---

## Bases de datos relacionales SQL

Usan tablas, filas y columnas.

Ejemplo:

```text
users
id | username | first_name | last_name
1  | fab      | Fabrisio   | Belahonia
```

Otra tabla:

```text
posts
id | user_id | date       | content
1  | 1       | 2026-01-01 | Hola mundo
```

Relación:

```text
users.id = posts.user_id
```

Ejemplos de bases SQL:

* MySQL
* PostgreSQL
* MSSQL
* Oracle
* SQLite
* MariaDB

---

## Bases de datos NoSQL

No usan tablas rígidas. Son más flexibles.

Modelos comunes:

* Key-Value
* Document-Based
* Wide-Column
* Graph

Ejemplo tipo JSON:

```json
{
  "100001": {
    "date": "01-01-2021",
    "content": "Welcome to this web application."
  },
  "100002": {
    "date": "02-01-2021",
    "content": "This is the first post."
  }
}
```

Ejemplos NoSQL:

* MongoDB
* ElasticSearch
* Redis
* Cassandra
* Neo4j
* DynamoDB

---

## 🛠️ Frameworks de desarrollo

Un framework ayuda a construir aplicaciones web de forma más rápida y estructurada.

Ejemplos:

| Framework | Lenguaje |
| --------- | -------- |
| Laravel   | PHP      |
| Express   | Node.js  |
| Django    | Python   |
| Rails     | Ruby     |
| ASP.NET   | C#       |
| Spring    | Java     |
| FastAPI   | Python   |

Un framework puede ayudar con:

* Rutas
* Controladores
* Sesiones
* Templates
* Autenticación
* APIs
* Conexión a base de datos

> Usar un framework no hace que una aplicación sea automáticamente segura. Depende de cómo se implemente.

---

## 🔌 APIs

Una API permite que el frontend se comunique con el backend.

```text
Frontend → API → Backend → Base de datos
```

Ejemplo:

```text
GET /api/users/5/posts
```

El backend procesa la solicitud, consulta los datos y devuelve una respuesta, normalmente en JSON.

---

## Query Parameters

Los parámetros pueden enviarse en la URL.

```text
/search.php?item=apples
```

Aquí:

```text
item = apples
```

Se usan para:

* Búsquedas
* Filtros
* Paginación
* Ordenamiento

---

## REST APIs

REST usa rutas y métodos HTTP.

| Método | Acción                        |
| ------ | ----------------------------- |
| GET    | Leer datos                    |
| POST   | Crear datos                   |
| PUT    | Actualizar o reemplazar datos |
| DELETE | Eliminar datos                |

Ejemplo:

```text
GET    /users
GET    /users/1
POST   /users
PUT    /users/1
DELETE /users/1
```

---

## SOAP APIs

SOAP usa XML para enviar y recibir datos.

Es más estructurado y pesado que REST.
Suele encontrarse en sistemas empresariales, banca o integraciones antiguas.

---

# 🔥 Vulnerabilidades comunes

---

## Sensitive Data Exposure

Ocurre cuando información sensible queda expuesta al usuario.

Puede aparecer en:

* Código fuente HTML
* Comentarios
* Archivos JavaScript
* Rutas ocultas
* Parámetros de debug
* Tokens
* Credenciales de prueba
* Hashes
* Correos o IDs internos

Ejemplo:

```html
<!-- TODO: remove test credentials test:test -->
```

### Prevención

* No dejar comentarios sensibles
* No exponer tokens en frontend
* No guardar secretos en JavaScript
* Revisar código antes de producción
* Clasificar información sensible

---

## HTML Injection

Ocurre cuando una aplicación muestra input del usuario como HTML sin filtrarlo.

```text
Usuario escribe HTML → La página lo interpreta como parte del documento
```

Impactos:

* Modificar apariencia
* Insertar formularios falsos
* Engañar usuarios
* Hacer defacement
* Preparar ataques XSS

---

## Cross-Site Scripting - XSS

XSS permite ejecutar JavaScript en el navegador de otra persona.

```text
HTML Injection = insertar estructura HTML
XSS            = ejecutar JavaScript
```

Tipos principales:

| Tipo          | Descripción                                                         |
| ------------- | ------------------------------------------------------------------- |
| Reflected XSS | La entrada se refleja inmediatamente en la respuesta                |
| Stored XSS    | La entrada queda guardada y afecta a otros usuarios                 |
| DOM XSS       | El problema ocurre directamente en el navegador al modificar el DOM |

Impactos:

* Robo de información visible
* Manipulación del DOM
* Redirecciones maliciosas
* Acciones en nombre del usuario
* Formularios falsos
* Toma de cuentas en ciertos escenarios

---

## CSRF

CSRF significa **Cross-Site Request Forgery**.

Permite que un atacante fuerce al navegador de una víctima autenticada a enviar una acción no deseada.

```text
Usuario autenticado + petición forzada = acción ejecutada con su sesión
```

Ejemplos de acciones afectadas:

* Cambiar correo
* Cambiar contraseña
* Crear usuarios
* Modificar configuración
* Realizar operaciones sensibles

### Defensas

* Anti-CSRF tokens
* SameSite cookies
* Reautenticación para acciones sensibles
* Validación de origen
* Buen diseño de sesiones

---

## Broken Authentication

Fallas que permiten saltar o abusar del proceso de autenticación.

Ejemplos:

* Login bypass
* Tokens débiles
* Sesiones mal gestionadas
* Contraseñas débiles
* Recuperación de contraseña insegura

---

## Broken Access Control

Ocurre cuando un usuario accede a recursos o funciones que no debería.

Ejemplo:

```text
/user/701/edit-profile
/user/702/edit-profile
```

Si un usuario cambia el ID y puede editar otro perfil, hay una falla de control de acceso.

---

## IDOR

IDOR significa **Insecure Direct Object Reference**.

Ocurre cuando se puede acceder a objetos ajenos modificando IDs o referencias.

```text
Ticket para casillero 701 → cambias a 702 → el sistema te deja entrar
```

Prevención:

* Verificar permisos en backend
* No confiar en IDs del cliente
* Aplicar control de acceso por objeto

---

## File Upload inseguro

Una funcionalidad de subida de archivos puede ser peligrosa si no valida bien.

Riesgos:

* Subida de scripts
* Doble extensión
* Webshells
* Sobrescritura de archivos
* Ejecución en servidor

Prevención:

* Validar extensión y contenido real
* Usar allowlist
* Guardar fuera del web root
* Renombrar archivos
* Bloquear ejecución
* Limitar tamaño

---

## Command Injection

Ocurre cuando la aplicación ejecuta comandos del sistema usando input del usuario sin validación.

Impactos:

* Ejecutar comandos
* Leer archivos
* Obtener acceso al sistema
* Comprometer el servidor

Prevención:

* Evitar ejecutar comandos del sistema
* Usar APIs seguras
* Validar input
* Usar allowlists
* Aplicar menor privilegio

---

## SQL Injection

Ocurre cuando el input del usuario se inserta inseguramente dentro de una consulta SQL.

Ejemplo vulnerable conceptual:

```php
$query = "select * from users where name like '%$searchInput%'";
```

Impactos:

* Saltar autenticación
* Leer datos sensibles
* Modificar información
* Borrar datos
* Extraer usuarios
* En ciertos casos, comprometer el servidor

Prevención:

* Prepared statements
* Consultas parametrizadas
* Validación de entrada
* Menor privilegio en la base de datos
* No mostrar errores SQL al usuario

---

# 🔐 Password Spraying

Password spraying es un ataque donde se prueba una misma contraseña común contra muchos usuarios.

## Brute force tradicional

```text
Usuario: fabrisio
Password1
Password2
Password3
Password4
```

Problema:

```text
La cuenta puede bloquearse rápido
```

---

## Password spraying

```text
fabrisio : Welcome2025
jgarcia  : Welcome2025
mlopez   : Welcome2025
admin    : Welcome2025
rrhh     : Welcome2025
```

Luego se espera y se prueba otra contraseña.

### Analogía

```text
Brute force = probar muchas llaves en una puerta
Password spraying = probar una llave común en muchas puertas
```

### Cadena de ataque común

```text
SQL Injection → Extraer usuarios → Password Spraying → Acceso a VPN/O365/Correo
```

### Defensas

* MFA
* Rate limiting
* Detección de patrones
* Contraseñas fuertes
* Bloqueo inteligente
* Alertas por intentos distribuidos
* Monitoreo de accesos anómalos

---

# 🧨 OWASP Top 10 relacionado

Vulnerabilidades base que aparecen constantemente en aplicaciones web:

| No. | Vulnerabilidad                             |
| --- | ------------------------------------------ |
| 1   | Broken Access Control                      |
| 2   | Cryptographic Failures                     |
| 3   | Injection                                  |
| 4   | Insecure Design                            |
| 5   | Security Misconfiguration                  |
| 6   | Vulnerable and Outdated Components         |
| 7   | Identification and Authentication Failures |
| 8   | Software and Data Integrity Failures       |
| 9   | Security Logging and Monitoring Failures   |
| 10  | Server-Side Request Forgery                |

---

# 🧾 Errores comunes de desarrollo

Errores frecuentes que pueden generar vulnerabilidades:

1. Permitir datos inválidos en la base de datos.
2. Confiar demasiado en el frontend.
3. Crear mecanismos de seguridad propios.
4. Dejar la seguridad para el final.
5. Guardar contraseñas en texto plano.
6. Permitir contraseñas débiles.
7. Guardar datos sensibles sin cifrar.
8. No validar rutas o parámetros.
9. Confiar demasiado en librerías de terceros.
10. Hardcodear credenciales o cuentas ocultas.
11. No prevenir SQL Injection.
12. Permitir inclusión remota de archivos.
13. Manejar datos sensibles de forma insegura.
14. Usar criptografía débil.
15. No registrar acciones importantes.
16. Configurar mal el WAF.
17. No aplicar control de acceso por rol.
18. Exponer errores internos.
19. No actualizar dependencias.
20. No monitorear actividad sospechosa.

---

# 🐞 Public Vulnerabilities, CVE y CVSS

Muchas aplicaciones usan software conocido:

* WordPress
* Joomla
* OpenCart
* Plugins
* CMS
* Frameworks
* Servidores web
* Librerías

Cuando se descubre una vulnerabilidad pública, puede recibir un identificador CVE.

```text
CVE = Common Vulnerabilities and Exposures
```

Como pentester, primero se identifica:

* Nombre del software
* Versión
* Plugins
* Framework
* Servidor web
* Tecnologías usadas

Luego se buscan vulnerabilidades públicas en:

* NVD
* Exploit DB
* Rapid7
* GitHub
* Advisories oficiales

---

## CVSS

CVSS mide la severidad de una vulnerabilidad en una escala de 0 a 10.

| Severidad | Rango      |
| --------- | ---------- |
| None      | 0.0        |
| Low       | 0.1 - 3.9  |
| Medium    | 4.0 - 6.9  |
| High      | 7.0 - 8.9  |
| Critical  | 9.0 - 10.0 |

```text
CVSS = termómetro del riesgo
```

Una vulnerabilidad crítica suele ser:

* Explotable remotamente
* De baja complejidad
* Sin autenticación
* Con alto impacto en confidencialidad, integridad o disponibilidad

---

# 🧭 Metodología mental para analizar una aplicación web

Cuando se evalúa una aplicación web, conviene pensar en preguntas como:

```text
1. ¿Qué tecnologías usa?
2. ¿Qué servidor web parece tener?
3. ¿Hay rutas ocultas?
4. ¿Qué entradas acepta el usuario?
5. ¿Qué parámetros viajan por URL?
6. ¿Qué APIs existen?
7. ¿Cómo maneja autenticación?
8. ¿Cómo maneja autorización?
9. ¿Hay roles diferentes?
10. ¿Se expone información en el frontend?
11. ¿Hay comentarios o datos sensibles en el código fuente?
12. ¿Hay subida de archivos?
13. ¿Se puede modificar algún ID?
14. ¿Existen versiones vulnerables?
15. ¿Se pueden encadenar vulnerabilidades?
```

---

# 🔗 Ejemplo de cadena de ataque

Una sola vulnerabilidad puede no parecer crítica, pero al encadenarla con otras puede generar un impacto alto.

```text
1. Se revisa el código fuente.
2. Se encuentra una ruta oculta.
3. La ruta expone una versión vulnerable.
4. Se identifica un CVE público.
5. Se logra acceso inicial.
6. Se enumeran archivos internos.
7. Se encuentran credenciales.
8. Se accede a la base de datos.
9. Se extraen usuarios.
10. Se intenta password spraying contra un portal externo.
```

La mentalidad de pentesting no consiste solo en encontrar una falla aislada, sino en entender cómo una falla puede conectarse con otra.

---

# ✅ Puntos clave del módulo

* El frontend es visible y controlable por el usuario.
* El backend debe validar todo.
* El DOM representa la estructura viva de la página.
* URL encoding permite representar caracteres especiales en URLs.
* HTML Injection modifica la estructura de una página.
* XSS ejecuta JavaScript en el navegador.
* CSRF abusa de sesiones activas.
* SQL Injection manipula consultas SQL.
* File Upload inseguro puede comprometer servidores.
* Broken Access Control permite acceder a recursos indebidos.
* Password spraying prueba una contraseña común contra muchos usuarios.
* CVE y CVSS ayudan a identificar y priorizar vulnerabilidades públicas.
* La arquitectura influye directamente en el impacto de una vulnerabilidad.
* La seguridad debe aplicarse en todas las capas de la aplicación.

---

# 📚 Referencias

* Hack The Box Academy - Web Applications
* OWASP Top 10
* OWASP Web Security Testing Guide
* PortSwigger Web Security Academy
* NVD - National Vulnerability Database
* Exploit DB
* Rapid7 Vulnerability Database
