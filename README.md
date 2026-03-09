# ⬡ .changelog

> Documentación automática de commits para equipos Git. Se activa con cada `git commit`, hace dos preguntas al desarrollador y genera un visor HTML interactivo sin necesidad de servidores ni configuración extra.

---

## ¿Qué hace?

Cada vez que haces un `git commit`, el sistema:

1. **Recoge toda la información** del commit automáticamente (hash, autor, rama, archivos modificados, líneas añadidas/borradas, tipo Conventional Commits)
2. **Te hace 2 preguntas** para enriquecer la documentación
3. **Guarda los datos** en JSONs organizados por rama
4. **Actualiza el visor HTML** con los datos más recientes, listo para abrir con Live Server

---

## 📁 Estructura generada

```
.changelog/
├── branches/
│   ├── main.json               # Commits de main
│   ├── feature-login.json      # Commits de feature/login
│   └── ...                     # Un archivo por rama
├── index.json                  # Metadatos del proyecto + resumen
└── index.html                  # Visor visual interactivo
```

---

## ⚡ Instalación

> Cada miembro del equipo debe ejecutar esto **una sola vez** en su clon local.

**1. Coloca estos 3 archivos en la raíz de tu proyecto:**

```
mi-proyecto/
├── setup-changelog.sh
├── post-commit
└── changelog-viewer.html
```

**2. Ejecuta el instalador:**

```bash
bash setup-changelog.sh
```

**3. ¡Listo!** Haz tu primer commit para probarlo:

```bash
git add .
git commit -m "feat: mi primer commit documentado"
```

---

## 💬 Flujo de uso

```
$ git commit -m "feat(auth): añadir login con Google"

📋 .changelog — Generando documentación...

❓ Dos preguntas para documentar mejor este commit:

  1. ¿Qué problema resuelve o qué aporta este commit?
     → Permite autenticarse con cuenta de Google sin registro manual

  2. ¿Hay algo que otro desarrollador deba saber?
     → Requiere configurar GOOGLE_CLIENT_ID en el .env

  ✓ JSONs actualizados
  ✓ HTML listo — ábrelo con Live Server

✅ Listo  hash: a1b2c3d  rama: feature/auth
```

---

## 🌐 Ver el visor

Abre `.changelog/index.html` con **Live Server** en VS Code.

> El visor tiene los datos inyectados directamente — no necesita servidor ni conexión.

---

## 🗂️ Estructura del JSON por commit

```json
{
  "hash": "a1b2c3d",
  "hash_full": "a1b2c3d4e5f6...",
  "message": "feat(auth): añadir login con Google",
  "type": "feat",
  "scope": "auth",
  "subject": "añadir login con Google",
  "description": "Permite autenticarse con cuenta de Google",
  "notes": "Requiere GOOGLE_CLIENT_ID en .env",
  "author": { "name": "Ana García", "email": "ana@empresa.com" },
  "branch": "feature/auth",
  "date": "2026-03-05T15:30:00Z",
  "stats": { "files_changed": 3, "lines_added": 120, "lines_deleted": 4 },
  "files": [
    { "file": "src/auth/google.js", "status": "added" },
    { "file": "src/login.js",       "status": "modified" }
  ]
}
```

---

## 🏷️ Tipos de commit soportados

| Tipo | Color | Descripción |
|------|-------|-------------|
| `feat` | 🟢 Verde | Nueva funcionalidad |
| `fix` | 🔴 Rojo | Corrección de bug |
| `docs` | 🔵 Cian | Documentación |
| `style` | 🩷 Rosa | Formato, sin cambios de lógica |
| `refactor` | 🟣 Morado | Refactorización |
| `perf` | 🟠 Naranja | Mejora de rendimiento |
| `test` | 🟡 Amarillo | Tests |
| `chore` | ⚪ Gris | Mantenimiento |

---

## 🔀 Sin conflictos en equipo

| Situación | ¿Conflicto? |
|-----------|-------------|
| Ana en `feature/login` y Bob en `feature/payments` | ✅ Nunca — archivos distintos |
| Ana y Bob en la misma rama a la vez | ⚠️ Muy raro — commits se insertan al inicio del array |
| Merge entre ramas | ✅ Nunca — cada rama tiene su propio JSON |

---

## 📋 Requisitos

- Git
- Python 3
- Bash (en Windows: Git Bash o WSL)