# INC-001 — Failed SSH login test

## Summary

Repeated incorrect SSH passwords generated a lab alert. Investigation attributed the activity to a controlled test from the host machine. The source report did not identify an external attack.

| Field | Public value |
| --- | --- |
| Environment | Controlled Ubuntu lab |
| Host alias | `lab-ubuntu` |
| Target account alias | `lab-user` |
| Source address example | `192.0.2.10` — substituted documentation address |
| Log source | `/var/log/auth.log` |
| Detection | `01-failed-ssh.spl`, more than 1 matching event in 15 minutes |
| Configured severity | High |
| Disposition | Authorized lab test |

## Evidence and investigation

The project records SSH `Failed password` events after deliberate incorrect-password attempts. The original observed source was the VirtualBox NAT gateway, representing the host-side connection in this lab. The substituted address above must not be interpreted as an external indicator of compromise.

The investigator checked the account, source context, and known test activity. Some identical log messages were compacted into repeated-message entries, so a one-to-one mapping between indexed events and password attempts was not established.

## Outcome and next steps

The activity was classified as a controlled test. No external compromise was established in the documented investigation. No containment action is claimed. For an unknown source, review surrounding successful logins, account ownership, and host activity before selecting a response.

## Limitations

This report summarizes the source project and uses replacement identifiers. No fresh investigation, complete forensic timeline, or raw log export accompanies it. The global threshold is not sufficient to establish a brute-force attack.
