# Security

Security considerations for NativePHP desktop applications.

## File System Permissions

NativePHP runs with the same privileges as the logged-in user. Your app can:
- Read/write in user's home directory
- Access files the user can access
- Be prompted for permissions on first access (some OS)

**Best Practices**:
- Only access user home directory and appdata
- Don't access system directories
- Handle permission prompts gracefully

## Encryption

Use `System::encrypt()` and `System::decrypt()` for sensitive data:

```php
if (System::canEncrypt()) {
    $encrypted = System::encrypt('sensitive_data');
    // Store encrypted value
    
    $decrypted = System::decrypt($encrypted);
}
```

**Note**: Encryption keys are stored on the device - not suitable for server-side secrets.

## TouchID / Biometric Authentication

On macOS, use TouchID for additional protection:

```php
if (System::canPromptTouchID() && System::promptTouchID('access sensitive data')) {
    // Protected operation
}
```

**Note**: TouchID confirms the person using the device matches the person who unlocked it. It does NOT identify the user.

## Database Security

SQLite databases are stored in user-accessible locations. Consider:
- Encrypting sensitive columns
- Not storing server credentials
- Validating all user input

## External URLs

**Warning**: Don't display untrusted external websites in your windows without proper security measures.

If you must, use `Window::preventLeaveDomain()` or `Window::preventLeavePage()`.

## Child Processes

Be careful with child processes:
- Don't execute untrusted commands
- Validate all command arguments
- Use full paths to executables when possible
- Handle platform differences (Windows vs Unix)

## Settings Storage

Settings in `config.json` are not encrypted. Don't store:
- API keys
- Passwords
- Sensitive tokens

Use encryption for sensitive settings values.

## Security Planning Format

For security measures:

```
Security:
  File Access: {restricted-to}
  Encryption: {what-to-encrypt}
  Authentication: {TouchID/biometric}
  External Content: {safe-domains}
  Child Processes: {validation-rules}
  Settings: {sensitive-data-handling}
```
