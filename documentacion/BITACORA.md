# Bitácora del equipo

Basada en `PLANTILLA_EVIDENCIAS.md` del paquete del reto. Los campos marcados con *[completar]* se llenan durante el encuentro 2. **No escribir contraseñas, tokens ni claves.** Las capturas se guardan en `documentacion/evidencias/`.

## Registro del equipo

- **Equipo:** *[completar]*
- **Integrantes y responsabilidades:** *[completar: nombre — usuario GitHub — rol (admin / revisor / actualiza / documenta / repite B06)]*
- **Fecha:** 21 de noviembre de 2026 (encuentro 2)
- **Modalidad:** nube (GitHub Pages)
- **Arquitectura elegida y motivo:** sitio estático publicado con GitHub Pages desde `/docs` de `main`, versionado con Git y tags, respaldo independiente en Google Drive. Motivos en el [README](../README.md) y el [esquema](ESQUEMA.md).
- **Ayudas utilizadas y cambios realizados:**
  - `scripts/herramientas.py` del paquete: se usa para generar respaldos con manifiesto SHA-256 y como plan B local. Git reemplaza a `actualizar` y `restaurar` en la nube.
  - **Cambio propio:** se agregó la marca `v1.0.0` en el pie de `docs/index.html` (se conserva el texto "Versión 1" del cuerpo, que pide la guía). `sitio_v1/` y `sitio_v2/` quedan intactos.
  - Los PDF y las guías del paquete no se publican en el repositorio; se guardan en Drive.
  - Se usó Claude (asistente de IA) para estructurar el repositorio y redactar la documentación; el equipo revisó y ejecutó los procedimientos.
- **Recursos, permisos y posibles costos:** ver [PERMISOS.md](PERMISOS.md) y [ESQUEMA.md](ESQUEMA.md). Costo del ejercicio: ninguno.

---

## B01 — Publicación

**Resumen:** la versión 1 quedó publicada en GitHub Pages desde la carpeta `/docs` de `main` a las 10:07 a. m. del 21/11/2026. La dirección pública abre y muestra "Versión 1", el pie "v1.0.0", el título en morado y las dos experiencias. Es una publicación en la **nube** (GitHub Pages), no local. El tag `v1.0.0` se creó el 25/11/2026 a las 4:31 p. m. sobre el commit `a1c62ac` (merge del PR #1).

- **Qué queremos comprobar:** el sitio abre en la dirección pública con la versión inicial y sus estilos.
- **Versión y estado inicial:** v1.0.0 en `docs/` de `main`; Pages recién activado.
- **Pasos para repetirla:** [PROCEDIMIENTOS.md §0 y §1](PROCEDIMIENTOS.md).
- **Resultado esperado:** la URL muestra "Versión 1", el pie "v1.0.0" y el título en morado, desde ventana privada y en un navegador distinto al de configuración.
- **Resultado observado:**
  1. **Verificación del equipo (navegador del integrante, 21/11/2026 ≈ 11:10 a. m.):** la URL pública abre y muestra ✅ "Versión 1", ✅ el pie "v1.0.0", ✅ el título "Ruta Local" en morado (los estilos cargan) y ✅ las dos experiencias: *Recorrido por las historias del barrio* y *Taller de oficios y memoria*.
  2. **Verificación complementaria sin sesión (10:30 a. m.):** desde un navegador sin sesión de GitHub, la URL responde HTTP 200 y `styles.css` responde HTTP 200. Encabezados: `Last-Modified` 10:07:09 a. m. (hora en que Pages publicó) y `Cache-Control: max-age=600` (caché de 10 minutos).
- **URL:** https://thomast-maker.github.io/Infra-Nube-Proyecto-Estud-IA/
- **Inicio, fin y duración:** Pages publicó a las 10:07 a. m.; verificaciones a las 10:30 a. m. y ≈ 11:10 a. m. del 21/11/2026.
- **Evidencia:**

  Captura del equipo, con la barra de direcciones visible:

  ![B01: versión 1 publicada, captura del equipo](evidencias/B01_v1_publicada.png)

  Verificación complementaria sin sesión, con una franja agregada que indica la URL, la hora y los encabezados HTTP:

  ![B01: verificación sin sesión](evidencias/B01_v1_verificacion_sin_sesion.png)

  Punto de recuperación `v1.0.0`, creado el 25/11/2026 a las 4:31 p. m. sobre `a1c62ac`:

  ![B01: release v1.0.0](evidencias/B01_tag_v1_release.png)

- **¿Cumple?** Sí
- **Error encontrado y ajuste:** en la publicación no hubo errores. Dos ajustes de documentación: (1) la captura del navegador integrado no mostraba la barra de direcciones, así que se agregó una franja con la URL y la hora; (2) el tag `v1.0.0`, que estaba pendiente, se creó el 25/11/2026 sobre el commit publicado `a1c62ac`.
- **Resultado al repetir la prueba:** se verificó dos veces, desde el navegador del equipo y desde un navegador sin sesión de GitHub, con el mismo resultado. **No la repitió todavía otro integrante siguiendo las instrucciones:** esa repetición corresponde a B06 y queda pendiente.

## B02 — Actualización

**Resumen:** la versión 2 se publicó por Pull Request. Andrés propuso el cambio en el PR #4, el admin lo aprobó a las 11:30 a. m. del 21/11/2026 y Pages lo publicó en 24 segundos. La dirección pública muestra "Versión 2" y la nueva experiencia *Ruta de espacios verdes*. El tag `v2.0.0` se creó el 25/11/2026 sobre el commit `2676ef1`. Después de esta prueba, el PR #8 (25/11) dejó `main` con el CSS dentro de `index.html`; ver "Error encontrado".

- **Qué queremos comprobar:** la versión 2 se publica por PR y el cambio se ve en la URL.
- **Quién la hizo:** `andrezg876-lang` propuso el cambio; `thomasT-maker` (admin) lo revisó, aprobó e hizo el merge.
- **Versión y estado inicial:** v1.0.0 publicada (commit `a1c62ac`). El respaldo B03 todavía no se había hecho al momento de actualizar.
- **Pasos realizados:**
  1. El integrante reemplazó `docs/index.html` por el contenido de `sitio_v2/index.html` y abrió el **[PR #4](https://github.com/thomasT-maker/Infra-Nube-Proyecto-Estud-IA/pull/4)** ("mi version 2, andres") desde su propia copia (*fork*) del repositorio. Cambió solo 1 archivo (`docs/index.html`); `styles.css` es igual en v1 y v2.
  2. El admin revisó el cambio y lo **aprobó**. La regla `proteger-main` exige 1 aprobación antes del merge.
  3. Merge a `main` (commit `2676ef1`) y despliegue automático de GitHub Pages.
  4. Verificación en el navegador sobre la URL pública.
- **Resultado esperado:** la URL muestra "Versión 2", "Ruta de espacios verdes" y el pie "v2.0.0"; existe el tag `v2.0.0`.
- **Resultado observado:** la URL pública muestra ✅ "Versión 2", ✅ la nueva experiencia **Ruta de espacios verdes** (3 experiencias en total) y ✅ el título en morado (los estilos cargan). ⚠️ El pie **no** muestra "v2.0.0", porque se copió `sitio_v2/index.html` tal cual, sin agregar la marca que sí tiene la v1.
- **Tiempos (21/11/2026, hora de Colombia):**

  | Momento | Hora |
  |---|---|
  | PR #4 creado | 11:25:41 |
  | Aprobación del admin | 11:30:04 |
  | Merge a `main` | 11:30:15 |
  | Pages: despliegue iniciado → terminado | 11:30:18 → 11:30:39 |
  | **Del PR al sitio actualizado** | **≈ 5 min** (de los cuales ~4 min 20 s fueron la espera de la aprobación y 24 s el merge y el despliegue) |

- **Evidencia:**

  Sitio publicado con la versión 2 (captura del equipo, barra de direcciones visible):

  ![B02: versión 2 publicada](evidencias/B02_v2_publicada.png)

  Punto de recuperación `v2.0.0`, creado el 25/11/2026 a las 4:43 p. m. (Colombia) por el admin sobre el commit `2676ef1`, el merge del PR #4:

  ![B02: release v2.0.0](evidencias/B02_tag_v2_release.png)

- **¿Cumple?** Sí. La versión 2 se publicó por PR con aprobación del admin, se ve en la URL pública y quedó marcada con el tag `v2.0.0`.
- **Observación y decisión:** el pie de la versión 2 **no** muestra la marca `v2.0.0`, porque se copió `sitio_v2/index.html` tal cual. Como la guía solo pide comprobar que aparece "Versión 2" y los tags no se pueden mover, se decidió **no** modificar el pie y etiquetar el commit que ya estaba publicado y verificado. Así el tag coincide exactamente con lo que muestra la captura. La versión del sitio se identifica por el tag y por el texto "Versión 2" del cuerpo.
- **Error encontrado y ajuste:**
  1. El pie de la versión 2 no dice `v2.0.0`, porque se copió `sitio_v2/index.html` sin esa marca. Se decidió no cambiarlo y etiquetar el commit ya verificado. La versión se identifica por el tag y por el texto "Versión 2".
  2. El tag `v2.0.0` se creó el 25/11/2026, después de la prueba, y no al momento del merge.
  3. **Observación posterior:** el PR #8 ("Volver a la version 1", 25/11/2026, 4:28 p. m.) reemplazó el contenido de `docs/index.html` por el CSS. El commit `2676ef1` y el tag `v2.0.0` no se ven afectados, pero `main` sí, y el sitio publicado muestra texto de código en lugar del catálogo. Pendiente: revertir el PR #8 antes de seguir con las demás pruebas.
- **Resultado al repetir la prueba:** no se ha repetido todavía. La repetición por otro integrante, siguiendo solo `PROCEDIMIENTOS.md`, corresponde a B06 y queda pendiente.

## B03 — Respaldo

**Resumen:** se creó un respaldo de la versión 2 publicada correctamente (tag `v2.0.0`, commit `2676ef1`). El respaldo se hizo el 26/11/2026 a las 11:49 a. m. (hora de Colombia), a partir del tag y no de `main`, porque `main` tenía el CSS dentro de `index.html` por el PR #8. Las huellas SHA-256 de la copia coinciden con las de los archivos del tag. Se comprimió en un ZIP y se subió a Google Drive.

- **Qué queremos comprobar:** existe una copia íntegra, fuera de GitHub, con ubicación, versión y archivos identificados.
- **Versión respaldada:** v2.0.0 (commit `2676ef1`, merge del PR #4).
- **Ruta del respaldo local:** `respaldos\20261126_114935_473619` (equipo del integrante, rama local `bitacora-b01`).
- **Archivos incluidos:**
  - `index.html`: SHA-256 `b6a32ff3f46af4730b7faa17661355ef57d13f337e618de6dd2bedd656ad1302`
  - `styles.css`: SHA-256 `436b588e09fcbcae2b86a737a64393a81c1f667abeb36e9ebfdd836cc32da022`
  - `manifest.json`: lista las dos huellas anteriores.
- **Ubicación en Drive:** archivo `respaldo_v2_20261126.zip`. Según la captura, está en la raíz de "Mi unidad", **no** dentro de la carpeta "Ruta Local - Respaldos (EstudIA)". *[pendiente: moverlo a esa carpeta]*
- **Quién tiene acceso:** solo la cuenta del admin. *[pendiente: compartir la carpeta con el equipo, sin enlace público]*
- **Resultado observado:** el `manifest.json` tiene las mismas huellas que los archivos del tag `v2.0.0`. Se comprobó con `sha256sum` y con `diff` (salida `IGUAL`).
- **Evidencia:**

  Terminal con el comando `respaldar` y el manifiesto:

  ![B03: terminal con respaldo y manifiesto](evidencias/B03_respaldo_v2_terminal.png)

  Drive con el ZIP subido:

  ![B03: ZIP en Google Drive](evidencias/B03_respaldo_v2_drive.png)

- **¿Cumple?** Sí, con dos pendientes: mover el ZIP a la carpeta compartida y compartir esa carpeta con el equipo.
- **Error encontrado y ajuste:**
  1. **Huellas que no coincidían.** Al principio, `trabajo/index.html` tenía la versión 1. El paso `preparar` copia la v1 y el paso de copiar desde el tag no se había ejecutado después. Ajuste: volver a copiar `index.html` desde `v2.0.0` y comprobar con `diff` hasta obtener `IGUAL`.
  2. **Riesgo evitado.** `main` estaba roto por el PR #8. Respaldar desde `main` habría guardado la versión incorrecta. Ajuste: respaldar desde el tag `v2.0.0`.
  3. **ZIP fuera de la carpeta.** El archivo quedó en la raíz de Drive. Ajuste pendiente: moverlo a la carpeta compartida.
- **Uso del tag en este respaldo:** un tag es una marca fija en un commit. `v2.0.0` apunta a `2676ef1`, la versión correcta. Por eso el respaldo se tomó de ahí y no de `main`, que cambia con cada merge.
- **Resultado al repetir la prueba:** pendiente. La repetición por otro integrante corresponde a B06.

## B04 — Recuperación

**Resumen:** se provocó un error publicado en `main` con el PR #10 ("B04: error simulado") y se recuperó con un *revert* (PR #11). La URL pública volvió a mostrar la versión 2 con sus estilos, idéntica al commit `2676ef1`. El error estuvo en línea unos 4 minutos, medidos entre los dos merges. La hora exacta en que el sitio mostró la versión correcta no quedó anotada en el momento; se toma del historial de commits (ver "Duración").

- **Qué queremos comprobar:** después de un error publicado, se recupera la versión correcta y se mide el tiempo.
- **Versión y estado inicial:** v2.0.0 publicada (tag `v2.0.0`, commit `2676ef1`), con "Versión 2" y los estilos morados.
- **Error provocado:** `docs/index.html` reemplazado por una página de prueba con el título "Catálogo incorrecto" y el texto "Versión de error para practicar la restauración." Se hizo desde la cuenta de pruebas (`tabordathomas-maker`) como PR #10, con el admin (`thomasT-maker`) como revisor.
- **Pasos para repetirla:** [PROCEDIMIENTOS.md §4](PROCEDIMIENTOS.md).
- **Resultado esperado:** la URL vuelve a mostrar la versión del tag elegido, con estilos.
- **Método usado:** *revert*. Se creó el PR #11 ("Revert 'B04: error simulado'") desde el PR #10 ya fusionado; el admin lo aprobó y lo fusionó. Los tags `v1.0.0` y `v2.0.0` no se tocaron.
- **Tiempos (commits en hora de Colombia, UTC-5):**

  | Momento | Hora | Commit |
  |---|---|---|
  | Error publicado (merge del PR #10) | 16:48:10 | `34b60a2` |
  | Revert publicado (merge del PR #11) | 16:52:05 | `10eeaa8` |

- **Hora de inicio (error visible en la URL):** ≈ 4:48 p. m. (merge del PR #10). En B02, Pages tardó 21 segundos en publicar, así que el error se vio poco después de ese merge.
- **Hora de fin (versión correcta en la URL, ventana privada):** ≈ 4:52 p. m. (merge del PR #11) más el tiempo de despliegue. *[pendiente: anotar la hora exacta del ✅ en la pestaña Actions de GitHub, porque no se midió en el momento.]*
- **Duración:** **≈ 4 minutos** (estimado a partir de los dos merges; el despliegue añade unos segundos). *[pendiente: confirmar con la hora del despliegue.]*
- **Versión recuperada:** v2 (commit `2676ef1`). Se comprobó que `docs/index.html` de `main` es idéntico al de ese commit y que `styles.css` también coincide.
- **Evidencia antes y después:**

  Error publicado, con la barra de direcciones visible:

  ![B04: error publicado](evidencias/B04_error.png)

  Versión recuperada tras el revert, con la barra de direcciones visible:

  ![B04: versión recuperada](evidencias/B04_recuperado.png)

- **Pasos manuales y cuáles automatizaríamos:**
  - *Manuales (hoy):* editar `index.html` en GitHub, abrir el PR, aprobarlo, fusionarlo, abrir el revert, aprobarlo, fusionarlo y comprobar la URL en ventana privada.
  - *Automatizables:* crear el revert desde el último tag válido con un comando o un workflow; comprobar después del despliegue que la URL responde 200 y contiene "Versión 2"; avisar al equipo si falla.
  - *No automatizable sin cambiar la configuración:* la aprobación. La regla `proteger-main` exige un aprobador distinto del autor, y no hay un *bypass* configurado para emergencias. Por eso el admin debe aprobar a mano; en esta prueba el admin aprobó y fusionó el revert en pocos minutos.
- **¿Cumple?** Sí, con dos observaciones: la hora de fin debe confirmarse en Actions y la duración es una estimación. El punto importante es que la versión correcta quedó publicada por un PR revisado y sin tocar el tag.
- **Error encontrado y ajuste:** ninguno en la recuperación. Se encontró un detalle: el PR #10 se creó desde la rama `main` de la cuenta de pruebas en lugar de una rama propia, y eso no afectó al resultado. Para B06 conviene usar una rama con nombre propio, como indica `PLAN_PRUEBAS.md`.
- **Resultado al repetir la prueba:** pendiente. La repetición por otro integrante corresponde a B06.

## B05 — Permisos

- **Qué queremos comprobar:** lectura, actualización y administración están separadas.
- **Pasos para repetirla:** [PERMISOS.md, "Cómo demostrarlo"](PERMISOS.md).
- **Resultado esperado:** sin sesión se ve el sitio y no se edita; un push directo a `main` y el borrado de un tag `v*` son rechazados; solo el admin ve la configuración.
- **Resultado observado:** *[completar]*
- **Evidencia (sin credenciales):** *[completar]*
- **¿Cumple?** *[completar]*
- **Limitación:** en repo personal no hay rol "solo lectura" dentro de GitHub; ver PERMISOS.md.

## B06 — Repetibilidad

- **Qué queremos comprobar:** otro integrante (que no sea el admin) repite la actualización o la recuperación solo con estas instrucciones.
- **Quién la repite:** *[completar]*
- **Procedimiento repetido:** *[actualización / recuperación]*
- **Resultado observado:** *[completar]*
- **Dudas que tuvo y qué se corrigió en la documentación:** *[completar]*
- **Inicio, fin y duración:** *[completar]*
- **¿Cumple?** *[completar]*

---

## Cierre

- **Qué funciona realmente:** *[completar]*
- **Qué quedó como propuesta o pendiente:** *[completar]*
- **Procedimiento para recrear y recuperar:** [PROCEDIMIENTOS.md](PROCEDIMIENTOS.md).
- **Limitaciones y cambios para el encuentro 3:** *[completar. Ideas: organización gratuita con roles Read/Write/Admin; automatizar el respaldo con GitHub Actions; verificación automática de la URL después de cada despliegue]*
