# Diagnostics and Troubleshooting

When a cluster connection fails, KfVisor shows a **Diagnose** button next to the cluster profile in the sidebar. The diagnostics panel runs a staged connectivity test and shows exactly where the failure occurred, along with a recommendation.

## Running diagnostics

Click **Diagnose** next to a failing cluster. The panel opens and runs all stages automatically.

## Diagnostic stages

The test runs five stages in sequence:

| Stage | What it checks |
| --- | --- |
| **DNS Resolve** | Resolves the bootstrap hostname to an IP address |
| **TCP Connect** | Opens a TCP connection to the broker's port |
| **TLS Handshake** | Completes the TLS handshake (skipped if TLS is not enabled) |
| **SASL Authenticate** | Authenticates with the configured credentials (skipped if SASL is None) |
| **Metadata Fetch** | Requests Kafka cluster metadata to confirm protocol compatibility |

A stage marked with **—** (skipped) means the configuration does not use that mechanism — it is not an error.

## Reading results

Each stage shows one of three indicators:

- **✓** — passed (green)
- **✗** — failed (red)
- **—** — skipped

Failed stages show a message and a **💡 recommendation**. The total elapsed time is shown in the panel header.

Common causes by stage:

| Stage | Likely cause |
| --- | --- |
| DNS Resolve | Hostname is incorrect or not resolvable from your machine |
| TCP Connect | Port is closed, blocked by a firewall, or `advertised.listeners` points to an unreachable address |
| TLS Handshake | Certificate mismatch, expired certificate, or wrong CA |
| SASL Authenticate | Incorrect credentials or unsupported mechanism |
| Metadata Fetch | Kafka version incompatibility or listener protocol mismatch |

## Support bundle

Click **Copy Support Bundle** to copy a text report to your clipboard.

> *"Contains broker info and step results. No passwords or payloads."*

The bundle includes the broker address, each stage's result, duration, and error message — but no credentials, message data, or personal information. You can share it with your team or paste it when asking for help.

---

**See also:** [Getting Started](getting-started.md) · [Clusters and Connection Security](clusters.md)
