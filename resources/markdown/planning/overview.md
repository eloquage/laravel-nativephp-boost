# Plan Structure

> **For planning agents**: Your plan is the ONLY thing the implementing agent
> sees. Copy all relevant information from the guideline files into your plan.
> The implementing agent cannot access these files—if something isn't in your
> plan, they won't know it.

Your plan is a specification document for an implementing agent. It must be
complete enough that the implementing agent can write code without making
decisions.

## Before You Plan

Ask the user to clarify ambiguities before producing the plan. Don't guess.

| If the request mentions... | Ask about... |
| -------------------------- | ---------------------------------------------- |
| "Multiple windows" | Window IDs? Size/position? Window relationships? |
| "System tray icon" | Show/hide on startup? Context menu items? |
| "Global shortcuts" | Which shortcuts? Which actions? Platform-specific? |
| "File operations" | File dialogs or direct file access? User data directory? |
| "Notifications" | When to show? Click actions? Persistence? |
| "Settings storage" | User preferences? Application config? Persistent across sessions? |
| "Child processes" | Long-running? One-time commands? Alternatives (queues)? |
| "Auto-start" | All platforms? User permission required? |

**When to ask vs proceed:**

- Ask when the answer affects window configuration or system integration
- Ask when there are multiple valid approaches with different tradeoffs
- Proceed when the choice is cosmetic or easily changed later

## Verifying Syntax

Before finalizing your plan, verify configuration methods using search-docs:

| Verify | How |
| ----------------------- | ----------------------------------------- |
| Facade methods | Check [windows.md], [menus.md], [system-integration.md] |
| Window lifecycle | Check [lifecycle.md] |
| Service provider | Check NativePHP documentation |
| Configuration | Search NativePHP configuration docs |

**Keep URLs in plans**: After verifying, include documentation URLs as backup
references. Don't replace URLs with "search for X" - implementing agents need
direct links.

## Planning Order

Build your plan in this order:

1. **Models first** - Define tables, attributes, relationships (if using database)
2. **Service Provider second** - NativeAppServiceProvider configuration
3. **Windows third** - Window definitions, IDs, routes, lifecycle
4. **Menus fourth** - Application menus, context menus, menu bar
5. **System Integration fifth** - Tray, notifications, shortcuts, clipboard
6. **Features sixth** - Dialogs, child processes, queues, file operations
7. **Authorization seventh** - Security, permissions (if applicable)
8. **Tests last** - Test what you've specified above

This order ensures you don't reference things that aren't yet defined.

## Required Formats

Every plan element MUST include these lines. Do not omit any.

**Window**: ID, Route/URL, Size, Position, Title, Configuration (with full namespace)

**Menu Item**: Label, Action (facade method/route), Submenu (if applicable), Platform-specific

**Facade Method Call**: Facade Name, Method, Parameters, Return Type, When/Where Called

**Service Provider Method**: Method Name, Parameters, Return Type, Logic Description

### Why Namespaces Matter

The implementing agent uses namespaces to write correct imports.

**Always include full namespaces**:

| Element | Namespace Pattern |
| -------------- | ----------------------------------------- |
| Service Provider | `App\Providers\NativeAppServiceProvider` |
| Models | `App\Models\{Model}` |
| Facades | `Native\Desktop\Facades\{Facade}` |
| Routes | `routes/web.php` or specific route files |

## New vs Update Plans

| Scenario | Commands | Specifications |
| --------------- | ------------------------ | -------------------------------- |
| New window | Configure in NativeAppServiceProvider | Full specification |
| Update window | Modify in NativeAppServiceProvider | Only changes (Add/Modify/Remove) |
| New menu | Configure in NativeAppServiceProvider | Full specification |
| Update menu | Modify in NativeAppServiceProvider | Only changes (Add/Modify/Remove) |
| New model | Create migration | Full attributes |
| Update model | Alter migration | Only changed attributes |

## Required Sections

Every plan needs these sections:

### 1. Commands

List every artisan command to run before writing code (e.g., migrations, config publishing).

### 2. Models (if applicable)

Define every model with exact attributes and relationships. See Laravel docs.

### 3. Service Provider Configuration

Specify NativeAppServiceProvider setup: windows, menus, system integration. See [windows.md], [menus.md], [system-integration.md].

### 4. Windows

Define every window: ID, route, size, position, title, configuration. See [windows.md].

### 5. Menus

Define application menus, context menus, menu bar. See [menus.md].

### 6. System Integration

Specify system tray, notifications, global shortcuts, clipboard. See [system-integration.md].

### 7. Features

Define dialogs, child processes, queues, file operations, settings. See respective guides.

### 8. Authorization (if applicable)

Describe who can do what. See [security.md].

### 9. Tests

List what to test. See [testing.md].

## File Directory

| File | Purpose |
| --------------------- | ---------------------------------------- |
| [overview.md] | Plan structure and required sections |
| [windows.md] | Window management, lifecycle, IDs |
| [menus.md] | Application menus, context menus, menu bar |
| [system-integration.md] | System tray, notifications, clipboard, shortcuts |
| [dialogs.md] | Native dialogs, file/folder pickers, message boxes |
| [child-processes.md] | Process spawning, management, alternatives |
| [queues.md] | Queue workers in native context |
| [databases.md] | SQLite configuration, migrations, paths |
| [files.md] | File system operations, user data directories |
| [settings.md] | Application settings, persistence |
| [broadcasting.md] | Broadcasting patterns in native apps |
| [lifecycle.md] | Application boot, shutdown, event hooks |
| [security.md] | Security considerations, permissions |
| [testing.md] | Testing strategies for native apps |
| [publishing.md] | Building, cross-compilation, updater providers |
| [checklist.md] | Common mistakes to avoid |
| [troubleshooting.md] | Diagnostic checks for common issues |

## When You're Stuck

| Situation | What to do |
| ---------------------------------- | -------------------------------------------- |
| Requirements contradict each other | Ask user which takes priority |
| Feature seems impossible | Ask user if you understood correctly |
| Multiple valid approaches | Explain tradeoffs, ask user to choose |
| Missing critical information | Ask user (see "Before You Plan" above) |
| Request is too large | Propose splitting into phases, confirm scope |
| Platform-specific differences | Clarify which platforms must be supported |

Don't guess on window configuration or system integration decisions.

## Before Finalizing

**You must review [checklist.md] before submitting your plan.**
