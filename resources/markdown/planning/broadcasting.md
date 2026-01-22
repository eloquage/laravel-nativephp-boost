# Broadcasting

Event broadcasting in NativePHP for real-time communication between Laravel and JavaScript.

## Broadcasting Channels

NativePHP uses the `nativephp` broadcast channel for all native events.

### Custom Events

Broadcast your own events:

```php
use Illuminate\Broadcasting\Channel;
use Illuminate\Contracts\Broadcasting\ShouldBroadcastNow;

class JobFinished implements ShouldBroadcastNow
{
    public function broadcastOn(): array
    {
        return [
            new Channel('nativephp'),
        ];
    }
}
```

### Listening in JavaScript

```js
window.addEventListener('native:init', () => {
    Native.on('Native\\Desktop\\Events\\Windows\\WindowBlurred', (payload, event) => {
        // Handle event
    });
});
```

### Listening with Livewire

Use the `native:` prefix:

```php
use Livewire\Attributes\On;
use Native\Desktop\Events\Windows\WindowFocused;

class AppSettings extends Component
{
    #[On('native:'.WindowFocused::class)]
    public function windowFocused()
    {
        // Handle event
    }
}
```

### Native Events

All NativePHP events are automatically broadcast to the `nativephp` channel:

- Window events (WindowShown, WindowClosed, WindowFocused, etc.)
- Menu events (MenuItemClicked)
- Notification events (NotificationClicked, NotificationActionClicked)
- MenuBar events (MenuBarShown, MenuBarHidden)
- Power events (PowerStateChanged, ThermalStateChanged)
- Settings events (SettingChanged)

### Broadcasting Planning Format

For events:

```
Events:
  - {EventClass}: {when-fired} [payload: {properties}]
  
Listeners:
  - JavaScript: {event-class} → {callback}
  - Livewire: {component} → {method}
  - Laravel: {listener-class}
```
