# Clusters and Connection Security

KfVisor supports multiple named cluster profiles. Each profile stores its own connection settings, security credentials, and optional integration URLs. Profiles are saved locally on your machine in the application data directory.

## Managing profiles

From the sidebar you can:

- **Add** a new profile with **+ Add**
- **Edit** an existing profile by clicking its name and selecting the edit option
- **Delete** a profile — removes only the local record, does not affect the Kafka cluster
- **Connect / disconnect** by clicking the cluster name

The sidebar shows connection state: a green dot means live, a red dot means a connection error. Once data loads, the sidebar shows the broker count and topic count below the cluster name.

## Cluster form — Connection tab

The Connection tab holds the primary connection details.

| Field | Required | Description |
| --- | --- | --- |
| Name | Yes | Display label for this profile |
| Bootstrap Servers | Yes | One or more `host:port` addresses, comma-separated |
| SASL Mechanism | — | None (default), PLAIN, SCRAM-SHA-256, SCRAM-SHA-512 |
| Username / Password | Conditional | Appear when SASL ≠ None |
| Save password | — | Store the password locally for this profile |

## Authentication

Choose the SASL mechanism that matches your cluster:

**None** — plain TCP, no credentials required.

**SASL/PLAIN** — username and password transmitted in cleartext at the protocol level. Use together with TLS if the network path is not otherwise secured.

**SASL/SCRAM-SHA-256 / SCRAM-SHA-512** — challenge-response; credentials are not transmitted in cleartext.

## Cluster form — Security tab

The Security tab controls TLS settings.

| Field | Description |
| --- | --- |
| TLS/SSL | Enable to encrypt the connection between KfVisor and the broker |
| CA Certificate | Path to a PEM file for a self-signed or internal CA |
| Client Certificate | Path to a client certificate for mutual TLS (mTLS) |
| Client Key | Path to the matching private key |
| Verify hostname | Disable SNI hostname verification (use when the broker's hostname does not match its certificate) |

All three certificate/key fields are optional. Paths reference files on your local filesystem; KfVisor reads them at connection time.

## Cluster form — Integrations tab

The Integrations tab connects optional external services to this cluster profile.

| Field | Description |
| --- | --- |
| JMX URL | Jolokia endpoint URL for server-side broker metrics |
| Kafka Connect URL | Base URL of the Kafka Connect REST API |
| Schema Registry URL | Base URL of the Schema Registry REST API |

Kafka Connect and Schema Registry each independently support:
- **Username / Password** for Basic Auth
- **CA Certificate** path for a custom CA

These are HTTP integrations. Client certificate mTLS is not supported for Kafka Connect or Schema Registry connections.

## Local storage

Profiles and settings are stored in the application data directory. The path is shown in **Settings → About**.

> **Password storage:** Passwords are never written to the local configuration file — the password fields are excluded from serialisation. All passwords are stored in the system keyring (Keychain on macOS, Secret Service on Linux, Windows Credential Manager on Windows) under the `kfvisor` service with the following keys:
>
> | Password | Keyring key |
> | --- | --- |
> | SASL (cluster) | `kfvisor / {cluster_id}` |
> | Schema Registry Basic Auth | `kfvisor / {cluster_id}:sr` |
> | Kafka Connect Basic Auth | `kfvisor / {cluster_id}:connect` |
>
> The **Save password** checkbox in the cluster form controls the SASL password only — it is stored in the keyring when the checkbox is on. Schema Registry and Kafka Connect passwords are always saved to the keyring if provided.

## Network requirements

KfVisor connects from your machine directly to the cluster. The broker addresses in Bootstrap Servers must be reachable from your computer on the advertised listener ports. If the cluster is inside a private network or VPN, that network must be accessible from your machine first.

KfVisor does not require any server-side changes to Kafka, Schema Registry, or Kafka Connect.

---

**Next:** [Topics and Configuration](topics.md)
