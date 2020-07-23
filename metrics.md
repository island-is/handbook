# Metrics

Metric is one of the foundations pieces of telemetry we need to understand issues at runtime. It is theresfore deemed one of the core responsibilities of developers to provide metrics in their services.

## Metrics infrastructure

We are using [Prometheus](https://prometheus.io) for collecting, storing and querying metrics. To see the different metric types available please see [here](https://prometheus.io/docs/concepts/metric_types/). For more information on naming of metrics, please see [here](https://prometheus.io/docs/practices/naming/).

If you are using the `infra-express-server` library you already have the metrics infrastructure setup for you. Additionally we already provide metrics for the routes you are providing.
You need to add the metrics that represent your domain entities and the actions performed on these. For an example please take a look at this [file](https://github.com/island-is/island.is/blob/master/libs/infra-express-server/src/lib/infra-express-server.ts).

## Tracing

If you use the reference `infra-express-server` library you are already setup for producing tracing info when performing HTTP/HTTPS calls. We will be adding soon adding tracing for
