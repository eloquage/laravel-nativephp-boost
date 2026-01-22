# Troubleshooting

Common issues and diagnostic checks for NativePHP applications.

## Window Not Opening

**Symptoms**: Window doesn't appear when app starts.

**Checks**:
- [ ] `Window::open()` called in `NativeAppServiceProvider::boot()`
- [ ] Window ID is unique (if multiple windows)
- [ ] Route exists and is accessible
- [ ] Check application logs for errors

**Fix**: Verify window configuration in service provider, check route registration.

## Menu Not Appearing

**Symptoms**: Application menu not visible.

**Checks**:
- [ ] `Menu::create()` called in `NativeAppServiceProvider::boot()`
- [ ] On Windows/Linux, menu may be hidden (use ALT to reveal)
- [ ] Menu items have valid routes/actions

**Fix**: Verify menu configuration, check platform-specific behavior.

## Notification Not Showing

**Symptoms**: Notifications don't appear.

**Checks**:
- [ ] System notification permissions granted (especially macOS)
- [ ] Notification title and message set
- [ ] App not in background/do-not-disturb mode

**Fix**: Check system notification settings, ensure permissions granted.

## Global Shortcuts Not Working

**Symptoms**: Keyboard shortcuts don't trigger.

**Checks**:
- [ ] Shortcut registered in `NativeAppServiceProvider::boot()`
- [ ] Shortcut format correct (`CmdOrCtrl+K`)
- [ ] No conflicts with system shortcuts
- [ ] App has focus (global shortcuts work even when unfocused)

**Fix**: Verify shortcut registration, check for conflicts.

## Database Migration Fails

**Symptoms**: App crashes on startup, migration errors.

**Checks**:
- [ ] SQLite foreign keys enabled (Laravel 11+ auto-enabled)
- [ ] Migration syntax valid for SQLite
- [ ] Database file writable in appdata directory

**Fix**: Test migrations on SQLite, enable foreign keys if needed.

## Files Not Accessible

**Symptoms**: File operations fail, paths incorrect.

**Checks**:
- [ ] Using `storage_path()` for appdata directory
- [ ] Using correct Storage disk (`desktop`, `documents`, etc.)
- [ ] Platform-specific path differences considered
- [ ] File permissions correct

**Fix**: Use NativePHP storage disks, verify paths are platform-agnostic.

## Child Process Fails

**Symptoms**: Process doesn't start or errors.

**Checks**:
- [ ] Full path to executable provided
- [ ] Platform-specific command differences (Windows vs Unix)
- [ ] Process alias unique
- [ ] Command syntax correct for platform

**Fix**: Use full paths, handle platform differences.

## Build Fails

**Symptoms**: `native:build` command fails.

**Checks**:
- [ ] Version updated in config
- [ ] Pre-build hooks succeed (npm build, etc.)
- [ ] Code signing credentials valid (for signing)
- [ ] Dependencies installed

**Fix**: Run pre-build commands manually, verify configuration.

## Updates Not Working

**Symptoms**: Auto-updater doesn't check/download updates.

**Checks**:
- [ ] Updater enabled in config
- [ ] Provider credentials configured correctly
- [ ] App running in production mode
- [ ] Version number changed for new release

**Fix**: Verify updater configuration, check provider setup.

## Diagnostic Commands

```bash
# Clear caches
php artisan optimize:clear

# Check NativePHP config
php artisan config:show nativephp

# Run migrations manually
php artisan native:migrate

# Seed database
php artisan native:seed
```

## Debugging Tips

- Check `storage/logs/laravel.log` for errors
- Use `php artisan tinker` to test facade methods
- Enable verbose logging in development
- Test on target platforms (don't assume cross-platform compatibility)
