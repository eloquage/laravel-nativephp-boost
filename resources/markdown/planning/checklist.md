# Common Planning Mistakes

> **For planning agents**: Review this checklist before finalizing your plan.

## Vague Specifications

| Bad | Good |
|-----|------|
| "Add a window" | Full window spec: ID, route, size, position, title, features |
| "Configure menu" | Complete menu structure with all items, hotkeys, events |
| "System tray icon" | MenuBar spec: icon path, label, route, context menu |
| "Send notification" | Notification spec: title, message, event, actions |

## Missing Namespaces

Every element MUST have full namespace.

| Element | Pattern |
|---------|---------|
| Service Provider | `App\Providers\NativeAppServiceProvider` |
| Facades | `Native\Desktop\Facades\{Facade}` |
| Events | `Native\Desktop\Events\{Category}\{Event}` |
| Models | `App\Models\{Model}` |

## Missing Window Elements

- [ ] Window ID specified
- [ ] Route or URL specified
- [ ] Size (width, height) specified
- [ ] Title specified (or uses default)
- [ ] Features specified (resizable, movable, etc.)

## Missing Menu Elements

- [ ] Menu type specified (Application/Context/MenuBar)
- [ ] All menu items listed
- [ ] Menu item actions specified (route/event)
- [ ] Hotkeys specified (if applicable)
- [ ] Platform-specific considerations noted

## Security Gaps

- [ ] Sensitive data not encrypted
- [ ] External URLs not validated
- [ ] Child process commands not sanitized
- [ ] Settings storage for sensitive data
- [ ] File permissions not considered

## System Integration Unclear

For each system feature:

- [ ] Facade specified correctly
- [ ] Configuration options specified
- [ ] Events to listen for specified
- [ ] Platform limitations noted (macOS/Windows/Linux)

## Missing Tests

- [ ] No window operation tests
- [ ] No menu action tests
- [ ] No notification tests
- [ ] No facade fake assertions

## Window Management Issues

| Wrong | Right |
|-------|-------|
| Window opened without ID | Window ID specified (or 'main' as default) |
| Route not specified | `->route('named-route')` or `->url('/path')` |
| Size not specified | `->width(800)->height(600)` |
| Multiple windows without IDs | Unique ID for each window |

## Menu Configuration Issues

| Wrong | Right |
|-------|-------|
| Menu items without actions | Each item has route/event specified |
| Hotkeys without modifiers | `'Ctrl+K'` or `'Cmd+K'` format |
| Context menu not configured | JavaScript code for context menus specified |

## Notification Issues

- [ ] Missing title
- [ ] Missing event for click handling
- [ ] Platform-specific features (actions, reply) not noted

## File Operation Issues

- [ ] Storage disk not specified
- [ ] File paths not platform-agnostic
- [ ] Bundled files location not specified

## Final Verification

Before submitting:

- [ ] All windows have IDs, routes, sizes
- [ ] All menus have complete structure
- [ ] All facades include full namespaces
- [ ] All events include full namespaces
- [ ] Platform-specific features noted
- [ ] Security considerations addressed
- [ ] Test specifications included
