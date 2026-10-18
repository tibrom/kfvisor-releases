# KfVisor

A desktop client for Apache Kafka. Browse topics and messages, inspect consumer groups and their lag, manage topic configuration, and work with Schema Registry and Kafka Connect — all from a native desktop interface that connects directly to your clusters.

**[kfvisor.com](https://kfvisor.com)** · **[Documentation](https://kfvisor.com/docs)** · **[Download](https://kfvisor.com/download)**

---

## Download

The latest release is available on the [Releases page](https://github.com/tibrom/kfvisor-releases/releases/latest).

| Platform | Architecture | Package |
| --- | --- | --- |
| macOS | Apple Silicon (arm64) | `.dmg` |
| macOS | Intel (x86\_64) | `.dmg` |
| Linux | x86\_64 | `.AppImage`, `.deb` |
| Windows | x86\_64 | `.msi` |

> **macOS — Gatekeeper notice:** The current release is not notarized by Apple. After installing, macOS may block the app from opening. If KfVisor doesn't launch, run the following command in Terminal to remove the quarantine attribute:
>
> ```bash
> xattr -dr com.apple.quarantine /Applications/kfvisor.app
> ```
>
> You only need to run this once. The command does not change the application — it tells macOS that you intentionally chose to open it.

---

## Quick start

1. Launch KfVisor — the sidebar shows **No clusters yet**.
2. Click **+ Add** and fill in:
   - **Name** — a label for this cluster (e.g. `prod`, `local`)
   - **Bootstrap Servers** — e.g. `kafka:9092`
   - **SASL Mechanism** — PLAIN, SCRAM-SHA-256, SCRAM-SHA-512, or None
   - **TLS/SSL** — enable if your cluster requires it
3. Click **Add & Connect**. The status dot turns green when connected.

---

## What's included

| Feature | Status |
| --- | --- |
| Topics — list, partitions, config, create, compare | ✓ |
| Messages — live streaming and historical fetch | ✓ |
| Produce (single message) | ✓ |
| Consumer Groups — state, lag, per-partition offsets | ✓ |
| Consumer Group Offset Reset | ✓ |
| Brokers — metadata, client-side throughput, Jolokia metrics | ✓ |
| Schema Registry — subjects, versions, Avro decoding | ✓ |
| Kafka Connect — connectors, tasks, pause/resume/restart | ✓ |
| ACLs — view, create, delete | ✓ |
| Connection diagnostics | ✓ |
| SASL/PLAIN, SCRAM-SHA-256, SCRAM-SHA-512, mTLS | ✓ |
| Protobuf | Not in this release |
| Kerberos / OAuthBearer | Not in this release |
| Auto-update | Not in this release |

---

## Supported Kafka

KfVisor targets Kafka APIs available in Kafka 2.4 and later. The full compatibility matrix has not been formally tested against all versions; standard setups on 2.4+ are the expected range.

---

## Documentation

Full documentation is available at **[kfvisor.com/docs](https://kfvisor.com/docs)** and mirrored in the [`docs/`](docs/) folder of this repository:

| Topic | File |
| --- | --- |
| Getting Started | [docs/getting-started.md](docs/getting-started.md) |
| Clusters and Connection Security | [docs/clusters.md](docs/clusters.md) |
| Topics and Configuration | [docs/topics.md](docs/topics.md) |
| Messages | [docs/messages.md](docs/messages.md) |
| Consumer Groups | [docs/consumer-groups.md](docs/consumer-groups.md) |
| Brokers and Partitions | [docs/brokers.md](docs/brokers.md) |
| Schema Registry | [docs/schema-registry.md](docs/schema-registry.md) |
| Kafka Connect | [docs/kafka-connect.md](docs/kafka-connect.md) |
| ACL | [docs/acl.md](docs/acl.md) |
| Diagnostics and Troubleshooting | [docs/diagnostics.md](docs/diagnostics.md) |

---

## Data storage

| Data | Location |
| --- | --- |
| Cluster profiles | `{app_data_dir}/state.json` |
| Passwords | System keyring (macOS Keychain / Linux Secret Service / Windows Credential Manager) |
| TLS certificates | Paths you provide — files are read at connect time, not copied |

`{app_data_dir}` is shown in **Settings → About**.

---

## Early Access

KfVisor is currently in Early Access. The Early Access version is free. No license key is required to download or use it.

If an Early Access offer is active, you will find an activation button in **Settings** inside the application.

---

## Feedback and bugs

Open an issue in this repository or email [tibromcrm@gmail.com](mailto:tibromcrm@gmail.com).

When reporting a connection issue, include the diagnostic bundle from the connection error screen: click **Diagnose** on the failing cluster, then **Copy Support Bundle**.
