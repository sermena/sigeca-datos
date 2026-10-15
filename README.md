# Guía Maestra de Documentos del SIGECA (prototipo)

Prototipo conceptual de un buscador para la guía maestra de documentos del Sistema Institucional de Gestión de Calidad (SIGECA) del Tecnológico de Costa Rica.

Permite buscar procedimientos, políticas, manuales, guías, instructivos, formularios y normativa, filtrarlos y ver con qué otros documentos se relaciona cada uno.

**Página publicada:** https://sermena.github.io/sigeca-datos/

> Los códigos, documentos y relaciones que muestra el prototipo son ficticios y solo ilustran el funcionamiento.

## Contenido

| Archivo | Descripción |
| --- | --- |
| `index.html` | Página autocontenida (HTML, CSS y JavaScript sin librerías). Incluye datos de ejemplo. |

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
