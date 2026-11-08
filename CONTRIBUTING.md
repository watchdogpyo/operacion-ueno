# Cómo colaborar

¡Gracias por querer ayudar! Este mapa solo es útil si es **preciso**. Por eso hay pocas reglas, pero son estrictas.

## Reglas

1. **Sin fuente, no entra.** Todo vínculo nuevo necesita al menos una fuente pública y verificable: nota de prensa, documento oficial, registro público, resolución judicial, etc. Incluí el enlace.
2. **Hechos, no opiniones.** Describí qué dice la fuente («figura como directivo de…», «recibió G. X de…»), sin adjetivos ni acusaciones que la fuente no sostenga.
3. **Si la identidad no está confirmada, no se publica el nombre.** Se puede proponer, pero queda marcado `[POR CONFIRMAR]` o fuera del mapa hasta verificarlo.
4. **Nada de datos privados** (domicilios, teléfonos, documentos de identidad, menores de edad).
5. **Las correcciones son bienvenidas**, incluso de las personas que aparecen en el mapa. Si algo está mal, abrí un Issue con la fuente que lo demuestra.

> **¿Te preocupa tu seguridad?** Usá una cuenta de GitHub anónima para colaborar, o enviá la información por mensaje directo (DM) a [@watchdogpyo](https://x.com/watchdogpyo) en Twitter/X.

## Opción A — Sin programar: abrir un Issue

1. Entrá a la pestaña **Issues** del repositorio → **New issue**.
2. Elegí **«Nuevo vínculo o corrección»**.
3. Completá el formulario (quién, con quién, qué relación, fuente) y enviá.

Quien mantiene el proyecto lo revisa y, si está bien respaldado, lo agrega.

## Opción B — Editar el mapa (Pull Request)

Todo está en `index.html`. Los datos están en tres listas dentro del archivo:

- **`nodes`** — las entidades. Ejemplo:
  ```js
  { id: "mi_empresa", label: "Mi Empresa S.A.", role: "Proveedora del Estado", group: "satellite" },
  ```
  - `id`: código corto, sin espacios ni acentos, único.
  - `group`: una de `hub`, `offshore`, `antecedent`, `state`, `regulator`, `political`, `family`, `holding`, `executive`, `satellite`.
  - **Agregá entidades nuevas al final de la lista** para no cambiar los códigos existentes.

- **`CLUSTERS`** — los grupos del mapa (Familia Peña, Grupo Vázquez, Fondos del Estado, etc.). Para que una entidad nueva aparezca dentro de un grupo, agregá su `id` a la lista `members` de ese grupo; el círculo del grupo crece solo. Si no está en ningún grupo, el mapa la muestra aparte, en un círculo propio llamado «SIN GRUPO» cerca de la entidad con la que está vinculada (nunca dentro del círculo de otro grupo). Eso es una señal de que falta asignarle un grupo.
  - Para crear un grupo nuevo alcanza con `{ id: "nuevo", title: "NOMBRE", hub: "id_del_centro", members: ["id1", "id2"] },` — el mapa le busca un lugar libre cerca de lo que está vinculado (`x` / `y` son opcionales).
  - Abrí la consola del navegador (F12): si un `id` no existe, está en dos grupos o quedó sin grupo, aparece un aviso.

- **`SOURCES`** — las fuentes. Cada artículo o documento se carga **una sola vez**, con una clave:
  ```js
  "abc-2026-11-04": { medio: "ABC Color", fecha: "04/11/2026", titulo: "Título de la nota", url: "https://..." },
  ```

- **`links`** — los vínculos. Cada uno cita sus fuentes por clave con `src`:
  ```js
  { source: "mi_empresa", target: "ueno", desc: "Qué dice la fuente, con montos si los hay.", src: ["abc-2026-11-04"] },
  ```

Antes de mandar el cambio, abrí `index.html` en el navegador y comprobá que el mapa carga y que tu entidad aparece.

En la descripción del Pull Request explicá qué agregaste y pegá las fuentes.
