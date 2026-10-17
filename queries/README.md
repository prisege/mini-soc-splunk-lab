# Search files

Files 01–05 transcribe the documented SPL search logic into separate files. File 06 adapts the documented inventory search by removing the original host filter and grouping by host as well as source and sourcetype.

Use the SPL search editor. These files have not been converted to SPL2. Set the time picker explicitly: last 15 minutes for alert tests, and a bounded interval containing the test events for investigation. The SPL files do not embed time boundaries or alert settings.

`main`, `linux_secure`, and the source paths are the original lab configuration. Adjust them to your own authorized lab. Files 01–04 return individual events; their alert thresholds apply to returned event counts, not aggregate rows.

The account-creation detection does not depend on the original temporary username. The administrative search matches only selected literal command paths and can miss equivalent commands under other paths. File 05 is a service-activity search, not an implemented alert in this project.
