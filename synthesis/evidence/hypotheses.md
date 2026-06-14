# A.3 Hypothesis Development

## Hypothesis 1: Malware Payload Delivery

### Statement
Host 10.11.11.203 downloaded a potentially malicious payload from acjabogados.com.

### Supporting Evidence
- HTTP communication to 188.95.248.71
- Request for /40group.tiff
- Unencrypted HTTP traffic

### Evidence That Would Refute
- File verified as legitimate image
- No execution or follow-on activity

### Verdict
Likely malicious

### Confidence
High

---

## Hypothesis 2: Command and Control Infrastructure

### Statement
Suspicious domains may represent malware C2 infrastructure.

### Supporting Evidence
- corposted.com
- magnwnce.com
- amongolia.com
- presifered.com
- coujtried.com
- jjanuatu.com

### Evidence That Would Refute
- Domains belong to legitimate services

### Verdict
Suspicious

### Confidence
Medium

---

## Hypothesis 3: Legitimate Enterprise Traffic

### Statement
The majority of TLS traffic is normal enterprise browsing and updates.

### Supporting Evidence
- Microsoft Update domains
- Google domains
- Facebook domains
- DigiCert OCSP traffic

### Evidence That Would Refute
- Malicious content delivered through trusted services

### Verdict
Likely benign

### Confidence
High
