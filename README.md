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

| Sección | Descripción | ¿Para quién? |
|---------|-------------|--------------|
| [🎯 Primeros Pasos](#1-introducción) | Por qué usar estas herramientas juntas | Todos |
| [💾 Engram: Comandos Esenciales](#2-engram-tu-sistema-de-memoria-persistente) | Los 4 comandos que más usarás | Todos |
| [📦 Agent Teams Lite: Flujo SDD](#3-agent-teams-lite-desarrollo-dirigido-por-especificaciones) | Los 8 comandos del orquestador | Todos |
| [🔗 Integración con OpenCode](#4-integración-con-opencode) | Cómo activar ambas herramientas | Usuarios nuevos |
| [⚡ Cheat Sheet](#5-cheat-sheet-de-referencia-rápida) | **Todos los comandos en una tabla** | Todos |
| [📖 Glosario](#6-glosario-de-términos) | Términos técnicos explicados | Juniors |

> **💡 Tip:** Si ya sabes lo básico y solo necesitas recordar comandos, salta directo a la sección [⚡ Cheat Sheet](#5-cheat-sheet-de-referencia-rápida)

---

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

<div align="center">

### 🎯 Guía Completa

¿Necesitas más detalles? Explora las secciones arriba o consulta la documentación oficial:

- [📚 Engram Docs](https://github.com/Gentleman-Programming/engram)
- [📚 Agent Teams Lite Docs](https://github.com/Gentleman-Programming/agent-teams-lite)

---

*Hecho con ❤️ para la comunidad de developers que usan AI*

</div>
