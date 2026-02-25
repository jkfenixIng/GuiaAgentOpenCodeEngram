# 🚀 Guía Rápida de Uso: Engram + Agent Teams Lite

<div align="center">

![Engram](https://img.shields.io/badge/Engram-Memoria%20Persistente-6C5CE7?style=for-the-badge)
![Agent Teams Lite](https://img.shields.io/badge/Agent%20Teams%20Lite-SDD%20Framework-00CEC9?style=for-the-badge)
![OpenCode](https://img.shields.io/badge/OpenCode-Compatible-FF7675?style=for-the-badge)

**La guía definitiva para developers que trabajan con AI**

*Desde lo básico hasta comandos avanzados — todo lo que necesitas en un solo lugar*

</div>

---

## 📋 Índice Rápido

| # | Sección | Descripción | ¿Para quién? |
|---|---------|-------------|--------------|
| 1 | [🎯 Primeros Pasos](#introducción) | Por qué usar estas herramientas juntas | Todos |
| 2 | [💾 Engram: Comandos](#engram) | Los 4 comandos que más usarás | Todos |
| 3 | [📦 Agent Teams Lite: Flujo SDD](#agent-teams-lite) | Los 8 comandos del orquestador | Todos |
| 4 | [🔗 Integración con OpenCode](#integración) | Cómo activar ambas herramientas | Usuarios nuevos |
| 5 | [⚡ Cheat Sheet](#cheat-sheet) | **Todos los comandos en una tabla** | Todos |
| 6 | [📖 Glosario](#glosario) | Términos técnicos explicados | Juniors |
| 7 | [🌊 Ejemplo de Flujo Real](#ejemplo-flujo) | Ejemplo completo paso a paso | **Todos** |

> **💡 Tip:** Si ya sabes lo básico y solo necesitas recordar comandos, salta directo a la sección [⚡ Cheat Sheet](#cheat-sheet)

---

<a name="introducción"></a>
## 1. 🎯 Introducción: ¿Por qué usar estas herramientas juntas?

Engram y Agent Teams Lite se complementan perfectamente: **Engram** recuerda lo que tú olvidas, **Agent Teams Lite** organiza cómo trabajas.

### El Problema que Resuelven

| Problema | Engram | Agent Teams Lite |
|----------|--------|------------------|
| ✅ Pierdo contexto entre sesiones | ✅ Lo guarda todo | ❌ No aplica |
| ✅ Mi código no tiene estructura | ❌ No aplica | ✅ Flujo SDD definido |
| ✅ Olvido decisiones importantes | ✅ Búsqueda instantánea | ❌ No aplica |
| ✅ Cambios sin documentación | ❌ No aplica | ✅ Specs formales |

<details>
<summary><strong>🧠 ¿Cómo funcionan juntos?</strong></summary>

**Un día típico:**
1. **Mañana:** `/sdd:new mi-feature` → el sistema investiga, propone y planea
2. **Mediodía:** `/sdd:apply` → implementa mientras tú haces otras cosas
3. **Tarde:** `/sdd:verify` → valida contra specs + `mem_save` para guardar aprendizajes
4. **Antes de irte:** `mem_session_summary` → documenta el progreso

</details>

---

<a name="engram"></a>
## 2. 💾 Engram: Tu Sistema de Memoria Persistente

> **⚡ TL;DR:** Los únicos comandos que necesitas son: `mem_save`, `mem_search`, `mem_session_summary` y `mem_context`

### Los 4 Comandos Esenciales

| Comando | Cuándo Usarlo | Ejemplo |
|---------|---------------|---------|
| **`mem_save`** | Después de algo importante (bugfix, decisión arquitectónica) | `mem_save(title: "Fix N+1", type: "bugfix", content: "...")` |
| **`mem_search`** | Cuando necesitas recordar algo | `mem_search("query N+1 user list")` |
| **`mem_session_summary`** | Al final de cada sesión | `mem_session_summary(goal: "...", discoveries: "...", ...)` |
| **`mem_context`** | Al empezar una sesión | `mem_context("mi-proyecto")` |

### Estructura de una Memoria

```markdown
mem_save(
  title: "Fixed N+1 query in user list",    # What happened
  type: "bugfix",                            # bugfix | decision | pattern | learning
  content: """
    What: Query N+1 encontrado en /api/users
    Why: El loop hacia user.posts causaba una query por usuario
    Where: endpoints/users.ts línea 45
    Learned: Siempre usar eager loading con include()
  """
)
```

### 🔑 Topic Keys (para temas que evolucionan)

```markdown
# 1. Primero, sugiere una clave
mem_suggest_topic_key(type: "architecture", title: "Auth system")

# 2. Usa la misma clave en todas las actualizaciones
mem_save(title: "Added JWT refresh", topic_key: "architecture-auth-system", ...)
# → Engram ACTUALIZA la memoria existente en lugar de crear otra nueva
```

### 💻 Comandos CLI (alternativos)

```bash
engram serve [port]        # Iniciar servidor API (default: 7437)
engram tui                 # Interfaz visual interactiva
engram search <query>      # Buscar desde terminal
engram save <title> <msg>  # Guardar desde terminal
engram sync                # Sincronizar con Git
```

> **💡 Tip CLI:** Ejecuta `engram tui` para explorar tus memorias visualmente — es como tener un navegador de memoria integrado.

---

<a name="agent-teams-lite"></a>
## 3. 📦 Agent Teams Lite: Desarrollo Dirigido por Especificaciones

> **⚡ TL;DR:** Todo flujo SDD empieza con `/sdd:new` y termina con `/sdd:archive`

### Los 8 Comandos del Orquestador

| Comando | Alias | QuéHace | Cuándo |
|---------|-------|---------|--------|
| `/sdd:init` | — | Inicializar contexto SDD | Una vez por proyecto |
| `/sdd:explore <topic>` | — | Investigar el codebase | Antes de proponer |
| `/sdd:new <name>` | — | Iniciar nuevo cambio | Nueva feature |
| `/sdd:continue` | — | Siguiente fase lista | Después de aprobar |
| `/sdd:ff <name>` | Fast-Forward | Ejecutar proposal→specs→design→tasks | Cuando tienes prisa |
| `/sdd:apply` | — | Implementar tareas | Hora de programar |
| `/sdd:verify` | — | Validar vs specs | Antes de commit |
| `/sdd:archive` | — | Cerrar cambio | Todo listo |

### Flujo Visual

```
┌─────────────┐
│ /sdd:new    │ ← INICIO: Nueva feature
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ Exploration │ ← Explorer + Proposer
│ + Proposal  │   Crean proposal.md
└──────┬──────┘
       │ Aprobar propuesta?
       ▼
┌─────────────┐
│ Specs +     │ ← Spec Writer + Designer + Task Planner
│ Design +    │   Crean delta specs, design.md, tasks.md
│ Tasks       │
└──────┬──────┘
       │ Ejecutar /sdd:apply?
       ▼
┌─────────────┐
│ Implement   │ ← Implementer escribe código
│ (iterable)  │   Marca tareas completadas
└──────┬──────┘
       │ Todo implementado?
       ▼
┌─────────────┐
│ /sdd:verify │ ← Verifier valida contra specs
└──────┬──────┘
       │ Todo OK?
       ▼
┌─────────────┐
│ /sdd:archive│ ← ARCHIVER cierra cambio
└─────────────┘
```

### Ejemplo Completo

```bash
# 1. Iniciar nuevo cambio
/sdd:new add-dark-mode

# 2. El sistema lanza Explorer + Proposer automáticamente
#    → Crea proposal.md

# 3. Aprobar y continuar
/sdd:continue
# ó fast-forward si tienes prisa:
/sdd:ff add-dark-mode

# 4. Implementar
/sdd:apply

# 5. Verificar
/sdd:verify
# Reporte: CRITICAL / WARNING / SUGGESTION

# 6. Cerrar
/sdd:archive
```

### Formato de Delta Specs

```markdown
## ADDED Requirements
### Requirement: Dark Mode
El sistema SHALL permitir cambiar entre modo claro y oscuro.

## MODIFIED Requirements
### Requirement: Theme Persistence
El sistema SHALL guardar la preferencia en localStorage.
(Previously: No persistencia de tema)

## REMOVED Requirements
### Requirement: Hardcoded Colors
La aplicación NO SHALL usar colores hardcodeados en CSS.
```

---

<a name="integración"></a>
## 4. 🔗 Integración con OpenCode

### Engram → Ya viene con MCP

Simplemente asegúrate de que Engram esté corriendo:

```bash
engram serve
# ó
engram mcp
```

### Agent Teams Lite → Configuración

```bash
# 1. Copiar skills
cp -r skills/sdd-* ~/.opencode/skills/

# 2. Integrar en config (lee examples/opencode/opencode.json)

# 3. Usar
#    Selecciona "sdd-orchestrator" con Tab
#    Enjoy! 🎉
```

---

<a name="cheat-sheet"></a>
## 5. ⚡ Cheat Sheet de Referencia Rápida

### Comandos de Engram (MCP)

| Comando | Descripción |
|---------|-------------|
| `mem_save(title, type, content)` | ✅ Guardar una memoria |
| `mem_search(query)` | 🔍 Buscar en todas las memorias |
| `mem_session_summary(goal, discoveries, accomplished, files)` | 📝 Resumen de sesión |
| `mem_context(project)` | 📚 Obtener contexto de sesiones anteriores |
| `mem_update(id, content)` | ✏️ Actualizar una memoria |
| `mem_delete(id)` | 🗑️ Eliminar una memoria |
| `mem_timeline(observation_id)` | 📅 Ver contexto cronológico |
| `mem_stats()` | 📊 Ver estadísticas del sistema |
| `mem_suggest_topic_key(type, title)` | 🔑 Sugerir topic_key estable |

### Comandos de Agent Teams Lite (SDD)

| Comando | Descripción |
|---------|-------------|
| `/sdd:init` | 🚀 Inicializar orquestación |
| `/sdd:explore <topic>` | 🔬 Investigar el codebase |
| `/sdd:new <name>` | ✨ Iniciar nuevo cambio |
| `/sdd:continue` | ⏭️ Ejecutar siguiente fase |
| `/sdd:ff <name>` | ⚡ Fast-forward planning |
| `/sdd:apply` | 💻 Implementar tareas |
| `/sdd:verify` | ✅ Verificar implementación |
| `/sdd:archive` | 📦 Cerrar y persistir cambio |

### Comandos CLI de Engram

| Comando | Descripción |
|---------|-------------|
| `engram serve [port]` | 🌐 Iniciar servidor API |
| `engram tui` | 🎨 Interfaz visual interactiva |
| `engram search <query>` | 🔍 Buscar desde terminal |
| `engram save <title> <msg>` | 💾 Guardar desde terminal |
| `engram export` | 📤 Exportar a JSON |
| `engram import <file>` | 📥 Importar desde JSON |
| `engram sync` | 🔄 Sincronizar con Git |

---

<a name="glosario"></a>
## 6. 📖 Glosario de Términos

| Término | Definición Simple |
|---------|-------------------|
| **MCP** | Protocolo que conecta tu agente AI con herramientas externas |
| **Sub-agente** | Agente especializado que hace una tarea específica |
| **Delta Specs** | Specs que solo muestran cambios (ADDED/MODIFIED/REMOVED) |
| **Given/When/Then** | Formato para escribir requisitos: Dado X, Cuando Y, Entonces Z |
| **RFC 2119** | Estándar para requisitos: SHALL (debe), SHOULD (debería), MAY (puede) |
| **FTS5** | Tecnología de búsqueda rápida en SQLite |
| **Artifact Store** | Dónde se guardan specs/proposals: engram, openspec, o none |

---

<a name="ejemplo-flujo"></a>
## 7. 🌊 Ejemplo de Flujo Real: Agregar Exportación CSV

Esta sección te muestra un ejemplo completo y paso a paso de cómo usar ambas herramientas juntas en un escenario real. Imagina que estás trabajando en una aplicación de gestión de tareas y necesitas agregar una funcionalidad de exportación a CSV.

### Contexto Inicial

Es lunes por la mañana. Tienes una aplicación de tareas construida con React + Node.js. Ya tienes varias semanas trabajando en el proyecto y has corregido varios bugs importantes. Antes de empezar cualquier cosa nueva, siempre es buena práctica obtener contexto de sesiones anteriores.

### Paso 1: Obtener Contexto de Sesiones Anteriores

```markdown
mem_context("task-app")
```

**Resultado:** Engram te devuelve un resumen de lo que hiciste en sesiones anteriores:

- Session 15: Se implementó autenticación JWT
- Session 14: Fix de bug en delete de tareas
- Session 13: Se agregó filtro por status
- **Aprendizaje clave:** "Evitar usar useEffect para llamadas API, preferir React Query"

Ahora sabes que la autenticación ya está implementada y que hay un filtro por status. Perfecto para empezar.

### Paso 2: Iniciar un Nuevo Cambio con SDD

Tu jefe te pide que agregues la funcionalidad de exportar tareas a CSV. Ejecutas:

```markdown
/sdd:new export-csv-tasks
```

**El sistema responde:**

- 🕵️ **Explorer** analiza tu codebase y detecta: React frontend, Node.js backend, PostgreSQL database
- ✨ **Proposer** crea `proposal.md` con:
  - **Intent:** Agregar botón de exportar que genere CSV con todas las tareas del usuario
  - **Scope:** Backend endpoint + Frontend botón + Utilidad de conversión a CSV
  - **Riscos:** Manejo de caracteres especiales en CSV, gran cantidad de datos

### Paso 3: Revisar y Aprobar la Propuesta

Revisas la propuesta. Está bien, pero quieres agregar que también se exporten las subtareas. Aprobas con esa modificación y continuas:

```markdown
/sdd:continue
```

### Paso 4: Generación Automática de Specs y Design

El sistema ejecuta múltiples sub-agentes en paralelo:

- 📝 **Spec Writer** crea `specs/export-csv.md` con escenarios Given/When/Then
- 🎨 **Designer** crea `design.md` con decisiones técnicas
- 📋 **Task Planner** crea `tasks.md` con checklist de 8 tareas

**Ejemplo de lo que genera Spec Writer:**

```markdown
## ADDED Requirements

### Requirement: CSV Export
El sistema SHALL permitir exportar todas las tareas del usuario a formato CSV.

### Requirement: CSV Columns
El export SHALL incluir: título, descripción, fecha de creación, fecha de vencimiento, estado.

## MODIFIED Requirements

### Requirement: Task Data
Las tareas SHALL incluir campo de subtareas.
(Previously: Las tareas solo incluían título y descripción)
```

### Paso 5: Implementar las Tareas

Ejecutas la implementación:

```markdown
/sdd:apply
```

**Fase 1: Backend (3 tareas)**

- ✅ 1.1 Crear endpoint GET /api/tasks/export
- ✅ 1.2 Implementar utilería de conversión a CSV
- ✅ 1.3 Manejar caracteres especiales (comas, saltos de línea)

**El sistema se pausa** porque necesita tu confirmación para continuar.

### Paso 6: Guardar un Aprendizaje Importante

Durante la implementación, descubriste algo importante: las comas en los campos de texto rompen el CSV si no se encierran en comillas. Guarda este aprendizaje:

```markdown
mem_save(
  title: "CSV export: siempre usar quotes para campos con texto",
  type: "learning",
  content: """
    What: Descubrí que campos con comas rompen el CSV
    Why: El formato CSV estándar requiere que campos con comas vayan entre comillas
    Where: utils/csv.ts línea 15
    Learned: Usar siempre: "${campo.replace(/"/g, '""')}" para escapar comillas
  """,
  topic_key: "export-csv-tasks"
)
```

### Paso 7: Continuar con la Siguiente Fase

```markdown
/sdd:apply
```

**Fase 2: Frontend (5 tareas)**

- ✅ 2.1 Crear componente ExportButton
- ✅ 2.2 Agregar endpoint a API client
- ✅ 2.3 Implementar download del archivo
- ✅ 2.4 Agregar loading state
- ✅ 2.5 Mostrar toast de éxito/error

### Paso 8: Verificar la Implementación

Una vez completado, verificas que todo cumple con las specs:

```markdown
/sdd:verify
```

**Reporte del Verificador:**

| Estado | Cantidad | Descripción |
|--------|----------|-------------|
| ✅ PASS | 5 | Requisitos cumplidos |
| ⚠️ WARNING | 1 | El nombre del archivo debería incluir la fecha |
| 💡 SUGGESTION | 2 | Considerar agregar export de filtros actuales |

Corriges el warning manualmente y listas para cerrar.

### Paso 9: Cerrar el Cambio y Guardar Resumen de Sesión

```markdown
/sdd:archive
```

Ahora documentas lo que lograste hoy:

```markdown
mem_session_summary(
  goal: "Agregar funcionalidad de exportación CSV",
  discoveries: [
    "CSV requiere escape de comillas con doble comilla",
    "React Query maneja bien el blob download"
  ],
  accomplished: [
    "Endpoint de backend para /api/tasks/export",
    "Utilería de conversión a CSV",
    "Componente ExportButton en frontend",
    "Manejo de errores y estados de carga"
  ],
  files: [
    "backend/routes/tasks.js",
    "backend/utils/csv.js", 
    "frontend/components/ExportButton.tsx"
  ]
)
```

### Resumen del Flujo Completo

```
┌─────────────────────────────────────────────────────────────────┐
│                        DÍA COMPLETO                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  🌅 MAÑANA                                                      │
│  ┌──────────────────┐    ┌──────────────────┐                 │
│  │ mem_context()    │ →  │ /sdd:new         │                 │
│  │ (obtener pasado) │    │ export-csv-tasks │                 │
│  └──────────────────┘    └──────────────────┘                 │
│                                                                  │
│  ⏰ MEDIODÍA                                                    │
│  ┌──────────────────┐    ┌──────────────────┐                 │
│  │ /sdd:continue   │ →  │ /sdd:apply       │                 │
│  │ (specs+design)  │    │ (Fase 1: backend)│                 │
│  └──────────────────┘    └──────────────────┘                 │
│                                                                  │
│  🕐 DURANTE IMPLEMENTACIÓN                                      │
│  ┌──────────────────────────────────────────┐                   │
│  │ mem_save(title, type, "learning...")     │ ← GUARDAR        │
│  │ (aprender sobre escape de comillas CSV) │   INMEDIATAMENTE │
│  └──────────────────────────────────────────┘                   │
│                                                                  │
│  🌆 TARDE                                                       │
│  ┌──────────────────┐    ┌──────────────────┐                 │
│  │ /sdd:apply       │ →  │ /sdd:verify       │                 │
│  │ (Fase 2: frontend)   │ (validar vs specs)│                 │
│  └──────────────────┘    └──────────────────┘                 │
│                                                                  │
│  🌙 FIN DE DÍA                                                  │
│  ┌──────────────────┐    ┌──────────────────┐                 │
│  │ /sdd:archive     │ →  │ mem_session_     │                 │
│  │ (cerrar cambio)  │    │ summary()        │                 │
│  └──────────────────┘    └──────────────────┘                 │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Comandos Usados en Este Ejemplo

| Momento | Comando | Para qué |
|---------|---------|----------|
| MAÑANA | `mem_context("task-app")` | Recordar progreso anterior |
| MAÑANA | `/sdd:new export-csv-tasks` | Iniciar nuevo cambio |
| MEDIODÍA | `/sdd:continue` | Generar specs y design |
| MEDIODÍA | `/sdd:apply` | Implementar backend |
| IMPLEMENTACIÓN | `mem_save(...)` | Guardar aprendizaje |
| TARDE | `/sdd:apply` | Implementar frontend |
| TARDE | `/sdd:verify` | Validar contra specs |
| NOCHE | `/sdd:archive` | Cerrar cambio |
| NOCHE | `mem_session_summary(...)` | Documentar sesión |

---

<div align="center">

### 🎯 Guía Completa

¿Necesitas más detalles? Explora las secciones arriba o consulta la documentación oficial:

- [📚 Engram Docs](https://github.com/Gentleman-Programming/engram)
- [📚 Agent Teams Lite Docs](https://github.com/Gentleman-Programming/agent-teams-lite)

---

*Hecho con ❤️ para la comunidad de developers que usan AI*

</div>
