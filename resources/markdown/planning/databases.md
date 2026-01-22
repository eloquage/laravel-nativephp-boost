# Databases

NativePHP uses SQLite by default for local data storage.

## SQLite Configuration

NativePHP automatically:
- Switches to SQLite when building
- Creates database in `appdata` directory
- Runs migrations on app startup
- Handles database path management

### Development vs Production

**Development**: Database in build directory (`nativephp.sqlite`)

**Production**: Database in user's `appdata` directory

### Migrations

Migrations run automatically on app startup if version changed.

Manual migration commands:

```bash
php artisan native:migrate
php artisan native:migrate:fresh  # Destructive!
php artisan native:seed
```

### SQLite Considerations

When planning database features:

- Foreign key constraints must be enabled (Laravel 11+ does this automatically)
- Test migrations on production builds before release
- Consider file storage for critical metadata (separate from user data)

### Database Planning Format

```
Database: SQLite
  Location: appdata/database/database.sqlite
  Migrations: {run-on-startup}
  Seeders: {seeder-classes}
  Foreign Keys: {enabled/disabled}
```
