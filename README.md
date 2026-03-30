# network-traffic-analysis-wireshark
Wireshark DNS traffic analysis project identifying suspicious domain behavior

# Network Traffic Analysis with Wireshark

## Objective
Analyze DNS traffic to identify abnormal or suspicious network behavior using Wireshark.

## Tools Used
- Wireshark
- PCAP file (Malware Traffic Analysis dataset)

## What I Did
- Applied DNS filters to isolate traffic
- Investigated internal host communication
- Analyzed repeated domain queries
- Identified suspicious DNS patterns

## Key Findings
- Internal host 10.2.28.88 repeatedly queried DNS server 10.2.28.2
- Multiple requests to domain: easyas123.tech
- Frequent queries to subdomains such as wpad.easyas123.tech
- High frequency suggests automated or suspicious behavior

## Why This Matters
Repeated DNS requests to uncommon domains can indicate:
- Malware beaconing
- Command-and-control communication
- Misconfigured systems

## Skills Demonstrated
- Network traffic analysis
- DNS protocol understanding
- Wireshark filtering
- Threat detection fundamentals

## Disclaimer
This project is for educational purposes only using publicly available datasets.
