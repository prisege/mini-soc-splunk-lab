# INC-003 — Administrative command test

## Summary

A controlled `sudo whoami` command triggered the administrative-command alert. Investigation linked it to the planned lab test; the command returned the privileged identity and did not itself change system configuration.

| Field | Public value |
| --- | --- |
| Host alias | `lab-ubuntu` |
| Initiating account alias | `lab-user` |
| Working directory alias | `/home/lab-user` |
| Target identity | `root` |
| Command | `/usr/bin/whoami` |
| Log source | `/var/log/auth.log` |
| Detection | `04-administrative-commands.spl` |
| Configured severity | Medium |
| Disposition | Authorized lab test |

## Evidence and investigation

The documented sudo event records the initiating account, working directory, target user, and command. The command was matched to the known test activity. Personal account and directory identifiers are replaced in this narrative; no raw-event screenshot is published here.

## Outcome and next steps

The event was classified as a lab test. No containment action or configuration restoration was required for the documented `whoami` command. In an unknown case, correlate the login session, authorization, and adjacent administrative commands before drawing conclusions.

## Limitations

This command is commonly legitimate. The alert is an investigation aid, and this source-based report does not demonstrate malicious privilege escalation.
