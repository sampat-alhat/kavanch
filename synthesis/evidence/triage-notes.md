# A.2 Triage Pass – Initial Network Investigation

## Objective

Perform an initial triage analysis of the packet capture `2019-11-12-traffic-analysis-exercise.pcap` to identify key hosts, protocols, suspicious communications, and potential indicators of compromise.

---

## Capture Overview

The packet capture appears to represent traffic from a Windows Active Directory environment with multiple internal workstations communicating with both internal infrastructure and external Internet services.

The environment contains evidence of:

* Active Directory authentication
* File sharing activity
* Web browsing activity
* Encrypted HTTPS communications
* Unencrypted HTTP communications
* DNS lookups to both legitimate and suspicious domains

---

## Protocol Analysis

The most frequently observed protocols include:

| Protocol | Observation                       |
| -------- | --------------------------------- |
| TLS      | Dominant protocol in the capture  |
| HTTP     | Significant outbound web activity |
| LDAP     | Active Directory communications   |
| Kerberos | Domain authentication traffic     |
| SMB2     | File sharing activity             |
| LSARPC   | Windows security services         |
| DRSUAPI  | Directory replication activity    |

The protocol distribution is consistent with a Windows enterprise network.

---

## High-Activity Internal Hosts

| Internal Host | Packets | Bytes   |
| ------------- | ------- | ------- |
| 10.11.11.200  | 7,536   | 3.9 MB  |
| 10.11.11.179  | 5,806   | 3.2 MB  |
| 10.11.11.11   | 4,139   | 700 KB  |
| 10.11.11.217  | 4,037   | 1.95 MB |
| 10.11.11.203  | 1,379   | 613 KB  |

These systems were selected for further investigation due to their elevated traffic volumes.

---

## High-Activity External Hosts

| External Host  | Packets |
| -------------- | ------- |
| 151.101.50.208 | 3,270   |
| 172.217.6.162  | 1,206   |
| 104.18.74.113  | 1,079   |
| 31.13.93.26    | 711     |
| 13.33.255.25   | 728     |

Most communications utilized TLS over TCP/443, suggesting encrypted web activity.

---

## DNS Analysis

Frequently observed DNS requests include legitimate services such as:

* dns.msftncsi.com
* go.microsoft.com
* ctldl.windowsupdate.com
* [www.bing.com](http://www.bing.com)
* [www.google.com](http://www.google.com)
* [www.facebook.com](http://www.facebook.com)

However, several domains appear suspicious and do not resemble legitimate commercial or enterprise services:

* corposted.com
* magnwnce.com
* amongolia.com
* presifered.com
* coujtried.com
* jjanuatu.com

These domains may represent attacker-controlled infrastructure, malware distribution sites, or command-and-control resources.

---

## Suspicious Communication Identified

A notable communication was observed between:

Internal Host:

10.11.11.203

External Host:

188.95.248.71

Protocol:

HTTP (TCP/80)

Observed Request:

Host: acjabogados.com

Resource: /40group.tiff

This activity is unusual because:

* Most external communications in the capture use HTTPS.
* The communication uses unencrypted HTTP.
* The requested resource masquerades as a TIFF image.
* TIFF files are commonly abused by malware campaigns to deliver payloads or encoded command data.

---

## Initial Assessment

The communication between 10.11.11.203 and 188.95.248.71 is currently the strongest candidate for malicious activity within the capture.

The presence of suspicious DNS domains combined with an unusual HTTP request for a TIFF resource suggests possible malware infection and command-and-control activity.

---

## Recommended Next Steps

1. Extract all communications involving 10.11.11.203.
2. Review HTTP objects transferred from acjabogados.com.
3. Build an IOC list containing:

   * IP addresses
   * Domains
   * URLs
4. Correlate suspicious DNS lookups with outbound HTTP requests.
5. Develop and test investigative hypotheses.
6. Determine whether command-and-control activity or malware delivery occurred.

---

## Preliminary Conclusion

The network largely reflects normal enterprise Windows domain activity; however, host 10.11.11.203 exhibits suspicious outbound HTTP communications that warrant deeper investigation. Evidence collected during triage indicates potential malware-related activity and provides a basis for IOC extraction and hypothesis development in subsequent analysis phases.

