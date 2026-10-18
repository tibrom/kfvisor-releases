# Kafka Connect

The Connect section lists all connectors registered with a configured Kafka Connect cluster. You can inspect connector status, view tasks and configuration, and perform basic operational actions.

## Connecting to Kafka Connect

Add a Kafka Connect URL in the cluster's **Integrations** tab:

```
http://kafka-connect.internal:8083
```

Optional fields:

- **Username / Password** — Basic Auth
- **CA Certificate** — path to a PEM file for a custom CA

If Kafka Connect is not configured, the section shows a message prompting you to add the URL in cluster settings.

## Connector list

| Column | Description |
| --- | --- |
| Name | Connector name |
| Type | **Source** or **Sink** badge |
| Status | RUNNING (green), PAUSED (yellow), FAILED (red), UNASSIGNED (gray) |
| Tasks | Total task count; failed task count shown separately if any |

Use the search field to filter by connector name. Click **Refresh** to reload the list.

## Connector detail

Click a connector to open its detail panel with three tabs:

### Overview tab

Shows the connector type, current status, total task count, and the number of failed tasks (if any).

### Tasks tab

Lists each task with its **Task #**, **Status** badge, and **Worker ID**. A **Restart** button is shown for tasks in FAILED state.

### Configuration tab

Displays the full connector configuration as a key-value table. This is read-only.

## Actions

Action buttons appear in the connector detail header:

| Action | Effect |
| --- | --- |
| **Pause** | Suspends all tasks; the connector remains registered |
| **Resume** | Resumes a paused connector |
| **Restart** | Restarts the entire connector and all its tasks |

While an action is in progress, the button shows **"Working…"** and is disabled until the operation completes.

Use Restart on a FAILED connector after resolving the underlying cause — for example, a network issue, misconfigured credentials, or an unavailable target system.

## Limitations

The Connect view provides read access and basic operational control of existing connectors. The following are not available from the interface:

- Creating new connectors
- Deleting connectors
- Editing connector configuration
- Installing or listing connector plugins
- Viewing connector log streams

---

**Next:** [ACL](acl.md)
