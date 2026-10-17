# Lab setup and log collection

## Recorded environment

The project document records Windows 11 Pro, VirtualBox 7.2.4, Ubuntu Server 24.04.4 LTS, and Splunk Enterprise 10.4.2. These are the versions reported in the source, not a current compatibility recommendation or an independently rebuilt environment.

The Ubuntu VM used 4096 MB RAM, 2 virtual CPUs, and a dynamically allocated 40 GB disk. OpenSSH was installed for controlled authentication tests. Splunk Enterprise ran as the unprivileged `splunk` service account on that same VM.

## Connectivity

The VirtualBox NAT rules forwarded host `127.0.0.1:2222` to guest SSH port `22` and host `127.0.0.1:8000` to guest Splunk Web port `8000`. The loopback binding limits these forwarded host listeners to the local host. It does not replace the guest firewall or other access controls.

## Collection

The project used Files & Directories monitoring in Splunk:

| Path | Sourcetype | Index |
| --- | --- | --- |
| `/var/log/auth.log` | `linux_secure` | `main` |
| `/var/log/syslog` | `syslog` | `main` |

The `splunk` service account was added to the `adm` group, followed by a service restart, to allow it to read the selected logs. This grants access to other logs readable by that group as well; review permissions for your own environment. No credentials, Splunk binaries, VM images, or original log files are distributed here.

Before reproducing collection, verify that both files exist and receive new events. A journal-only installation needs a different collection configuration. Avoid duplicate monitors for the same file, and verify access after log rotation.

## Original troubleshooting

- A VirtualBox startup failure was resolved by reopening the application and restarting the VM.
- SSH initially appeared inactive as a service, while socket activation and a listening port confirmed availability in the documented environment.
- Splunk initially lacked log read access; updating group membership and restarting the service resolved collection.
- Splunk was stopped before configuring its systemd startup integration.

This is an account of the documented lab, not a complete unattended installation guide. Installation packages and licensing are obtained separately from their vendors.
