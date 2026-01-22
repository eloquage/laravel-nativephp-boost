# Windows

Windows are the primary UI containers in NativePHP applications. Each window displays Laravel routes and can be configured independently.

## Window Management

Windows are managed using the `Native\Desktop\Facades\Window` facade in your `NativeAppServiceProvider`.

### Opening Windows

The `Window::open()` method opens a new window. Each window must have a unique ID (defaults to `main`).

```php
use Native\Desktop\Facades\Window;

Window::open('main')
    ->width(800)
    ->height(600)
    ->route('dashboard');
```

### Window IDs

Every window must have a unique identifier. Use IDs to reference windows for operations like close, resize, or URL changes.

- Default ID: `main` (if not specified)
- Must be unique across all windows
- Used for all window operations

### Window Configuration

When specifying window configuration in your plan, include:

**Required**:
- Window ID (string)
- Route or URL (string)
- Width (integer)
- Height (integer)

**Optional but Important**:
- Title (string, defaults to app name)
- Position (x, y coordinates)
- Min/max width/height
- Resizable (boolean, default: true)
- Movable (boolean, default: true)
- Minimizable/maximizable/closable (boolean, default: true)
- Always on top (boolean)
- Remember state (boolean)
- Fullscreen (boolean)
- Background color (hex string)
- Title bar style (hidden, traffic lights hidden)

### Window Methods

Common window operations to specify in plans:

- `Window::open($id)` - Open a window
- `Window::close($id)` - Close a window
- `Window::resize($width, $height, $id)` - Resize a window
- `Window::minimize($id)` - Minimize a window
- `Window::maximize($id)` - Maximize a window
- `Window::focus($id)` - Focus a window
- `Window::get($id)->url($url)` - Change window URL
- `Window::get($id)->title($title)` - Change window title
- `Window::current()` - Get current focused window
- `Window::all()` - Get all open windows

### Window Routes

Specify how windows connect to Laravel routes:

```php
Window::open('settings')
    ->route('settings'); // Uses named route

Window::open('about')
    ->url('/about'); // Uses absolute URL path
```

### Window Events

NativePHP dispatches window events that can be listened to:

- `Native\Desktop\Events\Windows\WindowShown` - Window is shown
- `Native\Desktop\Events\Windows\WindowClosed` - Window is closed
- `Native\Desktop\Events\Windows\WindowFocused` - Window gains focus
- `Native\Desktop\Events\Windows\WindowBlurred` - Window loses focus
- `Native\Desktop\Events\Windows\WindowMinimized` - Window is minimized
- `Native\Desktop\Events\Windows\WindowMaximized` - Window is maximized
- `Native\Desktop\Events\Windows\WindowResized` - Window is resized (includes width, height)

### Multiple Windows

When planning applications with multiple windows:

1. **List each window separately** with its ID, purpose, route, and configuration
2. **Specify window relationships** - Which windows open from others?
3. **Define window lifecycle** - When are windows created? Closed?
4. **Consider window state** - Should windows remember position/size?

### Window Planning Format

For each window in your plan, specify:

```
Window: {window-id}
  Route: {route-name} or URL: {path}
  Size: {width}x{height}
  Position: ({x}, {y}) or centered
  Title: {title}
  Features: resizable, movable, minimizable, maximizable, closable
  Special: alwaysOnTop, rememberState, fullscreen, etc.
```

### Common Patterns

**Main Application Window**:
```php
Window::open('main')
    ->width(1200)
    ->height(800)
    ->route('dashboard')
    ->rememberState();
```

**Settings Window**:
```php
Window::open('settings')
    ->width(600)
    ->height(500)
    ->route('settings')
    ->resizable(false);
```

**Modal/Utility Window**:
```php
Window::open('quick-note')
    ->width(400)
    ->height(300)
    ->route('quick-note')
    ->alwaysOnTop()
    ->skipTaskbar();
```
