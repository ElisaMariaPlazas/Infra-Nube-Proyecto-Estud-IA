# Permisos (prueba B05)

La guía distingue tres accesos: **lectura** (consultar el sitio), **actualización** (cargar o modificar archivos) y **administración** (cambiar la configuración y los permisos).

## Quién tiene cada acceso

| Acceso | Quién | Cómo se obtiene en GitHub | Qué puede hacer |
|---|---|---|---|
| Lectura | Visitantes y aliados de Ruta Local (cualquiera) | No necesita cuenta: abre la URL de Pages | Ver el catálogo. No puede modificar nada. |
| Actualización | *[completar usuarios]* | Colaborador del repositorio (permiso de escritura) | Crear ramas y PR. **No** puede escribir directo en `main` ni borrar tags. |
| Revisión | *[completar usuario]* | Colaborador | Aprobar los PR que llegan a `main`. |
| Administración | *[completar: thomasT-maker]* | Dueño del repositorio | Configurar Pages, protección de rama, rulesets y colaboradores. |

> **Limitación del repositorio personal:** en una cuenta personal, todo colaborador tiene escritura; no existe un rol "solo lectura" dentro del repo. La lectura se demuestra como visitante sin sesión. Una organización gratuita de GitHub ofrecería los roles Read, Write y Admin por separado (mejora posible para el encuentro 3).

## Configuración que hace el admin (en la web)

### Protección de `main`
**Settings → Rules → Rulesets → New branch ruleset**
- Nombre: `proteger-main`; Enforcement: **Active**
- Target: **Include default branch**
- Activar: **Restrict deletions**, **Block force pushes**, **Require a pull request before merging** con **1 approval** requerida.
- Bypass list: dejar vacía. Si se acuerda el procedimiento de emergencia, agregar solo al admin y documentar cada uso en la bitácora.

### Protección de tags
**Settings → Rules → Rulesets → New tag ruleset**
- Nombre: `proteger-versiones`; Enforcement: **Active**
- Target: **Add target → Include by pattern** → `v*`
- Activar: **Restrict deletions**, **Restrict updates**, **Block force pushes**.

## Cómo demostrarlo

1. **Lectura:** abrir la URL en ventana privada, sin sesión. Se ve el sitio, y no hay ninguna forma de editarlo.
2. **Actualización:** un colaborador intenta `git push origin main` directo → GitHub lo **rechaza**. Luego lo hace por PR → funciona después de la aprobación.
3. **Tags:** un colaborador intenta `git push origin :refs/tags/v1.0.0` (borrar el tag) → **rechazado**.
4. **Administración:** captura de la pantalla de rulesets (sin datos personales ni tokens) y explicar que solo el admin la ve.

Registrar cada intento en la bitácora. **No incluir contraseñas, tokens ni capturas de credenciales.**
