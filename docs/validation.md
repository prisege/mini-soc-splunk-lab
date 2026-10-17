# Validation and reproduction

## Evidence status

The original project reports that all four alerts triggered after controlled tests. The three incident reports summarize that source evidence. During portfolio preparation, the text and selected screenshots were inspected, query logic was transcribed, and public identifiers were reviewed. No Splunk instance or live VM was available for a fresh execution test.

## Checklist for a fresh lab run

1. Confirm the host and all accounts belong to an authorized isolated lab.
2. Confirm both log sources are indexed with the expected source and sourcetype values using `06-log-source-inventory.spl`.
3. Record a test start time, timezone, query, and saved alert settings. Use a bounded time range.
4. Generate a small number of incorrect SSH passwords against a dedicated test account. Stop if lockout rules would be affected. Check that more than one matching indexed event reaches the failed-login rule; compaction can affect counts.
5. Perform one successful password SSH login and verify the matching event.
6. Create a dedicated temporary local account, verify its creation event, then remove only that test account after checking its contents. Do not use an existing user's account for cleanup.
7. Run `sudo whoami` in the lab and verify the recorded initiator, target user, and command.
8. Check each rule's Triggered Alerts entry after its scheduled execution, taking suppression into account.
9. Test the failed-login threshold with zero and one matching indexed event in the selected window; it should not trigger. Record the actual results rather than assuming them.
10. Capture redacted evidence, document expected versus actual outcomes, and verify that cleanup completed.

Avoid claiming timing, detection-rate, false-positive, or production results without measurements. A clean negative test must also exclude older events still inside the search window.
