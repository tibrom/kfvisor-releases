# ACL

The ACLs section lets you view and manage Kafka access control lists for the connected cluster. You need the appropriate administrative rights on your connection to read and modify ACLs.

## Viewing ACLs

The ACL table shows all rules:

| Column | Description |
| --- | --- |
| Principal | The Kafka principal the rule applies to (e.g. `User:alice`) |
| Resource | Resource type and name (e.g. `Topic: orders`) — monospace |
| Operation | The Kafka operation (Read, Write, Create, Delete, Alter, Describe, …) |
| Permission | **Allow** (green badge) or **Deny** (red badge) |

Use the search field to filter by principal, resource name, or operation simultaneously.

## Creating a rule

Click **+ Add rule** to open the creation form.

Fill in:

- **Principal** — e.g. `User:service-account`
- **Permission** — Allow or Deny
- **Operation** — select from the available Kafka operations
- **Resource type** — Topic, Group, Broker, or TransactionalId
- **Resource name** — the topic name, group ID, or other resource identifier
- **Pattern type** — **Literal** (exact match) or **Prefixed** (prefix match)
- **Host** — restrict to a specific IP or use `*` for all hosts

The rule is created immediately using the rights of the current connection.

## Deleting a rule

A delete button appears when you hover over a rule row. Deletion uses a two-stage confirmation:

1. First click — the button changes to **"Sure?"** with a red background
2. Second click within **3 seconds** — the rule is deleted

If you do not click a second time within 3 seconds, the button reverts to its default state and no deletion occurs.

## Limitations

- KfVisor manages Kafka ACLs only; it does not provide KfVisor-level user roles, SSO, or account management
- "What am I allowed to do?" effective-permission analysis is not available
- Kerberos/GSSAPI and OAuthBearer are not supported as connection authentication mechanisms

---

**Next:** [Diagnostics and Troubleshooting](diagnostics.md)
