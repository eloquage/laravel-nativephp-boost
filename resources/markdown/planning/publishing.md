# Publishing

Building and publishing NativePHP applications for distribution.

## Building

Build your app for production:

```bash
php artisan native:build
```

### Cross-Compilation

Build for different platforms:

```bash
php artisan native:build mac
php artisan native:build win
php artisan native:build linux
```

**Note**: Cross-compilation not supported on all platforms.

### Build Hooks

Configure pre/post build commands in `config/nativephp.php`:

```php
'prebuild' => [
    'npm run build',
    'php artisan optimize',
],
'postbuild' => [
    'npm run release',
],
```

## Versioning

Update version in `config/nativephp.php` before each build:

```php
'version' => '1.2.3',
```

**Important**: Migrations only run if version changed.

## Code Signing

### macOS

Requires Apple Developer credentials:

```env
NATIVEPHP_APPLE_ID=developer@example.com
NATIVEPHP_APPLE_ID_PASS=app-specific-password
NATIVEPHP_APPLE_TEAM_ID=XXXXXXXXXX
```

### Windows

Two methods:
1. **Azure Trusted Signing** (recommended) - cloud-based
2. **Traditional Certificate** - local certificate

## Publishing

Publish builds with automatic uploads:

```bash
php artisan native:publish
```

This builds and uploads to your configured updater provider.

### Updater Providers

- GitHub Releases (`github`)
- Amazon S3 (`s3`)
- DigitalOcean Spaces (`spaces`)

### Updater Configuration

Configure in `config/nativephp.php`:

```php
'updater' => [
    'enabled' => true,
    'default' => 'github',
    'providers' => [
        'github' => [
            'driver' => 'github',
            'repo' => env('GITHUB_REPO'),
            'owner' => env('GITHUB_OWNER'),
            'token' => env('GITHUB_TOKEN'),
        ],
        // ... other providers
    ],
],
```

## Publishing Planning Format

For publishing configuration:

```
Publishing:
  Platforms: {mac/win/linux}
  Version: {version-scheme}
  Code Signing: {method/credentials}
  Updater Provider: {provider-name}
  Build Hooks:
    Pre: [{commands}]
    Post: [{commands}]
```
