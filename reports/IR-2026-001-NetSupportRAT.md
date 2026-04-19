# SOC Incident Report

**Report Reference:** IR-2026-001
**Date:** 2026-02-28
**Analyst:** Qadir Bux (Noman)
**Severity:** 🔴 HIGH

---

## 1. Executive Summary

A Windows endpoint within the `easyas123.tech` domain was identified as infected with NetSupport Manager RAT. The infected host was actively communicating with a known malicious external IP address over TCP port 443. The activity was first detected via SIEM signature hits and confirmed through PCAP analysis.

---

## 2. Incident Timeline

| Time (UTC) | Event |
|---|---|
| 2026-02-28 19:55 | SIEM signature hits detected for NetSupport Manager RAT |
| 2026-02-28 19:55+ | C2 communication established to `45.131.214[.]85` over TCP/443 |
| 2026-04-20 | PCAP retrieved and analyzed |
| 2026-04-20 | Infected host identified and report generated |

---

## 3. Affected Host Details

| Field | Value |
|---|---|
| IP Address | `10.2.28.88` |
| MAC Address | `00:19:d1:b2:4d:ad` |
| Hostname | `DESKTOP-TEYQ2NR` |
| User Account | `brolf` |
| Full Name | Becka Rolf |
| Domain | `EASYAS123 / easyas123.tech` |
| LAN Segment | `10.2.28.0/24` |

---

## 4. Threat Details

| Field | Value |
|---|---|
| Malware Family | NetSupport Manager RAT |
| C2 Server | `45.131.214[.]85` |
| Protocol | TCP |
| Port | 443 (HTTPS) |
| Direction | Outbound (infected host → C2) |

---

## 5. MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Command & Control | Application Layer Protocol: Web Protocols | T1071.001 |
| Command & Control | Remote Access Software | T1219 |
| Defense Evasion | Encrypted Channel: Asymmetric Cryptography | T1573.002 |

---

## 6. Analysis Summary

PCAP analysis confirmed that internal host `10.2.28.88` (`DESKTOP-TEYQ2NR`) assigned to user Becka Rolf (`brolf`) was actively communicating with the external malicious IP `45.131.214[.]85` over TCP port 443. The traffic pattern is consistent with NetSupport Manager RAT C2 communication, which uses an HTTP-based protocol disguised over HTTPS to evade detection.

The use of port 443 suggests a deliberate attempt to blend in with legitimate HTTPS traffic and bypass perimeter firewall rules.

---

## 7. Containment Recommendations

| Priority | Action |
|---|---|
| 🔴 IMMEDIATE | Isolate `DESKTOP-TEYQ2NR` from the network |
| 🔴 IMMEDIATE | Block `45.131.214[.]85` on perimeter firewall |
| 🟡 HIGH | Reset credentials for user `brolf` |
| 🟡 HIGH | Scan all endpoints for NetSupport Manager RAT indicators |
| 🟢 MEDIUM | Review email logs for phishing attempts on brolf's account |
| 🟢 MEDIUM | Check AD logs for lateral movement from `10.2.28.88` |
| 🟢 MEDIUM | Notify Becka Rolf and conduct security awareness briefing |

---

## 8. Indicators of Compromise (IOCs)

```
IP Address:   45.131.214[.]85
Port:         443/TCP
Malware:      NetSupport Manager RAT
Hostname:     DESKTOP-TEYQ2NR
MAC:          00:19:d1:b2:4d:ad
Username:     brolf
```

---

## 9. Analyst Notes

This incident was identified through SIEM alerting and confirmed via manual PCAP analysis in Wireshark. The C2 communication over port 443 is a common evasion technique used by RAT malware to bypass network controls. Immediate isolation of the infected host is critical to prevent further damage or lateral movement within the `easyas123.tech` domain.

---

*Report completed by: Qadir Bux (Noman)*
*Date: 2026-04-20 | Reference: IR-2026-001*
