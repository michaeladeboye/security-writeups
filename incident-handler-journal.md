# Incident Handler's Journal

A working log of security incident investigations and detection work, started as the Course 6 portfolio activity for the Google Cybersecurity Professional Certificate (*Sound the Alarm: Detection and Response*). Being extended with detection work from my own home lab.

---

## Entry #1 — 9/9/26

**Description:** Documenting a cybersecurity incident at a small healthcare company. The incident occurred across two phases:
1. **Detection and Analysis:** The organization first detected the ransomware incident and contacted several other organizations for technical assistance.
2. **Containment, Eradication, and Recovery:** The company shut down its computer systems, and since it could not fully eradicate and recover from the incident alone, it contacted outside organizations for assistance.

**Tools used:** None

**The 5 W's**
- **Who:** An unknown, organized group of threat actors known to target organizations in the healthcare and transport industries.
- **What:** The attackers gained access to the company's network using phishing emails containing a malicious attachment that installed ransomware once downloaded.
- **When:** Tuesday morning, 9:00 AM.
- **Where:** On employees' computers.
- **Why:** Employees were not made aware of the possibility of phishing emails being used to deliver malware.

**MITRE ATT&CK:** T1566 (Phishing)

**Additional notes:** Employees should be made aware of this and similar attack patterns going forward, and trained on how to respond.

---

## Entry #2 — 9/10/26

**Description:** Analyzing network traffic data using Wireshark. Part of the Detection and Analysis phase of the NIST Incident Response Lifecycle.

**Tools used:** Wireshark — a network protocol analyzer with a GUI. Its value in cybersecurity is letting analysts capture and inspect network traffic to detect and investigate malicious activity.

**Notes:**
- Used Wireshark to explore the protocol and data layers inside a network packet.
- Applied filters to select and inspect packets based on specific criteria, e.g. `ip.addr == 142.250.1.139`
- Filtered and inspected UDP DNS traffic to examine protocol data, e.g. `udp.port == 53`
- Applied filters to TCP packet data to search for specific payload text, e.g. `tcp.port == 80`

**MITRE ATT&CK:** None

---

## Entry #3 — 9/10/26

**Description:** Capturing network traffic data using tcpdump. Part of the Detection and Analysis phase of the NIST Incident Response Lifecycle.

**Tools used:** tcpdump — a network protocol analyzer accessed via the command line. Like Wireshark, it lets analysts capture, filter, and analyze network traffic.

**Notes:**
- Identified network interfaces to capture packet data, e.g. `sudo ifconfig`
- Used tcpdump to filter live network traffic, e.g. `sudo tcpdump -i eth0 -v -c5`
- Captured network traffic to a file, e.g. `sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &`
- Filtered the captured packet data, e.g. `sudo tcpdump -nn -r capture.pcap -v`

**MITRE ATT&CK:** None

---

## Entry #4 — 9/10/26

**Description:** Investigating a cybersecurity incident at a financial services company. Part of the Detection and Analysis phase of the NIST Incident Response Lifecycle.

**Tools used:** VirusTotal — an investigative tool that analyzes files and URLs for malicious content (viruses, worms, trojans, and more). Useful for quickly checking whether an indicator of compromise has already been reported as malicious by the cybersecurity community. Used here to analyze a file hash that was reported as malicious.

This scenario placed me as a SOC analyst investigating a suspicious file hash after it was flagged by security systems, and determining whether the alert signified a real threat.

**The 5 W's**
- **Who:** The advanced threat actor BlackTech.
- **What:** An employee downloaded a file from a phishing email; opening it executed a malicious payload.
- **When:** 1:00 PM.
- **Where:** The computer of an employee at a financial services company.
- **Why:** The employee downloaded a malicious file.

**MITRE ATT&CK:** T1566 (Phishing)

**Additional notes:**
- Per the VirusTotal report, the file hash was flagged as malicious by over 50 vendors.
- Identified as Flagpro, malware commonly used by BlackTech.

---

## Entry #5 — 9/10/26

**Description:** Determining the validity of a phishing alert at a financial services company. Part of the Detection and Analysis phase of the NIST Incident Response Lifecycle.

**Tools used:** None

**The 5 W's**
- **Who:** A malicious actor.
- **What:** A phishing alert was triggered after an employee downloaded a suspicious file.
- **When:** Wednesday, July 20th, 9:30 AM.
- **Where:** The computer of an employee at a financial services company.
- **Why:** A malicious actor sent a phishing email with a malicious file disguised as a resume; the employee downloaded it, triggering the alert.

**Additional notes:** To prevent a repeat, the company should train employees to spot phishing emails — for example, grammatical errors and inconsistencies in the message.

**MITRE ATT&CK:** T1566.001 (Spearphishing Attachment)

---

## Entry #6 — 9/10/26

**Description:** Reviewing a major security incident at a retail company. Part of the Post-Incident Activity phase of the NIST Incident Response Lifecycle.

**Tools used:** None

**The 5 W's**
- **Who:** A malicious actor.
- **What:** Stole customer data and demanded a ransom in exchange for not releasing it publicly.
- **When:** December 22, 2022, 3:13 PM PT.
- **Where:** At a retail company.
- **Why:** A vulnerability in the company's e-commerce web application allowed a forced-browsing attack — the attacker modified the order number in a purchase confirmation page's URL to access other customers' transaction data, then exfiltrated it. Motivation appears financial, given the ransom demand.

**MITRE ATT&CK:** T1190 (Exploit Public-Facing Application)

**Additional notes:** The employee who first received the attacker's email claiming the data theft should have escalated it immediately rather than waiting for a follow-up message.

---

