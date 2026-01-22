# Lifecycle

NativePHP application lifecycle and event hooks.

## Application Boot Process

1. Electron shell starts
2. NativePHP runs `php artisan migrate`
3. NativePHP runs `php artisan serve`
4. `NativeAppServiceProvider::boot()` executes
5. `ApplicationBooted` event dispatched

## NativeAppServiceProvider

The service provider is where you configure your app:

```php
namespace App\Providers;

use Native\Desktop\Facades\Window;
use Native\Desktop\Facades\Menu;

class NativeAppServiceProvider
{
    public function boot(): void
    {
        // Configure windows, menus, shortcuts, etc.
        Window::open();
        Menu::default();
    }

    public function phpIni(): array
    {
        return [
            // PHP configuration
        ];
    }
}
```

## Application Events

### `ApplicationBooted`

Dispatched when application finishes booting:

```php
use Native\Desktop\Events\App\ApplicationBooted;

Event::listen(ApplicationBooted::class, function () {
    // Application is ready
});
```

## Window Lifecycle Events

- `WindowShown` - Window displayed
- `WindowClosed` - Window closed
- `WindowFocused` - Window gains focus
- `WindowBlurred` - Window loses focus
- `WindowMinimized` - Window minimized
- `WindowMaximized` - Window maximized
- `WindowResized` - Window resized (includes width, height)

## Application Shutdown

When the app quits:
- All child processes are gracefully terminated
- Queue workers stop
- Windows close

### Lifecycle Planning Format

For lifecycle hooks:

```
Lifecycle:
  Boot:
    - {action}: {when/where}
    - Event Listener: {EventClass} → {Handler}
  
  Runtime:
    - {action}: {triggered-by}
    - Event Listener: {EventClass} → {Handler}
  
  Shutdown:
    - {cleanup-action}
```
