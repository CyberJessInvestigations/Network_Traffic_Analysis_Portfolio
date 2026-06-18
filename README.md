# Network_Traffic_Analysis_Portfolio
Network traffic analysis portfolio project using Wireshark to investigate a malicious PCAP, identify NetSupport Manager RAT activity, extract IOCs, and enrich findings with threat intelligence tools.
# Network Traffic Analysis: NetSupport Manager RAT Investigation

## Project Overview

This project analyzes a malicious PCAP from Malware-Traffic-Analysis.net using Wireshark. The investigation focuses on identifying the infected host, reviewing DNS and HTTP traffic, extracting indicators of compromise, and confirming NetSupport Manager RAT activity through threat intelligence enrichment.

## Objective

The goal of this project was to investigate suspicious network traffic, identify the infected Windows host, collect IOCs, and document the findings in a professional incident-style report.

## Tools Used

* Wireshark
* VirusTotal
* AbuseIPDB
* AlienVault OTX
* Shodan
* Malware-Traffic-Analysis.net

## PCAP Source

* Source: Malware-Traffic-Analysis.net
* Exercise: 2026-02-28 Traffic Analysis Exercise — Easy as 123
* Malware Family: NetSupport Manager RAT

Note: The raw PCAP file is not included in this repository. This project only includes screenshots, notes, and the final report for documentation purposes.

## Key Findings

* Identified the suspected infected host as `10.2.28.88`
* Confirmed NetSupport Manager RAT traffic
* Observed repeated HTTP POST requests to suspicious external infrastructure
* Identified the suspicious IP address `45.131.214.85`
* Identified the suspicious domain `vadusa.xyz`
* Found repeated traffic to the `fakeurl.htm` endpoint
* Enriched IOCs using VirusTotal, AbuseIPDB, AlienVault OTX, and Shodan
* Compared findings against the official Malware-Traffic-Analysis.net answer key

## Indicators of Compromise

| Type        | Value                              | Description                                                                                   | Source                             |
| ----------- | ---------------------------------- | --------------------------------------------------------------------------------------------- | ---------------------------------- |
| IP Address  | `45.131.214.85`                    | External IP contacted by the infected host and associated with NetSupport Manager RAT traffic | Wireshark, VirusTotal, OTX, Shodan |
| Domain      | `vadusa.xyz`                       | Suspicious domain that resolved to `45.131.214.85`                                            | Wireshark DNS, VirusTotal, OTX     |
| URL         | `http://45.131.214.85/fakeurl.htm` | Repeated HTTP POST endpoint observed in traffic                                               | Wireshark, VirusTotal              |
| HTTP Object | `fakeurl.htm`                      | Repeated HTTP object associated with suspicious POST traffic                                  | Wireshark HTTP Objects             |
| User-Agent  | `NetSupport Manager/1.3`           | User-Agent observed in suspicious POST traffic                                                | Wireshark HTTP Stream              |

## Malware Identification

The traffic was identified as NetSupport Manager RAT activity. This was supported by repeated HTTP POST requests, the `NetSupport Manager/1.3` User-Agent, command-style fields in the HTTP stream, and confirmation from the Malware-Traffic-Analysis.net answer key.

## Threat Intelligence Summary

VirusTotal flagged the IP, domain, and URL as malicious. AlienVault OTX confirmed domain and infrastructure details, while Shodan showed that the suspicious IP had port 80 open and was running a Python-based HTTP server. AbuseIPDB did not report abuse for the IP, which was documented as a negative finding.

## Report

The full report is included in this repository:

`Network_Traffic_Analysis_Report.pdf`

## Screenshots

Screenshots are included to document the investigation process, including:

* Wireshark infected host filtering
* DNS analysis
* HTTP POST traffic
* HTTP stream analysis
* HTTP Objects export
* VirusTotal results
* AbuseIPDB results
* AlienVault OTX results
* Shodan results
* Malware-Traffic-Analysis.net answer key comparison

## Lessons Learned

This project helped strengthen my understanding of malicious PCAP analysis, IOC extraction, HTTP POST traffic review, DNS investigation, and threat intelligence enrichment. It also showed the importance of validating findings across multiple tools and documenting negative findings when a platform does not return results.
## Contact

- GitHub: [CyberJessInvestigations](https://github.com/CyberJessInvestigations)
- LinkedIn: Add your www.linkedin.com/in/jessicasansaricq
- Portfolio/YouTube: https://www.youtube.com/@CyberJessInvestigations
## Copyright / Usage Notice
© 2026 Jessica Sansaricq. This project is provided for educational and portfolio purposes. Please do not copy, redistribute, or present this work as your own.
