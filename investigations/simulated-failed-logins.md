# Case Study: Simulated Multiple Failed Logins

**Environment:** Windows Server 2022 → Azure Arc / AMA → Log Analytics → Microsoft Sentinel  
**Status:** Closed — Benign Positive (Suspicious but Expected)  
**Scenario:** Authorized failed-password simulation, not a genuine attack

## Objective

Validate that repeated failed sign-in attempts generated useful Windows authentication logs and triggered a scheduled Microsoft Sentinel detection.

## Detection

- Analytics rule: **SOC Lab - Multiple Failed Logins**
- Windows Event ID: **4625**
- Query window: **15 minutes**
- Threshold: **5 or more failures for one account**
- Evaluation frequency during testing: **5 minutes**
- Severity: **Medium**
- MITRE technique context: **T1110 — Brute Force**

See [the rule query](../kql/multiple-failed-logins-detection.kql).

## Activity and evidence

I generated controlled incorrect-password attempts against a disposable local account, `SOC-SERVER2022\\soc-test`. Windows recorded failed sign-ins with Event 4625. Investigation of the lab events showed interactive logon type **2**, the loopback address **`::1`**, and related authentication status information consistent with an incorrect password; event 4776 included **`0xC000006A`**.

The 15-minute threshold was reached during testing, and Sentinel created incidents. Some repeated test executions produced multiple incidents because the rule was scheduled to run repeatedly against overlapping time windows.

## Analyst triage

1. Reviewed the incident and its analytics rule.
2. Confirmed the Windows event ID, timestamp, affected test account, and repeated failed logons in Log Analytics.
3. Matched the incident timing and account to the authorized lab simulation.
4. Closed the simulated incident as **Benign Positive — Suspicious but Expected**.

## Outcome

**Detection test successful:** repeated authentication failures resulted in Sentinel incidents. **No compromise was claimed or established.** The investigation was a deliberately simulated test rather than evidence of an external malicious actor.

## Improvements for the next iteration

- Tune thresholds and suppression/grouping to reduce duplicate alerts.
- Validate entity mapping for account and host fields in incident details.
- Record response actions, timestamps, and detection coverage in a repeatable test checklist.
- Extend to separate controlled Kali-based network tests only after their telemetry is actually ingested and validated.

## Evidence

See the [screenshots guide](../screenshots/README.md). Screenshots will be added only after identifiers are checked and redacted.
