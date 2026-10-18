# Getting Started

KfVisor is a native desktop application for Apache Kafka. It runs on your machine, connects directly to your clusters over the network, and provides a visual interface for topics, messages, consumer groups, brokers, Schema Registry, and Kafka Connect — without a web server, Docker setup, or browser.

## Installation

Download the package for your platform from the [Releases page](https://github.com/tibrom/kfvisor-releases/releases/latest) or [kfvisor.com/download](https://kfvisor.com/download).

| Platform | Architecture | Package |
| --- | --- | --- |
| macOS | Apple Silicon (arm64) | DMG |
| Linux | x86\_64 | AppImage, DEB |
| Windows | x86\_64 | MSI |

Open the downloaded file and follow the standard installation steps for your OS. KfVisor stores its data in the application data directory shown in **Settings → About**.

> **macOS — Gatekeeper notice:** The current release is not notarized by Apple. After installing, macOS may block the app from opening. If KfVisor doesn't launch, run the following command in Terminal to remove the quarantine attribute:
>
> ```bash
> xattr -dr com.apple.quarantine /Applications/kfvisor.app
> ```
>
> You only need to run this once. The command does not change the application — it tells macOS that you intentionally chose to open it.

## First run

When KfVisor opens for the first time, the cluster list on the left sidebar is empty. Click **+ Add** to create your first cluster profile.

## Adding a cluster

The cluster form has three tabs: **Connection**, **Security**, and **Integrations**.

### Connection tab

| Field | Description |
| --- | --- |
| Name | Label for this profile (e.g. `prod`, `local`) |
| Bootstrap Servers | One or more `host:port` addresses, comma-separated |
| SASL Mechanism | None, PLAIN, SCRAM-SHA-256, or SCRAM-SHA-512 |

When SASL is set to anything other than None, two additional fields appear: **Username** and **Password**. A **Save password** checkbox controls whether the password is stored locally.

```
localhost:9092
broker1.internal:9092,broker2.internal:9092
```

### Security tab

| Field | Description |
| --- | --- |
| TLS/SSL | Enable to encrypt the connection |
| CA Certificate | Path to a PEM file for a self-signed or internal CA |
| Client Certificate | Path to a client certificate for mTLS |
| Client Key | Path to the matching private key for mTLS |
| Verify hostname | Toggle to disable SNI hostname verification |

CA certificate, client certificate, and client key fields are all optional. Paths reference files on your local filesystem — KfVisor reads them at connection time.

### Integrations tab

| Field | Description |
| --- | --- |
| JMX URL | Jolokia endpoint for server-side broker metrics (optional) |
| Kafka Connect URL | Base URL of the Connect REST API (optional) |
| Schema Registry URL | Base URL of the Schema Registry REST API (optional) |

Kafka Connect and Schema Registry each support independent **Basic Auth** credentials (username + password) and a custom **CA certificate** path.

Click **Add & Connect** to save the profile and connect immediately.

## Switching between clusters

All saved profiles appear in the left sidebar. Click a cluster name to connect. You can keep multiple profiles for different environments — dev, staging, production — and switch between them without restarting the application.

## Early Access

If an Early Access offer is currently active, you will find an activation button in **Settings** inside the application. Activation is handled inside the app — not through the website.

---

**Next:** [Clusters and Connection Security](clusters.md)
