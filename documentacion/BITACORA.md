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

- **¿Cumple?** Sí
- **Error encontrado y ajuste:** ninguno en la publicación. Pendiente: crear el tag `v1.0.0` sobre el commit publicado `a1c62ac` (*Merge pull request #1*) como punto de recuperación.
- **Resultado al repetir la prueba:** se repitió en dos navegadores distintos (el del integrante y uno sin sesión de GitHub) con el mismo resultado.

## B02 — Actualización

- **Qué queremos comprobar:** la versión 2 se publica mediante PR aprobado y el cambio se ve en la URL pública.
- **Versión y estado inicial:** v1.0.0 publicada (commit `a1c62ac`).
- **Pasos para repetirla:** [PROCEDIMIENTOS.md §3](PROCEDIMIENTOS.md).
- **Resultado esperado:** la URL muestra "Versión 2", la experiencia "Ruta de espacios verdes" y el pie "v2.0.0", con estilos.
- **Cómo se hizo:**
  1. **andrezg876-lang** (colaborador con permiso de actualización) copió `sitio_v2/index.html` en `docs/index.html` desde su fork. Commit `8c1a644` a las 11:24:31 a. m.
  2. Abrió el **PR #4 "mi version 2, andres"** a las 11:25:41 a. m.
  3. **thomasT-maker** (admin/revisor) lo **aprobó** a las 11:30:04 a. m. y hizo el **merge** a las 11:30:15 a. m. La regla `proteger-main` exigió esa aprobación.
  4. GitHub Pages volvió a publicar automáticamente al cambiar `main`.
- **Resultado observado (21/11/2026 ≈ 11:41 a. m.):** la URL pública muestra ✅ "Versión 2", ✅ la nueva experiencia "Ruta de espacios verdes", ✅ las dos experiencias anteriores y ✅ el título morado (`styles.css` responde HTTP 200). ❌ El pie **no** muestra "v2.0.0": se usó `sitio_v2/index.html` tal cual, sin la marca de versión que definió el equipo.
- **Inicio, fin y duración:** 11:24:31 a. m. (commit) → 11:30:15 a. m. (merge aprobado) → verificación en la URL ≈ 11:41 a. m. Del commit al merge: **≈ 6 min**, en su mayoría a la espera de la aprobación.
- **Evidencia:**

  ![B02: versión 2 publicada](evidencias/B02_v2_publicada.png)

- **¿Cumple?** Sí, para lo que exige la guía (la versión 2 se publicó y el cambio es visible). Queda un ajuste propio pendiente: la marca `v2.0.0` en el pie.
- **Error encontrado y ajuste:** falta `<br><small>v2.0.0</small>` antes de `</footer>` en `docs/index.html`. Se corrige con un PR pequeño y luego se crea el tag `v2.0.0` sobre ese merge.
- **Resultado al repetir la prueba:** *[completar después del ajuste]*
- **Nota:** el PR #6 (nota de prueba en el README, de juanpati913-sketch) también pasó por aprobación; generó otro despliegue a las 11:40:59 a. m. sin cambiar el sitio.

## B03 — Respaldo

- **Qué queremos comprobar:** existe una copia íntegra, fuera de GitHub, con ubicación, versión y archivos identificados.
- **Versión y estado inicial:** *[completar: versión respaldada]*
- **Pasos para repetirla:** [PROCEDIMIENTOS.md §2](PROCEDIMIENTOS.md).
- **Resultado esperado:** ZIP en Drive con `index.html`, `styles.css` y `manifest.json`.
- **Ruta del respaldo local:** *[completar: respaldos/AAAAMMDD_HHMMSS_…]*
- **Ubicación en Drive y quién tiene acceso:** *[completar]*
- **Resultado observado:** *[completar]*
- **Evidencia:** *[completar]*
- **¿Cumple?** *[completar]*

## B04 — Recuperación

- **Qué queremos comprobar:** después de un error publicado, se recupera la versión correcta y se mide el tiempo.
- **Versión y estado inicial:** *[completar: v2.0.0 publicada]*
- **Error provocado:** *[completar: p. ej. index.html reemplazado por "Catálogo incorrecto"]*
- **Pasos para repetirla:** [PROCEDIMIENTOS.md §4](PROCEDIMIENTOS.md).
- **Resultado esperado:** la URL vuelve a mostrar la versión del tag elegido, con estilos.
- **Método usado:** *[revert / restaurar desde tag / emergencia del admin]*
- **Hora de inicio (error visible en la URL):** *[completar]*
- **Hora de fin (versión correcta en la URL, ventana privada):** *[completar]*
- **Duración:** *[completar]*
- **Versión recuperada:** *[completar]*
- **Evidencia antes y después:** *[completar: evidencias/B04_error.png, evidencias/B04_recuperado.png]*
- **Pasos manuales y cuáles automatizaríamos:** *[completar]*
- **¿Cumple?** *[completar]*

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
