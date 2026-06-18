# Network Traffic Analysis Portfolio

Network traffic analysis portfolio project using Wireshark to investigate a malicious PCAP, identify NetSupport Manager RAT command-and-control activity, extract indicators of compromise, enrich findings with threat intelligence tools, and perform a host identification follow-up.

## Projects Included

### 01 — NetSupport Manager RAT C2 Investigation

This project analyzes a malicious PCAP from Malware-Traffic-Analysis.net using Wireshark. The investigation focuses on identifying the infected host, reviewing DNS and HTTP traffic, extracting indicators of compromise, confirming NetSupport Manager RAT activity, and enriching findings with threat intelligence tools.

**Folder:** `report/` and `screenshots/`

### 02 — Host Identification Follow-Up

This follow-up investigation goes one layer deeper by identifying host-level details tied to the infected IP address. The analysis focuses on finding or confirming the infected host’s MAC address, hostname, Windows username, and full name using Wireshark and the official Malware-Traffic-Analysis.net answer key.

**Folder:** `host-identification-follow-up/`

---

# Network Traffic Analysis: NetSupport Manager RAT Investigation

## Project Overview

This project analyzes a malicious network traffic capture from Malware-Traffic-Analysis.net using Wireshark. The investigation focuses on identifying the infected Windows host, reviewing DNS and HTTP traffic, analyzing suspicious HTTP POST requests, extracting indicators of compromise, and confirming NetSupport Manager RAT command-and-control activity.

The scenario involves a compromised Windows workstation communicating with suspicious external infrastructure. The infected host sent repeated outbound HTTP POST requests to an attacker-controlled server using traffic that appeared to blend in with normal web communication.

## Objective

The goal of this project was to investigate suspicious network traffic, identify the infected Windows host, collect indicators of compromise, confirm the malware family, and document the findings in a professional incident-style report.

This project demonstrates how network traffic analysis can be used to answer important incident response questions, including:

* Which internal host was infected?
* What external IP address did the host communicate with?
* What suspicious domain and URL were involved?
* What network behavior indicated command-and-control activity?
* What malware family was associated with the traffic?
* What IOCs should be blocked or monitored?
* What response actions should be taken?

## Tools Used

* Wireshark
* VirusTotal
* AbuseIPDB
* AlienVault OTX
* Shodan
* Malware-Traffic-Analysis.net
* GitHub

## PCAP Source

Source: Malware-Traffic-Analysis.net
Exercise: 2026-02-28 Traffic Analysis Exercise — Easy as 123
Malware Family: NetSupport Manager RAT

Note: The raw PCAP file is not included in this repository. This project only includes screenshots, notes, indicators of compromise, and final reports for documentation purposes.

## Case Summary

| Field             | Value                            |
| ----------------- | -------------------------------- |
| Incident Date     | 2026-02-28                       |
| Report Date       | 2026-06-10                       |
| PCAP Source       | Malware-Traffic-Analysis.net     |
| Infected Host     | 10.2.28.88                       |
| Hostname          | DESKTOP-TEYQ2NR                  |
| MAC Address       | 00:19:d1:b2:4d:ad                |
| Windows Account   | brolf                            |
| Full Name         | Becka Rolf                       |
| Malware Family    | NetSupport Manager RAT           |
| C2 IP Address     | 45.131.214.85                    |
| Suspicious Domain | vadusa.xyz                       |
| Suspicious URL    | http://45.131.214.85/fakeurl.htm |
| Severity          | High                             |
| Status            | Investigation Completed          |

## Investigation Workflow

The investigation followed a structured network traffic analysis workflow:

1. Opened the PCAP in Wireshark.
2. Reviewed endpoint statistics.
3. Reviewed conversation statistics.
4. Identified the most active internal host.
5. Filtered DNS traffic for suspicious domain queries.
6. Identified the suspicious domain `vadusa.xyz`.
7. Confirmed the domain resolved to `45.131.214.85`.
8. Filtered HTTP POST traffic.
9. Identified repeated POST requests to `/fakeurl.htm`.
10. Followed the suspicious TCP stream.
11. Confirmed the `NetSupport Manager/1.3` User-Agent string.
12. Extracted indicators of compromise.
13. Enriched IOCs using VirusTotal, AbuseIPDB, AlienVault OTX, and Shodan.
14. Identified the malware family as NetSupport Manager RAT.
15. Documented findings and recommended response actions.

## Key Findings

The investigation identified a compromised Windows host communicating with suspicious external infrastructure.

Key findings included:

* Internal host `10.2.28.88` was identified as the infected system.
* The infected host communicated with external IP `45.131.214.85`.
* DNS traffic showed the suspicious domain `vadusa.xyz`.
* The domain resolved to the same external IP address used in suspicious HTTP traffic.
* HTTP POST traffic showed repeated requests to `http://45.131.214.85/fakeurl.htm`.
* The HTTP User-Agent was `NetSupport Manager/1.3`.
* TCP stream analysis confirmed suspicious NetSupport Manager communication.
* Threat intelligence tools flagged the IP, domain, and URL as malicious or suspicious.
* The traffic was consistent with NetSupport Manager RAT command-and-control behavior.

## Indicators of Compromise

| Type        | Value                            | Description                                                                                   | Source                             |
| ----------- | -------------------------------- | --------------------------------------------------------------------------------------------- | ---------------------------------- |
| IP Address  | 45.131.214.85                    | External IP contacted by the infected host and associated with NetSupport Manager RAT traffic | Wireshark, VirusTotal, OTX, Shodan |
| Domain      | vadusa.xyz                       | Suspicious domain resolving to 45.131.214.85                                                  | Wireshark DNS, VirusTotal, OTX     |
| URL         | http://45.131.214.85/fakeurl.htm | Repeated HTTP POST endpoint observed in traffic                                               | Wireshark, VirusTotal              |
| HTTP Object | fakeurl.htm                      | Repeated HTTP object associated with suspicious POST traffic                                  | Wireshark HTTP Objects             |
| User-Agent  | NetSupport Manager/1.3           | User-Agent observed in suspicious POST traffic                                                | Wireshark HTTP Stream              |

## Malware Identification

The traffic was identified as NetSupport Manager RAT activity. This was supported by repeated HTTP POST requests, the `NetSupport Manager/1.3` User-Agent string, suspicious command-and-control infrastructure, and confirmation from the Malware-Traffic-Analysis.net answer key.

NetSupport Manager is a legitimate remote-access product, but threat actors frequently abuse it as a remote access trojan for unauthorized access, remote control, and command-and-control activity.

## Threat Intelligence Summary

The extracted IOCs were enriched using multiple threat intelligence tools.

* VirusTotal flagged the IP address, domain, and URL as malicious or suspicious.
* AlienVault OTX confirmed domain and infrastructure relationships.
* Shodan showed that the suspicious IP had exposed web services and was running a Python-based HTTP server.
* AbuseIPDB did not report abuse for the IP address, which was documented as a negative finding.

Using multiple enrichment sources helped validate the packet-level findings from Wireshark.

---

# Host Identification Follow-Up

## Follow-Up Overview

After completing the main NetSupport RAT C2 investigation, a follow-up analysis was performed to identify host-level details tied to the infected IP address.

The purpose of this follow-up was to show how an analyst can move beyond identifying a suspicious IP and determine the specific device and user account involved in the incident.

## Follow-Up Objective

The goal of the host identification follow-up was to identify or confirm:

* The infected host IP address
* The MAC address
* The hostname
* The Windows username
* The full user name

## Host Identification Findings

| Field            | Value             | Source                      |
| ---------------- | ----------------- | --------------------------- |
| Infected Host IP | 10.2.28.88        | Wireshark                   |
| Hostname         | DESKTOP-TEYQ2NR   | Wireshark / Answer Key      |
| MAC Address      | 00:19:d1:b2:4d:ad | Wireshark Ethernet II       |
| Windows Username | brolf             | Answer Key / Search Attempt |
| Full Name        | Becka Rolf        | Answer Key                  |

## Follow-Up Methodology

The follow-up investigation used Wireshark to focus on the known infected host.

Filters and methods used included:

```text
ip.addr == 10.2.28.88
```

Used to focus only on traffic involving the infected host.

```text
eth.addr == 00:19:d1:b2:4d:ad
```

Used to verify traffic associated with the infected host’s MAC address.

```text
nbns
```

Used to locate Windows hostname information.

```text
frame contains "brolf"
frame contains "Becka"
frame contains "Rolf"
```

Used to search the packet capture for username or full-name artifacts.

## Follow-Up Findings Summary

The MAC address was found by selecting traffic from `10.2.28.88` and expanding the Ethernet II details in Wireshark. The hostname was identified through local name resolution traffic such as NBNS. The username and full name were harder to locate directly in the PCAP, so those details were documented and confirmed using the official exercise answer key.

This follow-up helped demonstrate that host identification is an important part of incident response. Finding the infected IP is useful, but identifying the hostname, MAC address, and user account gives the response team the information needed to isolate the correct device and reset affected credentials.

---

# Repository Structure

```text
Network_Traffic_Analysis_Portfolio/
│
├── README.md
│
├── report/
│   └── Network_Traffic_Analysis_Report.pdf
│
├── screenshots/
│   ├── 01_ipv4_endpoints.png
│   ├── 02_ipv4_conversations.png
│   ├── 03_dns_failures.png
│   ├── 04_suspicious_dns.png
│   ├── 05_post_stream.png
│   ├── 07_vt_ip_45.131.214.85.png
│   ├── 08_vt_domain_vadusa.xyz.png
│   ├── 09_vt_url.png
│   ├── 10_abuseipdb.png
│   ├── 11_alienvaultotx_ip.png
│   ├── 12_alienvaultotx_domain.png
│   ├── 13_alienvaultotx_url.png
│   ├── 14_shodan_ip.png
│   ├── 15_shodan_domain.png
│   └── 16_shodan_html.png
│
└── host-identification-follow-up/
    ├── screenshots/
    │   ├── 01_infected_host_filter.png
    │   ├── 02_mac_address_ethernet.png
    │   ├── 03_hostname_discovery.png
    │   ├── 04_username_search.png
    │   └── 05_answer_key.png
    │
    ├── notes/
    │   └── host_identification_notes.txt
    │
    └── report/
        └── Host_Identification_Wireshark_Report.pdf
```

## Reports

The full reports are included in this repository:

* `report/Network_Traffic_Analysis_Report.pdf`
* `host-identification-follow-up/report/Host_Identification_Wireshark_Report.pdf`

## Screenshots

Screenshots are included to document the investigation process, including:

* Wireshark endpoint analysis
* Wireshark conversation analysis
* DNS analysis
* HTTP POST traffic
* TCP stream analysis
* VirusTotal results
* AbuseIPDB results
* AlienVault OTX results
* Shodan results
* Infected host filtering
* MAC address discovery
* Hostname discovery
* Username search
* Answer key comparison

## Lessons Learned

This project strengthened my understanding of malicious PCAP analysis, IOC extraction, HTTP POST traffic review, DNS investigation, threat intelligence enrichment, and host identification.

The main investigation showed how network traffic can reveal command-and-control behavior, while the follow-up demonstrated how to connect an infected IP address to a specific device and user account.

This project also showed the importance of validating findings across multiple tools and documenting negative findings when a platform does not return results.

## Disclaimer

This project was completed in a controlled lab environment using a public malware traffic analysis exercise from Malware-Traffic-Analysis.net. No real systems were attacked, and no live malware was executed by me.

The raw PCAP file is not included in this repository. This repository only contains screenshots, notes, indicators of compromise, and final reports for educational and portfolio purposes.

## AI Use Disclosure

AI tools were used as a learning and documentation support resource for project planning, explanation, formatting, and writing refinement. All screenshots, analysis decisions, Wireshark review, IOC documentation, and final conclusions were reviewed and completed by me.

## Copyright / Usage Notice

© 2026 Jessica Sansaricq. This project is provided for educational and portfolio purposes only. The reports, screenshots, notes, and analysis are my original portfolio work. Please do not copy, redistribute, or present this project as your own.

This repository does not include live malware, raw PCAP files, private data, credentials, or confidential organizational information.

## Contact

GitHub: CyberJessInvestigations
LinkedIn: [www.linkedin.com/in/jessicasansaricq](http://www.linkedin.com/in/jessicasansaricq)
Portfolio/YouTube: https://www.youtube.com/@CyberJessInvestigations
