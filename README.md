# Dev Vault

Repositorio de documentación técnica del equipo: diagramas de arquitectura, flujos de datos y decisiones de diseño. Cada documento es un archivo HTML autocontenido (sin dependencias externas).

**URL pública:** https://irastorzatobias.github.io/dev-vault/

---

## Cómo funciona

Cada push a `main` despliega automáticamente via GitHub Actions. No hay build, no hay pipeline complejo — solo archivos HTML estáticos servidos por GitHub Pages.

El `index.html` raíz actúa como directorio: lee `manifest.json` y renderiza todos los documentos con su estado, dominio y autor.

---

## Agregar un nuevo documento

**1. Creá el archivo HTML**

El archivo debe ser autocontenido: todos los estilos y scripts inline, sin dependencias externas (sin CDN, sin imports). Así funciona offline y no rompe si cambia alguna URL externa.

**2. Copialo al repo**

```bash
cp mi-nuevo-diagrama.html dev-vault/
```

**3. Actualizá `manifest.json`**

Agregá un entry al array:

```json
{
  "file": "mi-nuevo-diagrama.html",
  "title": "Título del documento",
  "description": "Una línea explicando qué muestra",
  "domain": "Callback",
  "status": "draft",
  "author": "tu-nombre",
  "updated": "2026-06-22"
}
```

**4. Pusheá a main**

```bash
git add .
git commit -m "feat(docs): add mi-nuevo-diagrama"
git push
```

En ~30 segundos el documento aparece en el vault.

---

## Estados disponibles

| Status | Significado |
|--------|-------------|
| `draft` | Borrador inicial, trabajo en curso |
| `en-discusion` | Decisiones de diseño abiertas, se está discutiendo con el equipo |
| `en-progreso` | Desarrollo activo, el diagrama refleja trabajo en curso |
| `en-revision` | Listo para review, esperando aprobación |
| `publicado` | Aprobado y estable |
| `archivado` | Ya no vigente, se mantiene como referencia histórica |

---

## Dominios

Usá el campo `domain` en el manifest para agrupar documentos por área. Ejemplos actuales: `Callback`. Podés agregar cualquier dominio nuevo simplemente usándolo en el manifest — el index lo agrupa automáticamente.

---

## Estructura del repo

```
dev-vault/
├── .github/
│   └── workflows/
│       └── deploy.yml          ← GitHub Actions: deploy automático en push a main
├── index.html                  ← Directorio del vault (lee manifest.json)
├── manifest.json               ← Metadata de todos los documentos
├── callback-batch-architecture.html
├── callback-lead-flow.html
└── README.md
```

---

## Transferir a la organización

Cuando sea necesario mover el vault a la org de Picallex:

1. Settings → General → Danger Zone → Transfer repository
2. Ingresar `picallex` como destino
3. La URL cambia a `picallex.github.io/dev-vault/` automáticamente

---

## Convenciones

- Un documento = un archivo HTML
- Sin frameworks, sin dependencias externas
- El HTML debe funcionar abriéndolo localmente (`file://`) antes de subirlo
- Commits en inglés siguiendo conventional commits: `feat(docs):`, `fix(docs):`, `update(docs):`
