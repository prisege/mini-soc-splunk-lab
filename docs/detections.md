# Alert configuration and limitations

The documented alerts run every minute using `*/1 * * * *` and search the last 15 minutes. The trigger action is Add to Triggered Alerts. This is a list of triggered alerts, not a dedicated incident case-management system.

| Search | Number of results | Severity | Suppression evidence |
| --- | --- | --- | --- |
| Failed password SSH | Greater than 1 | High | 15 minutes shown in source screenshot |
| Accepted password SSH | Greater than 0 | Low | Narrative says 15 minutes; source screenshot shows 15 seconds |
| New local user | Greater than 0 | High | 15 minutes shown in source screenshot |
| Selected sudo commands | Greater than 0 | Medium | 15 minutes shown in source screenshot |

The source narrative describes Trigger Once. Check the saved alert itself before relying on the final persisted settings. Configuration screenshots show the save dialog and do not independently establish the saved state. For a fresh reproduction, use Trigger Once and explicitly verify the suppression unit; a 15-minute suppression is a documented design intention, not a verified setting for every original alert.

## Interpretation

The failed-login threshold counts matching indexed events across the search. Two unrelated users can satisfy it. Repeated-message compaction can also make the event count differ from the number of incorrect passwords. This simple rule is a learning exercise rather than a validated brute-force detector.

Successful password authentication is monitored for visibility. It does not establish compromise and does not cover successful public-key authentication. New account creation and administrative commands can be legitimate; check authorization and surrounding activity.

The sudo rule matches a short list of command strings. Its original name, Suspicious Administrative Commands, describes an investigation prompt; the command alone does not prove malicious intent. A basic `whoami` test reads identity information and does not modify accounts.

## Operational limits

Overlapping 15-minute windows can return the same events repeatedly. Suppression can reduce repeats but can also hide unrelated activity if it applies to the whole alert. This project does not establish per-entity suppression, ingestion-delay coverage, an acceptable false-positive rate, or production detection effectiveness.

An improvement would group events by extracted source IP, account, and destination, tune thresholds using a baseline, and validate late-arriving events. These improvements are proposed work, not implemented achievements in this repository.
