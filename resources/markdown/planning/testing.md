# Testing

Testing NativePHP applications using fake test doubles.

## Fake Test Doubles

NativePHP facades can be faked in tests to avoid requiring Electron to be running:

```php
use Native\Desktop\Facades\Window;

Window::fake();

Window::assertOpened('window-name');
```

## Available Fakes

Common facades that support `fake()`:

- `Window::fake()`
- `Menu::fake()`
- `Notification::fake()`
- `MenuBar::fake()`
- `GlobalShortcut::fake()`
- `Clipboard::fake()`
- `ChildProcess::fake()`
- `Settings::fake()`

## Assertion Methods

Each facade provides assertion methods:

```php
Window::assertOpened($windowId);
Window::assertClosed($windowId);
Window::assertResized($windowId, $width, $height);

Notification::assertSent($title);
Notification::assertSentCount($count);

MenuBar::assertShown();
MenuBar::assertHidden();

GlobalShortcut::assertRegistered($key);
GlobalShortcut::assertUnregistered($key);
```

## Testing Patterns

### Testing Window Operations

```php
Window::fake();

Window::open('main')
    ->route('dashboard');

Window::assertOpened('main');
```

### Testing Notifications

```php
Notification::fake();

Notification::title('Test')
    ->message('Message')
    ->show();

Notification::assertSent('Test');
```

### Testing Menu Actions

```php
Menu::fake();

Event::fake([MenuItemClicked::class]);

// Trigger menu item click
// ...

Event::assertDispatched(MenuItemClicked::class);
```

### Testing Settings

```php
Settings::fake();

Settings::set('theme', 'dark');

expect(Settings::get('theme'))->toBe('dark');
```

## Testing Planning Format

For test specifications:

```
Tests:
  - {test-name}: {what-to-test}
    Fake: {facade-to-fake}
    Assert: {assertion-methods}
    Events: {events-to-listen-for}
```
