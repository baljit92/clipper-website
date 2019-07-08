+++
title= "Monitoring Clipper Metrics"
date= 2018-03-13T10:23:10-07:00
description = ""
draft= false
weight = 10
+++

Starting in Clipper v0.3.x, Clipper reports metrics to a [Prometheus](https://prometheus.io/) server.

## Prometheus Server
We use Prometheus as the metric tracking system. When you start a Clipper cluster, a Prometheus instance is automatically started for you.
If you are using `DockerContainerManager`, you can view Prometheus UI at: [`http://localhost:9090`](http://localhost:9090).
If you are using `KubernetesContainerManager`, the Prometheus address is dynamically generated by Kubernetes. You can fetch the address for your cluster by calling `clipper_conn.get_metric_addr()`.

Please note that the Prometheus UI is intended for debug purpose only. You can view certain metrics and plot the timeseries, but for better visualization we recommend [Grafana](https://grafana.com/).
Grafana has default support for Prometheus Client. Check out the [example](https://github.com/ucbrise/clipper/tree/develop/examples/monitoring) on GitHub to see how to use Grafana to display Clipper metrics.

## Available Metrics
Clipper provides latency and throughput metrics by default. In particular, we provide latency and throughput metrics across several processing stages. 

Check out the example for more details.

## User Defined Metrics
You can also add user defined metrics in your application. The API is simple. When you write your predict function, just add the following:

- `import clipper_admin.metric as metric` to import the Metrics module
- `metric.add(metric_name, metric_type, metric_description, optional_histogram_bucket)` to add a metric.  The metric type is defined in [Prometheus Data Types](https://prometheus.io/docs/concepts/metric_types/)
- `metric.report(metric_name, metric_data)` to report a metric. 

Please checkout a detailed [example/user_defined_metric](https://github.com/ucbrise/clipper/tree/develop/examples/user_defined_metric) with user defined metric. In the example, we will add metrics for a sklearn spam prediction model. 


## [WIP] System Metrics
Clipper does not collect physical system metrics like the CPU or memory usage yet. Please follow the progress [on GitHub](https://github.com/ucbrise/clipper/issues/421) and feel free to [contribute](/contributing)!