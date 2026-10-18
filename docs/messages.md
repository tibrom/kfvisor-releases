# Messages

The Messages tab inside any topic lets you read new messages as they arrive or query a specific range from the past. Select a message to inspect its key, value, headers, and metadata.

## Live mode

In **Live** mode, KfVisor subscribes to all partitions and streams incoming messages in real time.

Controls:

- **Pause / Resume** — stop accumulating new messages without disconnecting
- **Clear** — remove all locally displayed messages (does not affect the Kafka topic)
- **Auto-scroll** — keep the view scrolled to the latest message; uncheck to scroll freely
- **Message counter** — shows current count vs. the selected limit

## Historical mode

In **Historical** mode, KfVisor reads already-written messages from the topic.

Controls:

- **Partition** dropdown — read from all partitions or a specific one
- **From offset** — start at a specific offset in the selected partition
- **From time** — find the first offset at or after a given timestamp (mutually exclusive with From offset)
- **Limit** — maximum number of messages to load
- **Load** / **Stop** buttons

When a specific offset is set, the time field is not used. An offset is per-partition; offset 100 in partition 2 is unrelated to offset 100 in partition 0.

## Message limit

Both modes share a limit dropdown:

**50 · 100 · 200 · 500 · 1 000 · 5 000 · 10 000**

## Message table

Each row shows:

| Column | Description |
| --- | --- |
| Part. | Partition number |
| Offset | Message offset within the partition |
| Timestamp | Message timestamp |
| Key | Key preview (truncated) |
| Value | Value preview (truncated) |
| Size | Combined byte size of key + value |

Click a row to expand the message detail panel below the table.

## Message detail panel

The detail panel shows the full key and value with a decoder selector for each, plus headers and size metadata.

### Key decoders

| Decoder | Use |
| --- | --- |
| Auto | Attempts JSON first; falls back to String |
| String | Plain UTF-8 text |
| JSON | Parsed tree with collapsible nested objects |
| Hex | Raw bytes as hexadecimal pairs |
| Base64 | Decode a Base64-encoded text value |

### Value decoders

The value decoder has one additional option beyond the key decoders:

| Decoder | Use |
| --- | --- |
| Auto | Attempts JSON first; falls back to String |
| String | Plain UTF-8 text |
| JSON | Parsed tree with collapsible nested objects |
| Hex | Raw bytes as hexadecimal pairs |
| Base64 | Decode a Base64-encoded text value |
| **Avro (SR)** | Confluent wire-format Avro, decoded using Schema Registry |

> **Avro decoding** requires a Schema Registry URL in the cluster's Integrations settings. Only values in Confluent Avro wire format (magic byte `0x00` + 4-byte schema ID) are decoded. Avro decoding is available for the **value only** — the key decoder does not include an Avro option.

The decoder selection is remembered per topic and cluster for the current session.

> **64 KiB limit:** Key and value fields are truncated at 64 KiB. When truncation occurs, the original byte size is shown alongside a truncation badge. Full JSON or Avro decoding is not guaranteed for truncated data.

### Headers

All message headers are shown as key-value pairs. Binary header values are displayed as `(binary)`.

## Sending a message

Click **Produce** (top-right of the topic view) to open the send panel.

> **Warning:** The panel requires you to check **"I understand, allow sending"** before the Send button becomes active. Messages written to Kafka cannot be deleted.

Fields:

| Field | Description |
| --- | --- |
| Partition | **Auto** (let Kafka choose) or a specific partition number |
| Key | Text key; check **null** to send a null key |
| Value | Message value with format selector |
| Headers | Optional key-value pairs; add/remove freely |

**Value format** dropdown: String, JSON, Base64, Hex. Each format has live validation — a badge shows whether the current input is valid for the selected format. JSON also has a **pretty-print** button. The **null** toggle for value is labeled *null (tombstone)*.

An estimated byte size is shown above the Send button.

### Recent sends

The panel keeps a history of the last 20 send attempts for the current session. Each entry shows the time and result — partition + offset on success, an error message on failure. Pending sends that receive no result within 30 seconds are marked as **unknown**.

> **Known issue in this release:** The request tracking between UI and backend is not fully synchronised. Delivery confirmations (partition + offset) may not always appear in the history even when the message was successfully written. Treat the history as a best-effort log — confirm actual delivery by reading back from the topic if it matters.

## Limitations

- No full-text search across the topic
- No filter by JSONPath, key, or header value
- No export or backup of messages
- Historical read uses a dedicated consumer with auto-commit disabled; it does not affect offset positions of your application's consumer groups

---

**Next:** [Consumer Groups](consumer-groups.md)
