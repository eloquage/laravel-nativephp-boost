# Dialogs

Native file and folder dialogs using `Native\Desktop\Dialog`.

## File Dialogs

### Opening Files

```php
use Native\Desktop\Dialog;

$file = Dialog::new()
    ->title('Select a file')
    ->open();
```

### Saving Files

```php
$path = Dialog::new()
    ->title('Save file')
    ->save();
```

Note: `save()` returns the path - you must write the file yourself.

### Dialog Configuration

- `title($title)` - Dialog title
- `button($label)` - Button label (default: "Open"/"Save")
- `defaultPath($path)` - Initial directory
- `filter($name, $extensions)` - File type filter
- `multiple()` - Allow multiple selection
- `showHiddenFiles()` / `withHiddenFiles()` - Show hidden files
- `dontResolveSymlinks()` - Don't resolve symlinks
- `folders()` - Select folders instead of files
- `asSheet($windowId)` - Attach to window as sheet (macOS)

### File Filters

```php
Dialog::new()
    ->filter('Images', ['jpg', 'png', 'gif'])
    ->filter('Documents', ['pdf', 'docx'])
    ->open();
```

### Multiple File Selection

```php
$files = Dialog::new()
    ->multiple()
    ->open(); // Returns array of paths
```

### Dialog Planning Format

For each dialog:

```
Dialog: {purpose}
  Type: Open / Save / Folder
  Title: {title}
  Default Path: {path} or null
  Filters:
    - {name}: [{extensions}]
  Options: multiple, hidden files, etc.
  Sheet: {window-id} or null
```
