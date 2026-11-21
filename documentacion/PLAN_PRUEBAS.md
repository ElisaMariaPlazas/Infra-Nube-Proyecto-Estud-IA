# Plan de pruebas por Pull Request

**Regla del equipo:** cada prueba entra a `main` por un Pull Request (PR) que hace **un integrante** y que **aprueba y fusiona el admin** (`thomasT-maker`). Nadie escribe directo en `main`; la regla `proteger-main` lo impide.

> Los PR que abra el propio admin los aprueba otro integrante, porque GitHub no deja que el autor apruebe su propio PR.

## Reparto

| Orden | Prueba | Responsable | PR(s) que abre | Estado |
|---|---|---|---|---|
| 0 | Integrar bitácora y plan | `thomasT-maker` (lo aprueba un compañero) | 1 PR: rama `pruebas-b01-b06` | ⏳ |
| 1 | B01 Publicación | `thomasT-maker` | — (ya registrada) | ✅ |
| 2 | B02 Actualización | `andrezg876-lang` | PR #4 (ya fusionado) + 1 PR para corregir el pie `v2.0.0` | 🟡 |
| 3 | B03 Respaldo | `juanpati913-sketch` | 1 PR de evidencia | ⏳ |
| 4 | B04 Recuperación | `simoncs02` | 3 PR: error → revert → evidencia | ⏳ |
| 5 | B05 Permisos | `andrezg876-lang` | 1 PR de evidencia | ⏳ |
| 6 | B06 Repetibilidad | `juanpati913-sketch` | 3 PR: error → revert → evidencia | ⏳ |

Después del paso 2, el **admin** crea los tags `v1.0.0` (sobre *Merge pull request #1*) y `v2.0.0` (sobre el merge de la corrección del pie), en **Releases → Draft a new release**.

---

## Antes de empezar (cada integrante)

1. Aceptar la invitación de colaborador del repositorio (correo o https://github.com/notifications). Así se trabaja con ramas dentro del repo, sin *fork*.
2. Leer `documentacion/PROCEDIMIENTOS.md`.
3. Tomar las capturas con **Win+Shift+S**, con la **barra de direcciones visible**, y guardarlas con el nombre indicado.
4. **Nunca** incluir contraseñas, tokens ni capturas de credenciales.

## Cómo se hace un PR de evidencia (igual para todos)

1. Repo → `documentacion/evidencias` → **Add file → Upload files** → arrastrar las capturas.
2. Abajo, **Create a new branch** con el nombre `prueba-bXX-usuario` → **Propose changes**. *No crear todavía el PR.*
3. En esa misma rama, abrir `documentacion/BITACORA.md` → lápiz ✏️ → **editar solo la sección de su prueba**: llenar los `[completar]` y pegar las imágenes así:
   ```
   ![B03: respaldo de la versión 2](evidencias/B03_respaldo_v2.png)
   ```
   **Commit directly to the `prueba-bXX-usuario` branch.**
4. **Compare & pull request** → título `BXX: <qué se hizo>` → en *Reviewers* elegir `thomasT-maker` → **Create pull request**.
5. Si GitHub dice *"This branch has conflicts"* (porque otro PR de bitácora entró antes), clic en **Resolve conflicts**, dejar ambas secciones y **Mark as resolved**.

---

## Paso 0 — Integrar la bitácora y este plan

- **Admin:** abre el PR de la rama `pruebas-b01-b06` hacia `main`.
- **Cualquier compañero:** **Files changed → Review changes → Approve**.
- **Admin:** **Merge**. A partir de aquí todos editan la bitácora que está en `main`.

## Paso 2 — B02: corregir el pie (`andrezg876-lang`)

1. Rama `prueba-b02-pie`: editar `docs/index.html` y agregar `<br><small>v2.0.0</small>` justo antes de `</footer>`.
2. En la misma rama, completar en la bitácora B02 el *Resultado al repetir la prueba* y cambiar la observación del pie a corregida.
3. PR → admin aprueba y fusiona → verificar en ventana privada que el pie dice `v2.0.0`.
4. Captura → `B02_v2_pie_corregido.png` (subirla en el mismo PR o en uno nuevo).

## Paso 3 — B03: respaldo de la versión 2 (`juanpati913-sketch`)

1. En su computador, dentro del repo clonado:
   ```
   git checkout main
   git pull
   python scripts/herramientas.py preparar
   copy docs\index.html trabajo\
   copy docs\styles.css trabajo\
   python scripts/herramientas.py respaldar
   type respaldos\NOMBRE_QUE_IMPRIMIÓ\manifest.json
   ```
2. Comprimir la carpeta del respaldo → `respaldo_v2_FECHA.zip` → subir a Drive, carpeta **"Ruta Local - Respaldos (EstudIA)"** (el admin la comparte con el equipo).
3. Capturas: `B03_respaldo_v2_terminal.png` (salida de `respaldar` y del manifiesto) y `B03_respaldo_v2_drive.png`.
4. PR de evidencia: llenar la sección B03 de la bitácora con la ruta del respaldo, la versión, los archivos, la ubicación en Drive y quién tiene acceso.
5. **No** subir la carpeta `respaldos/` ni el ZIP al repo: el respaldo debe quedar fuera de GitHub.

## Paso 4 — B04: error y recuperación (`simoncs02`)

Coordinar por llamada con el admin, porque el tiempo de espera de cada aprobación cuenta en la medición.

**PR 1 — provocar el error**
1. Rama `prueba-b04-error`: reemplazar todo `docs/index.html` por:
   ```html
   <!doctype html><html lang="es"><meta charset="utf-8"><title>Error simulado</title><h1>Catálogo incorrecto</h1><p>Versión de error para practicar la restauración.</p></html>
   ```
2. PR titulado `B04: error simulado` → admin aprueba y fusiona.
3. Cuando el sitio muestre **"Catálogo incorrecto"** en ventana privada: **⏱ anotar la HORA DE INICIO** y tomar la captura `B04_error.png`.

**PR 2 — recuperar**
4. Abrir el PR 1 (ya fusionado) → botón **Revert** → **Create pull request** → admin aprueba y fusiona.
5. Cuando el sitio vuelva a mostrar **Versión 2** con estilos y el pie `v2.0.0`: **⏱ anotar la HORA DE FIN** y tomar la captura `B04_recuperado.png`.

**PR 3 — evidencia**
6. Llenar la sección B04 de la bitácora: error provocado, método (revert), hora de inicio, hora de fin, duración, versión recuperada, pasos manuales y cuáles automatizarían.

## Paso 5 — B05: permisos (`andrezg876-lang`)

1. **Lectura:** en ventana privada, sin sesión, abrir el sitio (se ve) y `https://github.com/thomasT-maker/Infra-Nube-Proyecto-Estud-IA/settings` (debe dar **404**) → `B05_lectura_sin_sesion.png`.
2. **Actualización bloqueada en `main`:** en una terminal con su cuenta:
   ```
   git checkout main
   git pull
   echo prueba >> README.md
   git commit -am "Prueba B05: push directo"
   git push origin main
   ```
   Debe ser **rechazado** ("Changes must be made through a pull request") → `B05_push_rechazado.png`. Luego deshacer el commit local con `git reset --hard origin/main`.
3. **Tags protegidos:**
   ```
   git fetch --tags
   git push origin --delete v1.0.0
   ```
   Debe ser **rechazado** → `B05_tag_protegido.png`.
4. **Administración:** el colaborador no ve la pestaña **Settings** del repo → captura `B05_sin_settings.png`.
5. PR de evidencia con la sección B05 de la bitácora.

## Paso 6 — B06: repetibilidad (`juanpati913-sketch`)

Repetir **B04 completo** (PR de error → revert → evidencia) **solo con `PROCEDIMIENTOS.md`**, sin que nadie le explique. Capturas `B06_error.png` y `B06_recuperado.png`, horas de inicio y fin. En la sección B06 anotar las dudas que tuvo; si algo del procedimiento no se entendía, corregirlo en `PROCEDIMIENTOS.md` en el mismo PR.

> Antes de B06, el admin debe revisar y fusionar (o cerrar) el PR #5, que modifica `PROCEDIMIENTOS.md`, para que B06 se haga con la versión final de las instrucciones.

---

## Lista de revisión del admin (antes de aprobar cada PR)

- [ ] Cambia **solo** los archivos esperados (`docs/index.html` solo en PR de B02 y B04/B06; en los demás, solo `documentacion/`).
- [ ] La sección de la bitácora es la de su prueba y no borra la de otro.
- [ ] Las imágenes abren en la vista **Files changed** y no muestran credenciales.
- [ ] No hay ZIP, PDF ni carpeta `respaldos/` en el PR.
- [ ] En PR que tocan `docs/`: después del merge, revisar **Actions** (✅) y el sitio en ventana privada.
