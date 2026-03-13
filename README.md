# IT Support Operations Lab

**Hands-on Service Desk training: ticketing systems, Active Directory, networking diagnostics, OS troubleshooting, and ITIL workflows**

---

## Overview

This repository documents practical IT Support and Service Desk exercises completed through structured lab environments. Each section covers a core skill area required for L1/L2 Service Desk operations, with real tools, realistic scenarios, and professional documentation standards.

The goal is to demonstrate hands-on experience with enterprise IT support workflows — from ticket creation and ITIL-based incident management to Active Directory administration, network diagnostics, and OS troubleshooting.

---

## Lab 1 — ServiceNow Ticketing

Five realistic Service Desk scenarios completed in a ServiceNow Personal Developer Instance (PDI). Each ticket follows the full ITIL-based incident lifecycle: creation, triage, prioritisation (Impact × Urgency matrix), investigation, resolution documentation, and closure or escalation.

### Ticket 1 — Outlook Mobile Sync Failure

| Field | Value |
|-------|-------|
| **Incident** | INC0010007 |
| **Caller** | Beth Anglin (Sales Department) |
| **Channel** | Phone |
| **Category** | Software > Email |
| **Impact** | 3 — Low (single user) |
| **Urgency** | 2 — Medium (user cannot use mobile email) |
| **Priority** | P4 — Low |
| **State** | Resolved |

**Scenario:** User reported Outlook app on iPhone stopped syncing emails. Desktop Outlook was working normally. User needed mobile email for client communication while travelling.

**Troubleshooting:**
- Confirmed desktop Outlook syncing normally — ruled out server-side issue
- Guided user to check iPhone Settings > Passwords & Accounts
- Exchange account was present but showing error
- Removed and re-added Exchange account using company credentials
- Sync restored immediately after re-adding

**Root Cause:** Stale authentication token on mobile device.

**Resolution:** Removed and re-added Exchange account on iPhone. Full sync restored. Advised user to update saved credentials after future password changes.

<details>
<summary>📸 Screenshot — Resolved Ticket with Work Notes</summary>

![Ticket 1 - Email Sync](tickets/01-email-sync/ticket-resolved.png)

</details>

---

### Ticket 2 — Shared Drive Access Denied

| Field | Value |
|-------|-------|
| **Incident** | INC0010008 |
| **Caller** | David Loo (Finance Department) |
| **Channel** | Chat |
| **Category** | Software > Operating System |
| **Impact** | 3 — Low (single user) |
| **Urgency** | 2 — Medium (end-of-month reports due) |
| **Priority** | P4 — Low |
| **State** | Resolved |

**Scenario:** User receiving "Access Denied" error when trying to access \\fileserver\finance. Access was working last week. No role change. Team members unaffected.

**Troubleshooting:**
- Checked Active Directory group membership for the user
- User was NOT a member of SG-Finance-Drive security group
- Confirmed with Finance manager that user should have access
- Identified likely cause: accidental removal during recent group membership cleanup
- Re-added user to SG-Finance-Drive in ADUC
- Advised user to log off and log back on to refresh group membership token

**Root Cause:** User accidentally removed from security group during a recent AD cleanup.

**Resolution:** Re-added to SG-Finance-Drive in ADUC. Access restored after logoff/logon. AD admin team notified to review cleanup process.

<details>
<summary>📸 Screenshot — Resolved Ticket with Work Notes</summary>

![Ticket 2 - Shared Drive](tickets/02-shared-drive-access/ticket-resolved.png)

</details>

---

### Ticket 3 — Network Printer Failure (Multiple Users)

| Field | Value |
|-------|-------|
| **Incident** | INC0010009 |
| **Caller** | Fred Luddy (3rd Floor) |
| **Channel** | Phone |
| **Category** | Hardware |
| **Impact** | 2 — Medium (multiple users affected) |
| **Urgency** | 2 — Medium |
| **Priority** | P3 — Moderate |
| **State** | Resolved |

**Scenario:** Print jobs queuing with "Error" status on 3rd floor network printer (HP LaserJet 4300 — Printer-3F-01). Issue confirmed across multiple applications and reported by multiple users.

**Troubleshooting:**
- Attempted remote print queue clear via Print Management console — queue would not clear
- Restarted Print Spooler service on print server remotely (services.msc > Print Spooler > Restart)
- Print queue cleared after spooler restart
- Sent test print from remote session — completed successfully
- Confirmed with multiple 3rd floor users that printing was restored

**Root Cause:** Print Spooler service hang on the print server.

**Resolution:** Restarted Print Spooler service remotely. All queued jobs processed. Flagged for monitoring — if recurring, will submit as Problem ticket for infrastructure investigation.

<details>
<summary>📸 Screenshot — Resolved Ticket with Work Notes</summary>

![Ticket 3 - Printer](tickets/03-printer-failure/ticket-resolved.png)

</details>

---

### Ticket 4 — New Hire Onboarding (Service Request)

| Field | Value |
|-------|-------|
| **Incident** | INC0010010 |
| **Caller** | Alva Pennington (Marketing Manager) |
| **Channel** | Email |
| **Category** | Software |
| **Impact** | 3 — Low |
| **Urgency** | 3 — Low |
| **Priority** | P5 — Planning |
| **State** | Resolved |

**Scenario:** Manager requested full onboarding setup for new hire James Park starting Monday in Marketing. Requirements: Windows laptop (standard image), AD account, Microsoft 365 license, email, Marketing shared drive access, Teams, workstation setup at 2F-14.

**Actions Taken:**
- Created AD account (james.park) in OU=Marketing with temporary password (must change at next logon)
- Added to security groups: SG-Marketing-Drive, SG-AllStaff, SG-M365-Standard
- Assigned Microsoft 365 E3 license; email created (james.park@company.com)
- Teams account provisioned automatically via M365 license
- Requested laptop from Asset Management (ticket ASSET-4521)
- Received laptop, imaged with standard build (asset tag 2F-PC-0847)
- Delivered and configured at workstation 2F-14
- Tested login, Outlook, Teams, SharePoint, and shared drive access — all confirmed working
- Welcome packet with login instructions prepared
- Manager notified that setup is complete

**Resolution:** Full onboarding completed. All systems configured, tested, and confirmed working.

<details>
<summary>📸 Screenshot — Resolved Ticket with Work Notes</summary>

![Ticket 4 - Onboarding](tickets/04-new-hire-onboarding/ticket-resolved.png)

</details>

---

### Ticket 5 — VPN Connection Failure (Escalated to L2)

| Field | Value |
|-------|-------|
| **Incident** | INC0010011 |
| **Caller** | Benjamin Schkade (Engineering Department) |
| **Channel** | Phone |
| **Category** | Network > VPN |
| **Impact** | 3 — Low (single user) |
| **Urgency** | 1 — High (project deadline today) |
| **Priority** | P3 — Moderate |
| **State** | In Progress (Escalated to Network Team — L2) |

**Scenario:** Remote user reported VPN client returning "Connection timed out" error. Was working yesterday. Internet connectivity confirmed. User restarted PC and VPN client. Project deadline same afternoon.

**Troubleshooting (L1):**
- Confirmed internet connectivity: user can browse websites and ping 8.8.8.8 successfully
- VPN client version confirmed current (v4.2)
- Attempted alternate VPN gateway (vpn2.company.com) — same timeout error
- Cleared VPN client cache and re-attempted — same result
- Checked VPN server status dashboard — no reported outages
- Issue appears specific to this user or their ISP routing

**Escalation:** Unable to resolve at L1 after 20 minutes. All standard procedures exhausted. Escalated to Network Team with full summary of findings. Possible ISP routing issue or user-specific firewall/NAT conflict. User contact details and deadline included in handoff notes.

**Customer Communication:** User notified of escalation via customer-visible comment with ticket reference number and next steps.

<details>
<summary>📸 Screenshot — Escalated Ticket with Work Notes and Customer Comment</summary>

![Ticket 5 - VPN Escalation](tickets/05-vpn-escalation/ticket-in-progress.png)

</details>

---

## Skills Demonstrated

| Skill | Application |
|-------|-------------|
| **Ticketing System** | ServiceNow incident creation, lifecycle management, and resolution |
| **ITIL Processes** | Incident Management, Service Request Fulfilment, escalation procedures |
| **Prioritisation** | Impact × Urgency matrix applied correctly across all tickets |
| **Documentation** | Structured work notes following WHO → WHAT → WHY → HOW → RESULT format |
| **Active Directory** | Account unlock, group membership troubleshooting, onboarding account creation |
| **Troubleshooting** | Systematic diagnosis: elimination approach from simple to complex |
| **Escalation** | L1 → L2 handoff with complete documentation of steps already taken |
| **Communication** | Professional customer-visible updates separated from internal technical notes |

---

## Tools Used

`ServiceNow (PDI)` · `Jira Service Management` · `Active Directory` · `Wireshark` · `Windows CLI (ipconfig, ping, tracert, nslookup, netstat)` · `Task Manager` · `Event Viewer` · `ITIL Framework` · `Impact × Urgency Matrix`

---

## Upcoming Labs

| Lab | Topic | Status |
|-----|-------|--------|
| Lab 1 | ServiceNow Ticketing | ✅ Complete |
| Lab 2 | Active Directory & Identity Management | 🔄 In Progress |
| Lab 3 | Network Diagnostics & CLI Troubleshooting | ⬚ Planned |
| Lab 4 | Windows & macOS Troubleshooting | ⬚ Planned |
| Lab 5 | Jira Service Management | ⬚ Planned |
| Lab 6 | ITIL Classification & SLA Management | ⬚ Planned |

---

## About

This lab portfolio is part of a structured 7-day Service Desk training programme covering ticketing systems, Active Directory, networking diagnostics, OS troubleshooting, ITIL processes, and professional IT communication. Each lab is completed with real tools and documented with screenshots as evidence of hands-on practice.

**Author:** Beatriz Martins Costa
**GitHub:** [beatrizmartinsc](https://github.com/beatrizmartinsc)
