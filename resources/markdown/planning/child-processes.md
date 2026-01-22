# Child Processes

Long-running processes managed by NativePHP using `Native\Desktop\Facades\ChildProcess`.

## Starting Child Processes

```php
use Native\Desktop\Facades\ChildProcess;

ChildProcess::start(
    cmd: 'tail -f storage/logs/laravel.log',
    alias: 'tail'
);
```

### Process Management

- `ChildProcess::start($cmd, $alias)` - Start a process
- `ChildProcess::stop($alias)` - Stop a process
- `ChildProcess::kill($alias)` - Force kill a process
- `ChildProcess::all()` - Get all running processes

### Alternatives to Child Processes

**Queues**: For Laravel queued jobs - simpler, managed by Laravel

**Scheduler**: For periodic tasks - runs every minute

**shell_exec/proc_open**: For one-time commands (may block, can orphan)

**When to use Child Processes**: Long-running external programs you need to interact with repeatedly

### Process Planning Format

For each child process:

```
Child Process: {alias}
  Command: {full-command}
  When Started: {event/action/startup}
  When Stopped: {event/action/shutdown}
  Alternatives Considered: {queues/scheduler/etc}
  Platform Considerations: {windows/mac/linux differences}
```
