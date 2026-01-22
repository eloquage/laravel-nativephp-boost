# Menus

NativePHP applications use native menus through the `Menu` facade. Menus can be application menus, context menus, or menu bar menus.

## Menu Configuration

Menus are configured in `NativeAppServiceProvider::boot()` using the `Native\Desktop\Facades\Menu` facade.

### Creating Application Menus

```php
use Native\Desktop\Facades\Menu;

Menu::create(
    Menu::app(),     // macOS only
    Menu::file(),
    Menu::edit(),
    Menu::view(),
    Menu::window(),
);
```

Or use the default menu:

```php
Menu::default();
```

### Menu Types

**Application Menu**: Main menu bar (macOS/Windows/Linux)

**Context Menu**: Right-click menus on specific elements (configured via JavaScript)

**Menu Bar Menu**: Menu bar icon context menu (macOS/Linux)

### Predefined Menus

NativePHP provides predefined menus:

- `Menu::app()` - Application menu (macOS only)
- `Menu::file()` - File menu
- `Menu::edit()` - Edit menu (cut, copy, paste, undo, redo)
- `Menu::view()` - View menu (fullscreen, dev tools)
- `Menu::window()` - Window menu (minimize, zoom, etc.)

You can customize labels:

```php
Menu::edit('My Edit Menu');
```

### Custom Menus

Create custom menus using `Menu::make()`:

```php
Menu::make(
    Menu::label('Support'),
    Menu::separator(),
    Menu::link('https://example.com', 'Documentation'),
)
->label('Help');
```

### Menu Items

Available menu item types:

- `Menu::label($label, $hotkey = null)` - Clickable label
- `Menu::link($url, $label = null, $hotkey = null)` - Navigate to URL
- `Menu::route($route, $label = null, $hotkey = null)` - Navigate to route
- `Menu::checkbox($label, $checked = false, $hotkey = null)` - Checkbox item
- `Menu::radio($label, $checked = false, $hotkey = null)` - Radio item
- `Menu::separator()` - Visual separator

### Menu Item Configuration

Each menu item supports:

- `->label($label)` - Set label
- `->id($id)` - Set unique ID
- `->icon($path)` - Set icon (absolute path)
- `->visible($bool)` - Show/hide
- `->tooltip($text)` - Tooltip (macOS only)
- `->hotkey($key)` - Keyboard shortcut
- `->disabled($bool)` - Enable/disable
- `->event($eventClass)` - Custom event on click

### Handling Menu Clicks

Menu items fire events when clicked:

**Default Event**: `Native\Desktop\Events\Menu\MenuItemClicked`

**Custom Event**: Specify using `->event($eventClass)`

Events are broadcast to the `nativephp` channel and can be listened to in Laravel or JavaScript.

### Hotkeys

Define keyboard shortcuts for menu items:

```php
Menu::label('Quick Search')
    ->hotkey('Ctrl+K'); // or 'Cmd+K' for macOS
```

Available modifiers: `Cmd`, `Ctrl`, `CmdOrCtrl`, `Alt`, `Option`, `Shift`, `Super`, `Meta`

Menu item hotkeys only work when application windows are focused.

### Special Menu Items

- `Menu::undo()` - Undo action
- `Menu::redo()` - Redo action
- `Menu::cut()` - Cut action
- `Menu::copy()` - Copy action
- `Menu::paste()` - Paste action
- `Menu::fullscreen()` - Toggle fullscreen
- `Menu::minimize()` - Minimize window
- `Menu::quit()` - Quit application

### Context Menus

Context menus are created using JavaScript in your views:

```js
Native.contextMenu([
    {
        label: 'Edit',
        accelerator: 'e',
        click(menuItem, window, event) {
            // Handle click
        },
    },
]);
```

### Menu Bar Context Menu

Add a context menu to menu bar icon:

```php
MenuBar::create()
    ->withContextMenu(
        Menu::make(
            Menu::label('My App'),
            Menu::separator(),
            Menu::quit()
        )
    );
```

### Dynamic Menu Updates

You can update the application menu at any time by calling `Menu::create()` again. Useful for context-sensitive menus.

### Menu Planning Format

For each menu in your plan, specify:

```
Menu: {menu-name}
  Type: Application / Context / MenuBar
  Items:
    - {item-type}: {label} [hotkey: {key}] [event: {event-class}]
    - separator
    - {item-type}: {label}
  Platform: All / macOS / Windows / Linux
```
