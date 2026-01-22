# System Integration

NativePHP provides access to system-level features like notifications, clipboard, global shortcuts, system tray, and power monitoring.

## System Tray

The system tray (menu bar on macOS/Linux) allows your app to run in the background with a tray icon.

### Menu Bar Applications

```php
use Native\Desktop\Facades\MenuBar;

MenuBar::create()
    ->icon(storage_path('app/menuBarIcon.png'))
    ->label('Status: Online')
    ->tooltip('Click to open')
    ->route('dashboard');
```

### Menu Bar Configuration

Specify:
- Icon path (PNG, transparent background, 22x22px, with @2x for retina)
- Label (optional, text next to icon)
- Tooltip (hover text)
- Route/URL (window to open on click)
- Window size (width, height)
- Context menu (optional)

### Menu Bar Events

- `Native\Desktop\Events\MenuBar\MenuBarShown` - Menu bar window opened
- `Native\Desktop\Events\MenuBar\MenuBarHidden` - Menu bar window closed
- `Native\Desktop\Events\MenuBar\MenuBarContextMenuOpened` - Context menu opened

### Menu Bar Only Mode

Show only context menu without window:

```php
MenuBar::create()
    ->onlyShowContextMenu();
```

## Notifications

Native system notifications using `Native\Desktop\Facades\Notification`.

### Sending Notifications

```php
Notification::title('Task Complete')
    ->message('Your background task has finished')
    ->show();
```

### Notification Configuration

- `title($title)` - Notification title
- `message($message)` - Notification body
- `event($eventClass)` - Event fired on click
- `reference($ref)` - Unique reference for tracking
- `sound($sound)` - System sound name or file path
- `silent()` - No sound
- `hasReply($placeholder)` - Enable reply (macOS only)
- `addAction($label)` - Add action button (macOS only)

### Notification Events

- `Native\Desktop\Events\Notifications\NotificationClicked` - User clicked notification
- `Native\Desktop\Events\Notifications\NotificationClosed` - User closed notification
- `Native\Desktop\Events\Notifications\NotificationReply` - User replied (macOS)
- `Native\Desktop\Events\Notifications\NotificationActionClicked` - User clicked action button

## Clipboard

Access system clipboard using `Native\Desktop\Facades\Clipboard`.

### Clipboard Operations

```php
// Read
$text = Clipboard::text();
$html = Clipboard::html();
$image = Clipboard::image();

// Write
Clipboard::text('Copied text');
Clipboard::html('<div>HTML</div>');
Clipboard::image('path/to/image.png');

// Clear
Clipboard::clear();
```

## Global Shortcuts

Register system-wide keyboard shortcuts using `Native\Desktop\Facades\GlobalShortcut`.

### Registering Shortcuts

```php
GlobalShortcut::key('CmdOrCtrl+Shift+A')
    ->event(MyShortcutEvent::class)
    ->register();
```

### Unregistering Shortcuts

```php
GlobalShortcut::key('CmdOrCtrl+Shift+A')
    ->unregister();
```

### Available Modifiers

- `Command` / `Cmd`
- `Control` / `Ctrl`
- `CommandOrControl` / `CmdOrCtrl`
- `Alt`
- `Option`
- `AltGr`
- `Shift`
- `Super`
- `Meta`

### Available Keys

Numbers (`0-9`), Letters (`A-Z`), Function keys (`F1-F24`), Arrow keys, Media keys, etc.

## Power Monitor

Monitor system power state using `Native\Desktop\Facades\PowerMonitor`.

### Power State Methods

```php
// Check if on battery
PowerMonitor::isOnBatteryPower();

// Get idle state
$state = PowerMonitor::getSystemIdleState(60); // seconds threshold

// Get idle time
$seconds = PowerMonitor::getSystemIdleTime();

// Get thermal state
$thermal = PowerMonitor::getCurrentThermalState();
```

### Power Monitor Events

- `Native\Desktop\Events\PowerStateChanged` - Power state changed (battery/AC)
- `Native\Desktop\Events\SpeedLimitChanged` - CPU speed limit changed
- `Native\Desktop\Events\ThermalStateChanged` - Thermal state changed

## Screens

Get display information using `Native\Desktop\Facades\Screen`.

```php
// Get all displays
$displays = Screen::displays();

// Get cursor position
$position = Screen::cursorPosition();
```

## System Facade

Access system features using `Native\Desktop\Facades\System`.

### System Methods

- `System::canEncrypt()` - Check encryption availability
- `System::encrypt($data)` - Encrypt data
- `System::decrypt($encrypted)` - Decrypt data
- `System::canPromptTouchID()` - Check TouchID availability (macOS)
- `System::promptTouchID($reason)` - Prompt TouchID (macOS)
- `System::printers()` - List available printers
- `System::print($html, $printer, $settings)` - Print HTML
- `System::printToPDF($html)` - Generate PDF from HTML
- `System::timezone()` - Get system timezone
- `System::theme()` - Get/set system theme (light/dark)

### System Planning Format

For each system integration feature:

```
System Feature: {feature-name}
  Facade: {FacadeName}
  Configuration:
    - {setting}: {value}
  Events:
    - {EventClass}: {when-fired}
  Platform: All / macOS / Windows / Linux
```
