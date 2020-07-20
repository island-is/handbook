# Logging

Logging is one of the foundations pieces of telemetry we need to understand issues at runtime. It is theresfore deemed one of the core responsibilities of developers to provide meaningful logs.

## Logging infrastructure

Developers should use the `logging` library that is part of the monorepo and is configured for local as well as production environments.
Don't use other methods of logging since that could lead to log statements not getting delivered correctly to the central log store.

## Logging levels

The logging levels to be used are `error`, `warn`,`info` and `debug`.
Everything from level `info` and up (that's `info`, `error` and `warn`) are delivered to the central log store.
You can use all the levels of course, the rest simply are only local to the container/pod.

## Viewing logs

You can view the logs from all environments at [https://kibana.shared.devland.is](https://kibana.shared.devland.is). If you would like to view `debug` log statements you will need to look at the logs of the Kubernetes pod using the CLI.

## Best practices

Use `error` when you are reporting errors or exceptions.

Use `warn` when things are in 'suspicious' or potentially problematic state.

Use `info` when reaching important states - server started, user created, registration complete, etc.

Use `debug` for additional info.

Avoid logging at level `info` inside unbounded loops.

Don't log the same exception/error multiple times.
