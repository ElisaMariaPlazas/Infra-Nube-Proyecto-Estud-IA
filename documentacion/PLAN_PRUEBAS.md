# Plan de pruebas por Pull Request

**Regla:** cada prueba entra a `main` por un Pull Request (PR). Lo **abre la cuenta de pruebas** y lo **aprueba y fusiona la cuenta admin**. Nadie escribe directo en `main`; la regla `proteger-main` lo impide y exige 1 aprobación de **otra** cuenta con permiso de escritura.

| Papel | Cuenta | Permiso en el repo | Qué hace |
|---|---|---|---|
| **Pruebas** | `tabordathomas-maker` | Colaborador (escritura) | Crea ramas, cambia archivos, abre los PR, toma capturas, llena la bitácora |
| **Admin / revisor** | `thomasT-maker` | Dueño (administración) | Revisa, aprueba y fusiona; crea tags; configura Pages, reglas y Drive |

> **Transparencia:** las dos cuentas son de la misma persona (Thomas). Lo que se demuestra es la **separación de permisos** (quien propone no puede publicar sin aprobación de otra cuenta), no la separación de personas. Se declara así en la bitácora y en la demo.

---

## Preparación (una sola vez)

1. **Admin:** Settings → **Collaborators** → **Add people** → `tabordathomas-maker` → rol de escritura.
2. **Cuenta de pruebas:** aceptar la invitación (https://github.com/notifications).
3. **Dos navegadores**, para no confundir las sesiones:
   - Navegador A (por ejemplo **Chrome**): sesión de **`thomasT-maker`** → solo aprobar y fusionar.
   - Navegador B (por ejemplo **Edge**): sesión de **`tabordathomas-maker`** → abrir PR.
   - Para verificar el sitio: **ventana privada** (sin sesión).
4. **Admin:** compartir la carpeta de Drive "Ruta Local - Respaldos (EstudIA)" con el correo de la cuenta de pruebas (sin enlace público).

## Orden de trabajo

| # | Qué | Abre el PR (B) | Aprueba y fusiona (A) | Después |
|---|---|---|---|---|
| 0 | Integrar bitácora y plan | — (es el PR #7, de la cuenta admin) | **La cuenta de pruebas aprueba**; el admin fusiona | — |
| 0b | PR #5 (mejora de `PROCEDIMIENTOS.md`) | — | Admin aprueba y fusiona | Debe entrar **antes de B06** |
| 1 | **B01** Publicación | — | — | ✅ Ya registrada |
| 2 | **B02** Corregir el pie `v2.0.0` | `prueba-b02-pie` | ✔ | Admin crea tags `v1.0.0` y `v2.0.0` |
| 3 | **B03** Respaldo de la v2 | `prueba-b03-respaldo` (evidencia) | ✔ | — |
| 4 | **B04** Error → recuperación | 3 PR: error, revert, evidencia | ✔ los 3, rápido | ⏱ se mide el tiempo |
| 5 | **B05** Permisos | `prueba-b05-permisos` (evidencia) | ✔ | — |
| 6 | **B06** Repetibilidad | ver nota | ✔ | — |
| 7 | Cierre de la bitácora | `cierre-bitacora` | ✔ | Borrar ramas fusionadas |

---

## Cómo se hace un PR (siempre igual)

**En el navegador B (cuenta de pruebas):**
1. Ir al archivo → lápiz ✏️ (o, para imágenes: `documentacion/evidencias` → **Add file → Upload files**).
2. **Commit changes…** → **Create a new branch** → nombre de la tabla → **Propose changes** → **Create pull request**.
3. Para agregar más archivos a la misma rama: cambiar a esa rama (selector de ramas, arriba a la izquierda) y hacer commit **directamente en ella**.

**En el navegador A (admin):**
4. PR → **Files changed** → revisar con la lista de revisión (abajo) → **Review changes → Approve → Submit review**.
5. **Conversation** → **Merge pull request** → **Confirm merge**.
6. Si el PR tocó `docs/`: pestaña **Actions** ✅ → verificar el sitio en **ventana privada**.

---

## Paso 0 — Integrar la bitácora y este plan (PR #7)
- **B:** PR #7 → **Files changed → Review changes → Approve**.
- **A:** **Merge**. Desde aquí, la bitácora y este plan están en `main`.

## Paso 0b — PR #5 de Simón
- **A:** PR #5 → revisar → **Approve → Merge**. (Completa §4.3 y §4.5 de `PROCEDIMIENTOS.md`; está correcto.)

## Paso 2 — B02: corregir el pie
1. **B**, rama `prueba-b02-pie`: en `docs/index.html` agregar `<br><small>v2.0.0</small>` justo antes de `</footer>`. En la misma rama, en `README.md`, borrar la última línea suelta: "Prueba de commit".
2. **A**: aprobar → merge → Actions ✅ → ventana privada: el pie dice **v2.0.0**.
3. **B**: captura `B02_v2_pie_corregido.png` → subirla y completar en la bitácora B02 *Resultado al repetir la prueba* (se puede hacer en el PR de B03 para no abrir uno extra).
4. **A**: **Releases → Draft a new release**:
   - `v1.0.0` → Target: *Recent commits* → **"Merge pull request #1…"** → Publish.
   - `v2.0.0` → Target: **el merge de `prueba-b02-pie`** → Publish.

## Paso 3 — B03: respaldo de la versión 2
1. En el PC (terminal, dentro del repo clonado):
   ```
   git checkout main
   git pull
   python scripts/herramientas.py preparar
   copy docs\index.html trabajo\
   copy docs\styles.css trabajo\
   python scripts/herramientas.py respaldar
   type respaldos\NOMBRE_QUE_IMPRIMIÓ\manifest.json
   ```
2. Comprimir la carpeta del respaldo → `respaldo_v2_FECHA.zip` → subir a Drive, carpeta "Ruta Local - Respaldos (EstudIA)".
3. Capturas: `B03_respaldo_v2_terminal.png` y `B03_respaldo_v2_drive.png`.
4. **B**, rama `prueba-b03-respaldo`: subir las capturas y llenar la sección **B03** de la bitácora (ruta, versión, archivos, ubicación en Drive y quién tiene acceso). **No** subir el ZIP ni `respaldos/`.
5. **A**: comprobar en Drive que el ZIP existe → aprobar → merge.

> ⚠️ **B04 no empieza sin B03:** no se rompe el sitio sin tener un respaldo.

## Paso 4 — B04: error y recuperación (con cronómetro)

Tener abiertos los dos navegadores y una ventana privada con el sitio.

**PR 1 — error**
1. **B**, rama `prueba-b04-error`: reemplazar todo `docs/index.html` por:
   ```html
   <!doctype html><html lang="es"><meta charset="utf-8"><title>Error simulado</title><h1>Catálogo incorrecto</h1><p>Versión de error para practicar la restauración.</p></html>
   ```
2. **A**: aprobar → merge.
3. Ventana privada: cuando aparezca **"Catálogo incorrecto"** → **⏱ HORA DE INICIO** + captura `B04_error.png`.

**PR 2 — recuperar**
4. **B**: abrir el PR 1 (ya fusionado) → botón **Revert** → **Create pull request**.
5. **A**: aprobar → merge.
6. Ventana privada: cuando vuelva **Versión 2** con estilos y el pie **v2.0.0** → **⏱ HORA DE FIN** + captura `B04_recuperado.png`.

**PR 3 — evidencia**
7. **B**, rama `prueba-b04-evidencia`: subir las capturas y llenar **B04**: error provocado, método (*revert*), inicio, fin, **duración**, versión recuperada y qué pasos automatizarían.
8. **A**: aprobar → merge.

## Paso 5 — B05: permisos
1. **Lectura** (ventana privada, sin sesión): el sitio se ve; `https://github.com/thomasT-maker/Infra-Nube-Proyecto-Estud-IA/settings` da **404** → `B05_lectura_sin_sesion.png`.
2. **La cuenta de pruebas no puede publicar directo** (navegador B): abrir `docs/index.html` → ✏️ → **Commit changes…** La opción *Commit directly to the main branch* aparece bloqueada o, si se intenta, GitHub la rechaza por la regla → `B05_commit_directo_bloqueado.png`. Cancelar sin guardar.
3. **La cuenta de pruebas no ve la configuración** (navegador B): en el repo **no aparece la pestaña Settings** → `B05_sin_settings.png`.
4. **Tags protegidos** (terminal, con la cuenta de pruebas):
   ```
   git fetch --tags
   git push https://tabordathomas-maker@github.com/thomasT-maker/Infra-Nube-Proyecto-Estud-IA.git --delete v1.0.0
   ```
   (Si pide iniciar sesión, entrar con **tabordathomas-maker**.) Debe salir **rechazado** por *repository rule violations* → `B05_tag_protegido.png`. Comprobar en **Releases** que `v1.0.0` sigue ahí.
5. **Administración** (navegador A): Settings → **Rules** → captura de los dos rulesets activos → `B05_rulesets_admin.png`.
6. **B**, rama `prueba-b05-permisos`: subir las capturas y llenar **B05** → **A** aprueba → merge.

## Paso 6 — B06: repetibilidad

La guía pide que **otro integrante** repita un procedimiento solo con las instrucciones. **Una segunda cuenta de la misma persona no cumple eso.**

- **Opción recomendada:** pedirle a un compañero (Andrés, Juan o Simón) que repita **B04** leyendo solo `PROCEDIMIENTOS.md`, con sus capturas y sus horas. El admin aprueba sus PR.
- **Si nadie puede:** marcar B06 como **"No realizado"** en la bitácora, explicar por qué y dejarlo como pendiente para el encuentro 3. Es mejor reportarlo así que presentarlo como cumplido.

## Paso 7 — Cierre
1. **B**, rama `cierre-bitacora`: llenar **Registro del equipo** (integrantes, cuentas y roles, incluida la nota de transparencia) y **Cierre** (qué funciona, pendientes y mejoras para el encuentro 3).
2. **A**: aprobar → merge.
3. **A**: **Branches** → borrar 🗑️ las ramas ya fusionadas (`estructura-inicial`, `actualizar-v2`, `bitacora-b01`, `juanpati913-sketch-patch-1`, `pruebas-b01-b06`, `prueba-…`).

---

## Lista de revisión del admin (antes de cada *Approve*)

- [ ] **Files changed** toca solo lo esperado: `docs/index.html` solo en B02 y en los PR de error/revert; en los demás, solo `documentacion/` (y `README.md` en B02).
- [ ] En la bitácora cambia **solo la sección de esa prueba**.
- [ ] Las imágenes abren y **no muestran contraseñas, tokens ni códigos**.
- [ ] No hay **ZIP, PDF, `respaldos/` ni `trabajo/`**.
- [ ] Las horas tienen sentido (el fin es posterior al inicio).
- [ ] Si tocó `docs/`: después del merge, **Actions** ✅ y sitio en **ventana privada** (si se ve la versión anterior: Ctrl+Shift+R o esperar unos minutos, por la caché de ~10 min).

## Si algo sale mal

| Problema | Qué hacer |
|---|---|
| El sitio quedó roto | **B** abre el PR **Revert** → **A** aprueba → merge. |
| No se puede aprobar ("can't approve your own PR") | El PR lo abrió la cuenta equivocada: ciérralo y ábrelo desde el **navegador B**. |
| *"This branch has conflicts"* | **Resolve conflicts** → conservar ambas secciones → **Mark as resolved** → **Commit merge**. |
| La cuenta de pruebas no puede crear ramas | No ha aceptado la invitación de colaborador. |
| GitHub no responde | Último ZIP de Drive → `PROCEDIMIENTOS.md` §4.5 → demo local. |
