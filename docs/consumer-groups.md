# Consumer Groups

The Consumers section shows every consumer group in the connected cluster with its current state, total lag, member count, and coordinator broker. Drill into any group for per-partition offset detail and a lag history chart.

## Group list

The list refreshes automatically. Use the search field to filter by group ID.

Filter by state using the buttons above the list:

| State | Badge color | Meaning |
| --- | --- | --- |
| **Stable** | Green | All members are assigned and consuming |
| **Rebalancing** | Yellow | The group is mid-rebalance; assignments are changing |
| **Empty** | Gray | No active members; offsets may still be committed |
| **Dead** | Red | The group has been cleaned up or never fully initialised |

The **Lag** column shows the total lag. Lag is color-coded:

- **Green** — zero lag
- **Normal text** — under 1 000
- **Yellow** — 1 000 to 99 999
- **Red** — 100 000 or more

If data is unavailable for a partition, the cell shows a dash.

## Group detail

Click a group to open its detail panel on the right side. Three tabs are available.

### Overview tab

Shows the group state with a plain-language description. A **hints box** (yellow background) appears when KfVisor detects a notable condition:

- No active members are assigned
- More members than assigned partitions
- A single partition holds more than 90% of the total lag
- The group is currently rebalancing

These hints are based on the available metadata, not an automated root-cause analysis.

A **lag history sparkline** shows total lag over the current session. This chart is in-memory and resets when the application is closed.

### Members tab

Lists each member with Member ID, Client ID, Host, and partition assignments. Long IDs are truncated with an ellipsis.

### Offsets tab

Shows every topic/partition pair the group has committed offsets for:

| Column | Description |
| --- | --- |
| Topic | Topic name |
| Part. | Partition ID |
| Committed | Last committed offset |
| Earliest | Earliest available offset in the partition |
| Log End | Latest available offset in the partition |
| Lag | Log End − Committed |

Lag is color-coded using the same thresholds as the group list. If a partition has no committed offset, the lag cell may be empty.

## Reset Offsets

For **Empty** or **Dead** consumer groups, you can reset partition offsets to a new position using the Reset Offsets drawer.

### Strategies

| Strategy | Result |
| --- | --- |
| Earliest | Move to the start of available data in each partition |
| Latest | Move to the end of the log in each partition |
| Specific Offset | Set an explicit numeric offset |
| Timestamp | Find the nearest offset for a given date and time |

### Workflow

1. Select a strategy (and enter an offset or timestamp if required)
2. Click **Preview changes (dry-run)**
3. Review the preview table:

| Column | Description |
| --- | --- |
| Topic | Topic name |
| Part. | Partition ID |
| Current | Current committed offset |
| New | New offset after reset |
| Delta | New − Current (negative = reprocess messages, positive = skip messages) |
| ~Messages | Approximate number of messages affected |

Delta is color-coded: negative values are red (reprocessing), positive and zero are muted.

4. Once the preview looks correct, enter the **group name** to confirm and provide a **reason** (recorded in the audit log)
5. Click **Execute**

> **Important:** If you change the strategy after generating a preview, a warning appears and you must run a new dry-run before executing. The Execute button is disabled until the dry-run, group name, reason, and strategy are all consistent.

KfVisor resets the offsets; your application is responsible for any reprocessing that follows. Reset Offsets only works on groups that are not actively consuming.

> **Known issue in this release:** There is a confirmed bug where the dry-run preview may not correctly bind to the target group in some scenarios. Before clicking Execute, verify that the preview table shows the expected partitions and offsets for the correct group. If the preview looks inconsistent, close the drawer, reopen it, and run a fresh dry-run.

---

**Next:** [Brokers and Partitions](brokers.md)
