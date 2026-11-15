
# Wazuh Detection Rules

This folder contains custom detection rules developed and tested as part of my Wazuh SIEM lab.

## Custom Rule: Windows Process Creation Test

| Field | Value |
|---|---|
| Rule ID | 100100 |
| Parent Rule | 67027 |
| Event ID | 4688 |
| Configured Severity | Level 7 |
| Detection Marker | SOC_LAB_TEST |

## Detection Objective

Create a custom Wazuh rule that identifies a controlled Windows process creation event containing the marker `SOC_LAB_TEST`.

## Detection Logic

The rule uses:

- Parent rule 67027 to identify Windows process creation events.
- The `win.eventdata.commandLine` field to look for the test marker.
- Custom rule ID 100100 to generate a more specific alert.

## Validation

**Positive test:** A controlled command containing `SOC_LAB_TEST` successfully triggered rule 100100.

**Negative test:** A separate command containing `NORMAL_PROCESS_TEST` did not trigger rule 100100. It remained visible under the default Windows process creation detection.

## Important Note

The tests were performed in a controlled lab environment. The custom rule demonstrates pattern-based detection validation; it does not establish that malicious activity occurred.
