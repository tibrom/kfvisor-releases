# Topics and Configuration

The Topics section gives you a complete view of every topic in the connected cluster — partition count, replication factor, estimated message count, size, and retention — and lets you view and edit individual topic configuration.

## Topic list

The topic list shows all topics in the cluster. Use the search field to filter by name. Internal topics (names starting with `_`) are hidden by default; toggle **Show internal** to include them. Internal topics appear at reduced opacity in the list.

You can sort the list by clicking column headers:

- Name
- Partitions / RF (replication factor)
- Messages (estimated)
- Retention

> **Note:** The message count is an estimate based on partition offsets. It may differ from the actual number of records after log compaction.

## Topic detail

Click a topic name to open its detail view. The header shows the topic name and a **Produce** button. Four tabs are available: **Partitions**, **Messages**, **Topic Consumers**, and **Config**.

### Partitions tab

| Column | Description |
| --- | --- |
| Partition | Partition ID |
| Leader | The broker currently leading this partition |
| Replicas | All broker IDs holding a replica |
| ISR | In-sync replicas — shows a **!** badge if under-replicated |
| Early offset | Earliest available offset |
| Late offset | Latest available offset |
| Messages | Estimated record count (Late − Early) |

Under-replicated partitions are highlighted with a yellow background and an **!** badge on the ISR cell. A warning is shown in the tab footer when any partition is under-replicated.

### Topic Consumers tab

Lists consumer groups that have committed offsets for this topic, with their state, member count, and current lag.

## Configuration

The **Config** tab shows every configuration key for the topic.

| Column | Description |
| --- | --- |
| Key | Configuration parameter name |
| Value | Current effective value (sensitive values masked as ••••••) |
| Source | Where the value comes from |

**Source** values:

| Source | Meaning |
| --- | --- |
| Topic | An explicit override set on this topic |
| Broker | Inherited from the broker configuration |
| Broker default | The broker's built-in default |
| Static | A static default defined at the Kafka level |
| Default | System default |

Use the search field to filter keys by name. The toolbar shows a count of visible vs. total entries.

### Editing a value

Click the edit icon on a row to open an inline editor. Input type matches the parameter — text, number, boolean toggle, or a dropdown for enumerated values.

Parameters with **Source: Topic** have an explicit override and can be reset to the inherited value. Click the reset icon to remove the override.

> **Caution:** Saving `retention.ms`, `cleanup.policy`, or `retention.bytes` requires an additional "This may affect your data" confirmation step.

Read-only parameters cannot be edited. Sensitive parameter values are masked.

## Comparing two topics

Click **Compare** in the topic list toolbar to enter compare mode. Two dropdowns appear — select the topics to compare, then click **Compare configs**.

The diff view shows both configurations side by side:

- Rows with differences are highlighted
- Use **Differences only** to hide matching rows
- A count of differences is shown in the header

> **Note:** The comparison uses the already-loaded configurations. Open Config for both topics before using Compare to ensure both are available.

## Creating a topic

Click **+ New Topic** in the topic list. Fill in:

- **Name** — topic name
- **Partitions** — partition count
- **Replication factor** — number of replicas

The topic is created in the current cluster using the rights of the configured connection.

---

**Next:** [Messages](messages.md)
