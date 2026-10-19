# Guía Maestra de Documentos del SIGECA (prototipo)

Prototipo conceptual de un buscador para la guía maestra de documentos del Sistema Institucional de Gestión de Calidad (SIGECA) del Tecnológico de Costa Rica.

Permite buscar procedimientos, políticas, manuales, guías, instructivos, formularios y normativa, filtrarlos y ver con qué otros documentos se relaciona cada uno.

**Página publicada:** https://sermena.github.io/sigeca-datos/

> Los códigos, documentos y relaciones que muestra el prototipo son ficticios y solo ilustran el funcionamiento.

## Contenido

| Archivo | Descripción |
| --- | --- |
| `index.html` | Página autocontenida (HTML, CSS y JavaScript sin librerías). Incluye datos de ejemplo. |
| `roadmap/index.html` | Tablero del roadmap del proyecto, con modo de edición. |
| `roadmap/roadmap.json` | Datos del roadmap: fases, tareas, hitos, observaciones, riesgos y calendario. |

## Cómo funciona

- La búsqueda corre en el navegador: ignora tildes y mayúsculas, tolera errores de digitación y pondera más el código y el nombre.
- El estado de cada documento (vigente, próximo a vencer, revisión vencida) se calcula con la fecha de próxima revisión; el aviso se activa 90 días antes.
- Cada ficha tiene un enlace propio, por ejemplo `index.html#doc=PR-OPI-001`.

## Conectar datos reales

En el script de `index.html`, la constante `DATA_URL` apunta al archivo de datos. Si es `null`, la página usa los datos de ejemplo incluidos. Para usar la lista maestra real, exporte un archivo `documentos.json` con esta estructura y asigne `DATA_URL = "documentos.json"`:

```json
{
  "dependencias": { "OPI": "Oficina de Planificación Institucional" },
  "documentos": [
    {
      "codigo": "PR-OPI-001",
      "titulo": "Elaboración, revisión y aprobación de documentos del SIGECA",
      "tipo": "PR",
      "dependencia": "OPI",
      "proceso": "Planificación y calidad",
      "version": "3",
      "fecha_aprobacion": "2025-03-10",
      "proxima_revision": "2027-03-10",
      "palabras_clave": ["control documental", "versiones"],
      "resumen": "Define cómo se elabora, revisa, aprueba y publica un documento del sistema."
    }
  ],
  "relaciones": [["PR-OPI-001", "MA-OPI-001"]]
}
```

Cada relación se registra una vez, de origen a destino; la página calcula el sentido inverso ("referenciado por").

## Roadmap del proyecto

**Página publicada:** https://sermena.github.io/sigeca-datos/roadmap/

Muestra el avance esperado semana a semana frente al avance real (tareas cumplidas), por fase, hito, observación y riesgo. Todo el contenido vive en `roadmap/roadmap.json`.

### Editar el plan

1. Abra la página y pulse **Editar plan** (o entre a `roadmap/#editar`).
2. Cambie lo que necesite: duración, espera previa y dependencias de cada fase, tareas (y cuáles están cumplidas), insumos, entregables, hitos, notas de avance, observaciones, riesgos, fecha de inicio y recesos. Las fases se reprograman solas según sus dependencias.
3. Los cambios quedan como borrador en su navegador hasta que pulse **Guardar en GitHub** o **Descartar cambios**.

Para guardar desde la página se necesita un token personal de GitHub (una sola vez por navegador):

1. En GitHub, vaya a *Settings › Developer settings › Personal access tokens › Fine-grained tokens › Generate new token*.
2. En *Repository access*, elija **Only select repositories** y marque `sermena/sigeca-datos`.
3. En *Permissions › Repository permissions*, ponga **Contents: Read and write**.
4. Copie el token y péguelo en *Configuración › Guardar en GitHub* dentro de la página. Use **Probar conexión** para verificarlo.

Cada guardado crea un commit en `main` y GitHub Pages publica la nueva versión en uno o dos minutos. Si alguien guardó otra versión mientras usted editaba, la página avisa y le deja elegir entre sobrescribir o cargar la versión de GitHub.

Sin token, use **Descargar JSON** y suba el archivo a la carpeta `roadmap/` del repositorio desde la web de GitHub (*Add file › Upload files*).
