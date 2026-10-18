# Brokers and Partitions

The Brokers section lists every broker in the cluster with its status and metadata. Select a broker to view assigned partitions and traffic statistics.

## Broker list

| Column | Description |
| --- | --- |
| ID | Broker numeric ID |
| Host : Port | Advertised listener address |
| Rack | Rack label, or — if not configured |
| Status | **Online** (green) / **Offline** (red) |
| Leaders | Number of partitions for which this broker is the current leader |

The broker count at the top of the list distinguishes online vs. offline brokers. The controller broker is shown when that information is available in the cluster metadata.

## Broker detail

Click a broker to open its detail panel.

**Metadata:** ID, Host, Port, Rack, Status, Leader partitions count.

### Client-side throughput

KfVisor shows **Rx** and **Tx** byte rates with small sparkline history charts. These values come from the Kafka client library's internal statistics and represent traffic between KfVisor and this specific broker — not the total traffic across the Kafka cluster.

> Client-side statistics typically appear after approximately **10 seconds** of connection activity.

### Jolokia / JMX metrics

If a **JMX URL** (Jolokia endpoint) is configured for the cluster in the Integrations tab, KfVisor fetches server-side metrics:

- **Bytes In** — one-minute inbound byte rate from the broker's JMX MBeans
- **Bytes Out** — one-minute outbound byte rate

If the metrics data is outdated, a **stale** badge appears next to the values.

Jolokia requirements:

- A Jolokia HTTP endpoint accessible from your machine
- The current release does not support Jolokia authentication
- JMX metrics are shown in the detail panel of the selected broker

> **Multi-broker note:** In the current release, JMX metrics are fetched and stored at the cluster level, not per individual broker. The values displayed reflect the last fetched data for the cluster and are shown in whichever broker detail panel is open. Separate independent measurement for each broker in a multi-broker cluster is not confirmed in this build.

> Jolokia metrics are a supplement for quick inspection. For continuous monitoring, use a dedicated observability system.

## Partitions

Within the topic detail view (**Topics → [topic] → Partitions**), each partition shows:

- Partition ID
- Leader broker
- Replica list
- In-sync replicas (ISR) — a **!** badge and yellow row background if under-replicated
- Early offset and Late offset
- Estimated message count (Late − Early)

KfVisor does not support reassigning replicas or changing partition leadership.

---

**Next:** [Schema Registry](schema-registry.md)
