# Network Traffic Analysis with Wireshark

![Wireshark](https://img.shields.io/badge/Tool-Wireshark-1679A7?style=flat&logo=wireshark&logoColor=white)
![PCAP](https://img.shields.io/badge/File-PCAP-blue)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

## Objective
Analyze DNS traffic captured in a PCAP file to identify abnormal or suspicious network behavior using Wireshark. This project simulates a real SOC analyst workflow: ingesting packet data, filtering for relevant protocols, and identifying indicators of compromise (IOCs).

---

## Tools Used
- Wireshark
- PCAP file sourced from [Malware Traffic Analysis](https://www.malware-traffic-analysis.net/)
  - ---

  ## Methodology

  ### 1. Applied DNS Display Filters
  Isolated DNS traffic using Wireshark's display filter:
  ```
  dns
  ```
  This narrowed thousands of packets down to DNS-specific traffic for focused analysis.

  ### 2. Investigated Internal Host Communication
  Identified internal host `10.2.28.88` making repeated DNS queries to internal DNS server `10.2.28.2`, which is normal behavior — but the *destinations* being resolved were not.

  ### 3. Analyzed Query Patterns
  Examined frequency, timing, and destination domains of DNS queries to distinguish legitimate traffic from anomalous behavior.

  ---

  ## Key Findings

  | Indicator | Detail |
  |---|---|
  | Affected Host | `10.2.28.88` |
  | DNS Server Queried | `10.2.28.2` |
  | Suspicious Domain | `easyas123.tech` |
  | Suspicious Subdomain | `wpad.easyas123.tech` |
  | Behavior | High-frequency repeated queries suggesting automated beaconing |

  ---

  ## MITRE ATT&CK Mapping

  | Technique | ID | Description |
  |---|---|---|
  | Application Layer Protocol: DNS | T1071.004 | Adversaries may use DNS to communicate with C2 infrastructure |
  | Dynamic Resolution | T1568 | Use of dynamically generated or unusual domains to evade detection |

  The repeated queries to `easyas123.tech` and its subdomains are consistent with **DNS beaconing**, a common C2 communication method used by malware such as NetSupport RAT.

  ---

  ## Why This Matters
  Repeated DNS queries to uncommon or newly registered domains can indicate:
  - **Malware beaconing** — malware checking in with a command-and-control server
  - - **Command-and-control (C2) communication** — adversary maintaining persistent access
    - - **Misconfigured systems** — WPAD (Web Proxy Auto-Discovery) misconfiguration being exploited
     
      - Detecting this pattern early in the kill chain prevents adversaries from establishing persistent footholds.
     
      - ---

      ## Screenshots
      *See dns-analysis.png in repository*

      ---

      ## Skills Demonstrated
      - Network traffic analysis
      - - DNS protocol understanding
        - - Wireshark display filtering
          - - IOC identification
            - - MITRE ATT&CK framework mapping
              - - Threat detection fundamentals
               
                - ---

                ## What I Would Investigate Next
                - Correlate `10.2.28.88` activity with other protocols (HTTP, HTTPS) to identify additional C2 channels
                - - Check for any successful connections to `easyas123.tech` using TCP/HTTP filters
                  - - Run the domain through threat intel feeds (VirusTotal, Shodan) to confirm malicious classification
                    - - Escalate as a confirmed IOC and recommend blocking the domain at the DNS/firewall level
                     
                      - ---

                      ## Disclaimer
                      This project is for educational purposes only using publicly available PCAP datasets from malware-traffic-analysis.net.
