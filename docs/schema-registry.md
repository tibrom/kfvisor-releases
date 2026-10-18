# Schema Registry

The Schema Registry section lists all subjects in a connected Confluent-compatible Schema Registry. Select a subject to view its versions, the full schema definition, and the compatibility level. When Schema Registry is configured, KfVisor automatically enables the Avro decoder in the Messages view.

## Connecting Schema Registry

Add a Schema Registry URL in the cluster's **Integrations** tab:

```
http://schema-registry.internal:8081
```

Optional fields in the Integrations tab:

- **Username / Password** — Basic Auth for protected registries
- **CA Certificate** — path to a PEM file for a self-signed or internal CA

If Schema Registry is not configured, the section shows: *"Schema Registry not configured, add URL in cluster settings."*

## Subject list

The list shows all subjects with their latest schema version. Use the search field to filter by subject name. A warning badge appears in the toolbar if some subjects failed to load.

Click **Refresh** to reload the list from Schema Registry.

## Subject detail

Click a subject to open its detail panel with three tabs:

### Versions tab

Shows each registered version with its **Version number** and **Schema ID**.

### Definition tab

Displays the full schema definition as formatted text:

```json
{
  "type": "record",
  "name": "AppLog",
  "namespace": "com.kfvisor.demo",
  "fields": [
    { "name": "service", "type": "string" },
    { "name": "level",   "type": "string" },
    { "name": "message", "type": "string" },
    { "name": "ts",      "type": "string" }
  ]
}
```

### Compatibility tab

Shows the compatibility level configured for this subject as a badge (e.g. `BACKWARD`, `FULL`, `NONE`).

## Avro decoding in Messages

When a Schema Registry URL is configured, the **Avro (SR)** decoder becomes available in the Messages view for any topic value.

Avro decoding works with Confluent wire format: a message value that starts with a magic byte (`0x00`) followed by a 4-byte schema ID. KfVisor looks up the schema ID in Schema Registry, fetches the schema, and deserialises the value.

> **Limitations:**
> - Avro decoding applies to the message **value** only; the key decoder does not offer an Avro option.
> - Schema **references** (nested schemas) are not resolved.
> - Protobuf and JSON Schema formats are not supported.
> - The Schema Registry section is read-only — creating, updating, or deleting schemas is not available from the interface.

---

**Next:** [Kafka Connect](kafka-connect.md)
