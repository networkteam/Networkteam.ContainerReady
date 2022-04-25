# Networkteam.ContainerReady

Utilities to run Flow and Neos applications in containers.

## Logging to console

Instead of using log files in containers it's a good idea to log to the console.
This package contains an extended `ConsoleBackend` that adds additional information to see the source
of log messages (by adding a configurable prefix).

Example configuration:

```yaml
Neos:
  Flow:

    # Log to STDOUT to have correct 12 factor app behavior for running in a container
    log:
      psr3:
        'Neos\Flow\Log\PsrLoggerFactory':
          systemLogger:
            default:
              class: Networkteam\ContainerReady\Log\Backend\ConsoleBackend
              options:
                prefix: '[System]  '
          securityLogger:
            default:
              class: Networkteam\ContainerReady\Log\Backend\ConsoleBackend
              options:
                prefix: '[Security]'
                # Info level has too much verbosity
                severityThreshold: '%LOG_NOTICE%'
          sqlLogger:
            default:
              class: Networkteam\ContainerReady\Log\Backend\ConsoleBackend
              options:
                prefix: '[SQL]     '
          i18nLogger:
            default:
              class: Networkteam\ContainerReady\Log\Backend\ConsoleBackend
              options:
                prefix: '[I18N]    '
```
