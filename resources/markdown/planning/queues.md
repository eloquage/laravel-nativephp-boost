# Queues

Laravel queues work in NativePHP applications with automatic queue worker management.

## Queue Configuration

By default, NativePHP starts a single queue worker processing the `default` queue.

### Configuring Workers

Configure in `config/nativephp.php`:

```php
'queue_workers' => [
    'default' => [
        'queues' => ['default'],
        'memory_limit' => 128,
        'timeout' => 60,
        'sleep' => 3,
    ],
    'high-priority' => [
        'queues' => ['high'],
        'memory_limit' => 1024,
        'timeout' => 600,
    ],
],
```

Each worker runs as a persistent Child Process.

### Managing Workers Programmatically

```php
use Native\Desktop\Facades\QueueWorker;
use Native\DTOs\QueueConfig;

// Start worker with config
$config = new QueueConfig(
    alias: 'manual',
    queuesToConsume: ['default'],
    memoryLimit: 1024,
    timeout: 600
);
QueueWorker::up($config);

// Start worker by alias (from config)
QueueWorker::up(alias: 'default');

// Stop worker
QueueWorker::down(alias: 'manual');
```

### Queue Planning Format

For queue configuration:

```
Queues: {queue-names}
  Workers:
    - Alias: {alias}
      Queues: [{queue-list}]
      Memory Limit: {mb}
      Timeout: {seconds}
      Sleep: {seconds}
  When to Queue: {description}
```
