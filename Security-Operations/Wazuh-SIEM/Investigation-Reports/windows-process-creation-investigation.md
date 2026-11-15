
# SOC Investigation Report: Windows Process Creation Detection Using Wazuh

## 1. Executive Summary

This project involved implementing and validating a custom detection rule in Wazuh to monitor Windows process creation activity.

The investigation focused on Windows Security Event ID 4688 and the development of a custom rule designed to identify a controlled command-line test marker.

The custom detection rule successfully identified the intended test activity during positive testing and did not trigger on a separate negative test.

All tests were conducted in a controlled lab environment. No actual malicious activity was established.

## 2. Investigation Objectives

- Configure Windows process creation auditing.
- Collect Windows Security Event ID 4688.
- Enable process command-line logging.
- Forward endpoint events to Wazuh.
- Develop a custom detection rule.
- Validate the rule using positive and negative tests.

## 3. Lab Environment

| Component | Description |
|---|---|
| SIEM | Wazuh 4.13.1 |
| Manager | Linux virtual machine |
| Endpoint | Windows |
| Agent | Wazuh Windows Agent |
| Event Source | Windows Security Log |
| Event ID | 4688 |
| Custom Rule | 100100 |

## 4. Security Telemetry Configuration

Windows process creation auditing was enabled using the Windows audit policy.

Successful process creation auditing was verified.

Command-line logging was also enabled through the Windows registry using:

ProcessCreationIncludeCmdLine_Enabled = 1

This allowed command-line information to be included in relevant process creation events.

## 5. Detection Rule Development

A custom Wazuh rule was created with the following configuration:

- Rule ID: 100100
- Parent Rule: 67027
- Event ID: 4688
- Configured Severity: Level 7
- Detection Field: win.eventdata.commandLine
- Detection Marker: SOC_LAB_TEST

The rule was designed to identify Windows process creation events whose command line contained the controlled test marker.

## 6. Detection Testing

### Positive Test

A controlled command was executed on the Windows endpoint containing the marker:

SOC_LAB_TEST

The Windows Security log recorded the process creation event.

Wazuh subsequently generated an alert matching custom rule 100100 at configured level 7.

**Result: Passed.**

### Negative Test

A separate controlled command was executed using:

NORMAL_PROCESS_TEST

The event was collected by Wazuh and matched the default process creation detection rule 67027.

It did not trigger custom rule 100100.

**Result: Passed.**

## 7. Investigation Findings

The investigation confirmed:

1. The Windows endpoint successfully communicated with Wazuh.
2. Windows process creation events were collected.
3. Process names and parent process information were available.
4. Command-line information was successfully captured.
5. The custom detection rule matched the intended positive test.
6. The separate negative test did not trigger the custom rule.

## 8. Security Assessment

The successful tests demonstrate that the custom rule can identify a specific command-line pattern within Windows process creation events.

However, a matching test marker is not evidence of malicious activity. The configured severity level is a rule setting and does not independently establish threat severity.

The rule is a basic pattern-based detection and should be expanded before being used as a production security control.

## 9. Recommendations

- Develop additional detection rules for suspicious process behaviour.
- Monitor unusual parent-child process relationships.
- Review command-line activity alongside other security telemetry.
- Correlate process creation with authentication and network events.
- Periodically test detection rules for false positives and false negatives.
- Protect command-line logs because they may contain sensitive information.

## 10. Limitations

- Testing was conducted in a controlled lab environment.
- The custom rule detects a specific test string rather than malicious behaviour generally.
- The investigation did not demonstrate a confirmed security incident.
- Additional telemetry and correlation would be required for more advanced threat detection.

## 11. Conclusion

This project provided practical experience in Windows security auditing, SIEM monitoring, custom detection engineering and detection validation using Wazuh.

It demonstrated how endpoint security events can be collected, analysed and used to develop targeted detection logic.

The project also highlighted the importance of validating detection rules through both positive and negative testing.

---

**Project:** Wazuh SIEM – Windows Endpoint Monitoring and Detection

**Investigation Type:** Controlled SOC Lab Investigation

**Platform:** Wazuh 4.13.1
