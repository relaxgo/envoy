# 为什么 Round Robin 负载均衡看起来不起作用？

Envoy utilizes a siloed [threading model](../intro/arch_overview/threading_model.mdrch-overview-threading). This means that worker threads and the load balancers that run on them do not coordinate with each other. When utilizing load balancing policies such as [round robin](../intro/arch_overview/load_balancing.html#arch-overview-load-balancing-types-round-robin), it may thus appear that load balancing is not working properly when using multiple workers. The [`--concurrency`](../operations/cli.md#cmdoption-concurrency) option can be used to adjust the number of workers if desired.

The siloed execution model is also the reason why multiple HTTP/2 connections may be established to each upstream; [connection pools](../intro/arch_overview/connection_pooling.md#arch-overview-conn-pool) are not shared between workers.