# Challenge 03: PCAP Forensics - The Hidden Credential

> **Category:** Forensics  
> **Difficulty:** Medium  
> **Points:** 200  
> **Author:** Coach Ay (MAPELEAD)

---

## 🎯 Objective

Analyze the provided PCAP file to extract the hidden credentials and find the flag.

## 📜 Scenario

A security analyst captured network traffic from a suspected compromised workstation. The attacker performed several actions including data exfiltration. Your task is to analyze the PCAP and:

1. Find the attacker's IP address
2. Extract the stolen credentials
3. Identify the exfiltrated data
4. Find the flag

## 📁 Files

- `suspicious-traffic.pcap` - The network capture file
- `generate-pcap.py` - Script that generated this challenge (don't peek until after solving!)

## 🛠️ Tools You'll Need

- Wireshark or tshark
- NetworkMiner (optional)
- Python with scapy

## 🚀 Getting Started

```bash
# Basic analysis with tshark
tshark -r suspicious-traffic.pcap -q -z conv,tcp

# Extract HTTP objects
tshark -r suspicious-traffic.pcap --export-objects http,./extracted/

# Filter for specific traffic
tshark -r suspicious-traffic.pcap -Y "http.request" -T fields -e ip.src -e http.host -e http.request.uri
```

## 💡 Hints

<details>
<summary>Hint 1</summary>

Look for HTTP traffic first. What websites were visited? Any login forms?

</details>

<details>
<summary>Hint 2</summary>

Check for DNS queries. The attacker might have communicated with a C2 domain.

</details>

<details>
<summary>Hint 3</summary>

Look at the packet payloads carefully. Is there any data that looks encoded or encrypted?

</details>

## ✅ Solution

<details>
<summary>SPOILER: Click to reveal</summary>

### Step-by-Step Analysis

1. **Attacker IP:** 192.168.1.100 (most external connections originate from here)

2. **C2 Domain:** evil-c2.mapelead-lab.com (found in DNS queries)

3. **Stolen Credentials:** Found in HTTP POST request:
   ```
   username=admin&password=Sup3rS3cretP@ss!
   ```

4. **Flag:** Found in the final TCP stream, base64 encoded:
   ```
   RkxBR3tQQUNQX0FOQUxZU0lTX1RoM0tfTjB3fQ==
   ```
   
   Decoded: `FLAG{PCAP_ANALYSI5_Th3k_N0w}`

</details>

## 📚 Learning Outcomes

- Network traffic analysis with Wireshark/tshark
- Protocol analysis (HTTP, DNS, TCP)
- Extracting artifacts from PCAP files
- Base64 encoding/decoding
- Identifying C2 communications

---

*Challenge created by MAPELEAD | For educational purposes only*
