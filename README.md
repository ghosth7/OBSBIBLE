# OBSBible

**Software gratuito y de código abierto para proyectar la Biblia y canciones en iglesias, integrado con OBS Studio.**

Una alternativa moderna, ligera y rápida a HolyLyrics, FreeShow y EasyWorship. Funciona como *Browser Source* de OBS: sin capturar ventanas, con fondo transparente y cambios instantáneos.

![Licencia MIT](https://img.shields.io/badge/licencia-MIT-green)
![Plataforma](https://img.shields.io/badge/plataforma-Windows%2064--bit-blue)
![Gratis](https://img.shields.io/badge/precio-gratis-brightgreen)

---

## Características

- **Biblia:** búsqueda por referencia (`Juan 3:16`, `Romanos 8`) y por texto, favoritos, historial y múltiples versiones.
- **Canciones:** agregar, editar y eliminar; importar desde TXT y OpenLyrics; categorías, autores y tonos.
- **Integración con OBS:** fondo transparente, transiciones (fade, slide, zoom) y cambios en tiempo real vía WebSockets.
- **Diseño:** editor de temas con fuentes de Google Fonts, colores, contorno, sombra, caja, bordes, posición y más.
- **Operador:** vista previa en vivo, cola de presentación con arrastrar y soltar, y botones Anterior/Siguiente.
- **Ajuste automático de texto:** los versículos largos se reducen y se distribuyen para caber siempre en pantalla.
- **Control remoto:** manéjalo desde tu celular u otra PC en la misma red.
- **API REST** para automatización externa.

---

## Descarga

Ve a la sección **[Releases](../../releases)** y descarga la última versión para Windows:

| Archivo | Descripción |
|---|---|
| `OBSBible-x.x.x.exe` | Versión portable: un solo archivo, no requiere instalación. |
| `OBSBible-win-unpacked.zip` | Carpeta completa descomprimida (abre más rápido y es la mejor alternativa si Windows bloquea el `.exe`). |

No necesitas instalar Node.js, npm ni ninguna dependencia: todo viene incluido.

**Requisitos:** Windows 10 u 11 de 64 bits y OBS Studio.

---

## Uso normal

### 1. Abrir el programa

Ejecuta el `.exe` (o `OBSBible.exe` dentro de la carpeta descomprimida). Se abre el **Panel de Control** y el servidor local arranca automáticamente en el puerto `3000`.

> La primera vez, Windows puede pedir permiso de red (Firewall). Acepta para que OBS y tus dispositivos puedan conectarse.

### 2. Conectarlo a OBS Studio

1. En OBS, en el panel **Fuentes**, haz clic en **+** → **Navegador** (*Browser*).
2. En **URL** escribe:
   ```
   http://localhost:3000/output
   ```
3. Pon el ancho y alto de tu lienzo (por ejemplo `1920` x `1080`).
4. Acepta. No necesitas chroma key: el fondo es transparente.
5. Coloca esta fuente **encima** de tu cámara o escena.

### 3. Cargar una Biblia

OBSBible **no incluye el texto bíblico completo** de ninguna versión (por derechos de autor). Incluye solo una pequeña muestra para probar.

Para cargar una Biblia completa: **Ajustes → Importar Biblia completa (JSON)** y selecciona tu archivo con este formato:

```json
{
  "version": { "id": "rvr60", "name": "Reina-Valera 1960", "language": "es" },
  "verses": [
    { "book": "Juan", "chapter": 3, "verse": 16, "text": "Porque de tal manera amó Dios al mundo..." }
  ]
}
```

El campo `book` debe usar el nombre en español del libro (los acentos y las mayúsculas se ignoran).

> ⚠️ **Eres responsable de obtener el texto bíblico de una fuente que permita su uso.** Muchas versiones modernas (RVR1960, NTV, NVI, etc.) tienen derechos de autor. Las versiones de dominio público, como la Reina-Valera Antigua de 1909, no tienen ese problema.

### 4. Proyectar

1. Ve a la pestaña **Biblia** y escribe una referencia, por ejemplo `Juan 3:16-21`.
2. Haz clic en un versículo para mostrarlo en OBS, o usa **Siguiente ▶ / ◀ Anterior** para avanzar versículo por versículo.
3. Usa el botón **+** para agregar elementos a la **cola** y arrástralos para reordenarlos.
4. Usa **Ocultar** para quitar el texto de la pantalla.

### 5. Controlarlo desde el celular

En **Ajustes** copia la dirección de "Control remoto en la red local" (parecida a `http://192.168.x.x:3000/control`) y ábrela en el navegador de cualquier dispositivo conectado a la misma red WiFi.

---

## ⚠️ Aviso de seguridad de Windows: léelo antes de asustarte

Al abrir OBSBible, Windows puede mostrar un mensaje como:

- *"Windows protegió tu PC"* (SmartScreen), o
- *"El Control Inteligente de Aplicaciones bloqueó una aplicación que podría no ser segura"*.

### ¿Es un virus? **No.**

Estos avisos aparecen porque el programa **no tiene firma digital de un "editor verificado"**. Esa firma es un certificado de pago que cuesta cientos de dólares cada año, y OBSBible es un proyecto **gratuito y de código abierto** que no puede costear esa licencia.

Windows desconfía de **cualquier** programa nuevo sin firma, sin importar si es seguro o no. No significa que OBSBible contenga algo malicioso.

### ¿Cómo sé que es seguro?

- **Todo el código es público** en este repositorio: puedes leerlo, revisarlo y compilarlo tú mismo.
- No tiene publicidad, ni telemetría, ni cuentas. Funciona localmente en tu PC y no envía tus datos a ningún servidor.
- Puedes verificar que el archivo descargado es el mismo que publicamos comparando su huella SHA-256. En CMD:
  ```cmd
  certutil -hashfile "OBSBible.exe" SHA256
  ```
  Compara el resultado con el que aparece en la descripción de cada Release.
- Si quieres 100 % de tranquilidad, compílalo tú mismo (ver [Uso alternativo](#uso-alternativo-si-windows-lo-bloquea)).

### Si sale el aviso azul de SmartScreen

1. Haz clic en **Más información**.
2. Haz clic en **Ejecutar de todos modos**.

Solo hace falta la primera vez.

---

## Uso alternativo: si Windows lo bloquea

En algunos equipos con Windows 11, el **Control Inteligente de Aplicaciones** (*Smart App Control*) bloquea el `.exe` y **no ofrece un botón para saltarse el aviso**. En ese caso tienes tres alternativas, de la más recomendada a la menos:

### Opción A: usar la carpeta descomprimida

1. Descarga `OBSBible-win-unpacked.zip` de Releases y descomprímelo.
2. Abre `OBSBible.exe` desde esa carpeta.

Esta versión no empaqueta el programa en un solo archivo y es más probable que Windows la deje correr. No es garantía: depende de la configuración de seguridad de cada equipo.

### Opción B: ejecutarlo desde el código fuente (la más segura)

Requiere [Node.js](https://nodejs.org) (versión LTS). Como el programa lo ejecuta Electron y no un `.exe` nuevo sin firma, no se activa el bloqueo.

```bash
git clone https://github.com/TU_USUARIO/OBSBible.git
cd OBSBible
npm install
npm start
```

> Si `npm install` falla con errores de `node-gyp` o `better-sqlite3`, usa **Node.js 20 LTS**. Las versiones muy recientes de Node pueden no tener binarios precompilados para SQLite.

Para no usar la consola cada vez, crea un archivo `Iniciar_OBSBible.bat` con este contenido:

```bat
@echo off
cd /d "C:\RUTA\A\OBSBible"
npm start
pause
```

### Opción C: desactivar el Control Inteligente de Aplicaciones

1. Abre **Seguridad de Windows** → **Control de aplicaciones y navegador**.
2. Entra en **Configuración del Control Inteligente de Aplicaciones**.
3. Selecciona **Desactivado**.

> ⚠️ En muchas versiones de Windows 11 **no se puede volver a activar** sin reinstalar el sistema, y reduce la protección contra programas desconocidos. Úsala solo si entiendes el riesgo.

---

## Compilar el `.exe` tú mismo

```bash
npm install
npm run build:win
```

El resultado queda en la carpeta `dist/`. Si falla con errores de `winCodeSign` o enlaces simbólicos, ejecuta la consola como administrador o activa el **Modo de desarrollador** de Windows.

---

## Solución de problemas

| Problema | Solución |
|---|---|
| OBS no muestra nada | Verifica que OBSBible esté abierto y que la URL sea `http://localhost:3000/output`. Haz clic derecho en la fuente → *Actualizar caché de la página actual*. |
| El puerto 3000 está ocupado | Cierra otra copia de OBSBible que esté abierta. |
| No conecta desde el celular | Verifica que estén en la misma red WiFi y que el Firewall de Windows permita la conexión. |
| Texto cortado en OBS | Asegúrate de usar la última versión y que el Browser Source tenga el tamaño de tu lienzo. |
| La Biblia no aparece | Debes importarla desde **Ajustes**: el programa no incluye el texto completo. |

---

## Arquitectura

```
OBSBible/
├── main.js          # Proceso principal de Electron
├── preload.js       # Puente seguro Electron ↔ interfaz
├── server/          # Express + Socket.IO + SQLite + API REST
├── renderer/
│   ├── control/     # Panel del operador
│   └── output/      # Página que carga OBS como Browser Source
├── assets/  themes/  songs/  bibles/  plugins/
```

**Tecnologías:** Electron, Node.js, Express, Socket.IO, SQLite (better-sqlite3), HTML5, CSS3 y JavaScript vanilla.

---

## API REST y WebSocket

| Método | Ruta | Descripción |
|---|---|---|
| GET | `/api/bible/reference?ref=Juan 3:16&version=rvr60` | Buscar por referencia |
| GET | `/api/bible/search?q=amor&version=rvr60` | Buscar por texto |
| GET/POST/PUT/DELETE | `/api/songs` | Gestionar canciones |
| GET/POST/PUT/DELETE | `/api/themes` | Gestionar temas |
| GET | `/api/live/state` | Estado actual en pantalla |
| POST | `/api/live/show` · `/api/live/clear` | Mostrar u ocultar contenido |

Eventos de Socket.IO: `live:show`, `live:clear`, `live:update-theme` (cliente → servidor) y `live:state`, `connection:status` (servidor → clientes).

---

## Contribuir

¡Las contribuciones son bienvenidas! Abre un *issue* para reportar errores o proponer ideas, o envía un *pull request*.

```bash
npm run lint
```

Ayuda especialmente: más plantillas de diseño, atajos de teclado, soporte para Mac/Linux y traducciones.

---

## Licencia

Distribuido bajo licencia **MIT**. Consulta el archivo [LICENSE](LICENSE).

El texto bíblico y las canciones que cargues son responsabilidad tuya y están sujetos a sus propias licencias.
