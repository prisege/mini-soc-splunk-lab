# INC-002 — Local user creation test

## Summary

A temporary local account was created to validate account-creation monitoring. The new-user alert matched the generated event. The source project classifies this as an authorized test and reports removal of the account after testing.

| Field | Public value |
| --- | --- |
| Host alias | `lab-ubuntu` |
| Created account alias | `lab-test-user` |
| Home directory alias | `/home/lab-test-user` |
| Log source | `/var/log/auth.log` |
| Detection | `03-new-local-user.spl`, more than 0 matching events |
| Configured severity | High |
| Disposition | Authorized lab test |

## Evidence and investigation

The documented `useradd` event includes a new account name, UID/GID, and a home directory. The original values are not reproduced here. The known test action and account details were checked against the alert to establish why it fired.

## Outcome and next steps

The source report states that the temporary account was removed after testing. This portfolio does not include an independent cleanup log or a fresh verification of deletion. In an unknown case, verify the creator's authorization, group membership, login history, and credentials before deciding whether account containment is appropriate.

## Limitations

New account creation alone does not prove persistence or compromise. This is a source-based, anonymized lab report, not a production incident record.
