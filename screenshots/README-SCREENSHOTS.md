# Microsoft Sentinel SOC Lab — screenshots

GitHub-ready selected evidence from an authorized Windows Server 2022 / Azure Arc / Microsoft Sentinel lab, October 17, 2026.

1. `01-Azure-Arc-Connected.png` — Arc machine connected and monitoring extension installed.
2. `02-Windows-Security-Events.png` — KQL results verifying Windows SecurityEvent ingestion.
3. `03-Failed-Login-Investigation.png` — Eight observed 4625 failed login events for `soc-test` in the query window.
4. `04-Analytics-Detection-Rule.png` — Scheduled rule configuration and account/host entity mapping.
5. `05-SOC-Incident-Closed.png` — Incident #3 closed as benign positive; owner name and deep link redacted.
6. `06-Entity-Mapping.png` — Close-up of Account and Host mappings (same settings as #4).

Note: Incident screenshot is #3, not #1. Different recorded query time windows produced different counts.
Before publishing, review images for any additional details you prefer not to share.
