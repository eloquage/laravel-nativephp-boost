# Settings

Application settings persistence using `Native\Desktop\Facades\Settings`.

## Settings Storage

Settings are stored in `appdata/config.json` and persist across app sessions.

### Setting Values

```php
use Native\Desktop\Facades\Settings;

Settings::set('key', 'value');
Settings::set('theme', 'dark');
Settings::set('window_width', 1200);
```

### Getting Values

```php
$value = Settings::get('key');
$theme = Settings::get('theme', 'light'); // with default
$width = Settings::get('window_width', function() {
    return 800; // default via closure
});
```

### Removing Values

```php
Settings::forget('key');
Settings::clear(); // Remove all settings
```

### Settings Events

Listen for changes:

```php
use Native\Desktop\Events\Notifications\SettingChanged;

Event::listen(SettingChanged::class, function (SettingChanged $event) {
    $key = $event->key;
    $value = $event->value;
});
```

### Settings Planning Format

For application settings:

```
Settings:
  - {key}: {type} [default: {value}]
  - {key}: {type} [default: {value}]
  
Events: {listen-to-SettingChanged}
```
