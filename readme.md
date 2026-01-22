# NativePHP Boost

**A Laravel Boost extension that helps AI agents produce accurate, detailed
implementation plans for NativePHP desktop applications.**

## Setup

Install NativePHP Boost using Composer:

```bash
composer require eloquage/laravel-nativephp-boost --dev
```

Then run the Boost installer and select **NativePHP Boost** when prompted:

```bash
php artisan boost:install
```

To verify installation, check your `AGENTS.md`, `CLAUDE.md`, or similar file for
a new **NativePHP Boost** section.

## Usage

1. Enable **planning mode** in your AI agent (Claude Code, Cursor, etc.)
2. Ask the agent to create a **NativePHP Boost plan** for your feature

Example prompt:

```
Create a NativePHP Boost plan for a desktop task management app.

The app should have a main window with a task list, a system tray icon,
and global shortcuts for quick task creation. Users can create, edit, and
delete tasks. Each task has a title, description, due date, priority, and
status. The app should use native notifications for reminders and save
tasks to a local SQLite database. Include a settings window for user
preferences and enable auto-start on login.

The main menu should have File, Edit, and View options. The system tray
icon should show a context menu with quick actions.
```

The agent will produce a detailed specification document ready for direct
implementation, no guessing required.

## What's Included

NativePHP Boost provides comprehensive planning guides covering:

- Windows, menus, and system integration
- Dialogs, notifications, and clipboard operations
- Child processes, queues, and database management
- File system operations and settings persistence
- Broadcasting, security, and testing
- Application lifecycle and publishing

## License

MIT. Please see the [license file](license.md) for more information.
