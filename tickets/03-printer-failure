# Ticket 3 — Network Printer Failure (Multiple Users)

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

---

## Scenario

Print jobs queuing with "Error" status on 3rd floor network printer (HP LaserJet 4300 — Printer-3F-01). Issue confirmed across multiple applications and reported by multiple users.

---

## Troubleshooting

- Attempted remote print queue clear via Print Management console — queue would not clear
- Restarted Print Spooler service on print server remotely (services.msc > Print Spooler > Restart)
- Print queue cleared after spooler restart
- Sent test print from remote session — completed successfully
- Confirmed with multiple 3rd floor users that printing was restored

---

## Root Cause

Print Spooler service hang on the print server.

---

## Resolution

Restarted Print Spooler service remotely. All queued jobs processed. Flagged for monitoring — if recurring, will submit as Problem ticket for infrastructure investigation.

---

## Screenshot

![Ticket 3 - Resolved](screenshot/ticket-resolved3.png)
