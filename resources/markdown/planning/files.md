# Files

File system operations in NativePHP applications.

## Storage Paths

NativePHP rewrites `storage_path()` to point to Electron's `appdata` directory.

### Default Storage

- `storage_path()` → `appdata` directory
- `Storage::disk('local')` → `appdata/storage/app`

### User Directory Disks

NativePHP provides convenient filesystem disks:

- `user_home` - User's home directory
- `desktop` - Desktop directory
- `documents` - Documents directory
- `downloads` - Downloads directory
- `music` - Music directory
- `pictures` - Pictures directory
- `videos` - Videos directory
- `recent` - Recent files
- `extras` - Bundled application files (read-only)

### Using Storage Disks

```php
use Illuminate\Support\Facades\Storage;

// User directories
Storage::disk('desktop')->put('file.txt', $content);
Storage::disk('documents')->get('file.txt');

// App data (default)
Storage::put('config.json', $content);

// Bundled files (read-only)
$toolPath = Storage::disk('extras')->path('my-tool.exe');
```

### Bundling Files

Place files in `extras/` directory at project root:

```
extras/
  ├── my-tool.sh
  ├── my-tool.exe
  └── sample.csv
```

Access via `Storage::disk('extras')`. Files are read-only and bundled with the app.

### File Planning Format

For file operations:

```
Files: {description}
  Storage Location: {disk-name} or {path}
  Operations: read / write / delete
  Bundled: yes / no
  Platform Considerations: {path-differences}
```
