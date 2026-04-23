# 🔍 Wireshark Network Attack Analysis.

---

## 🧾 Summary

In this lab, I analyzed a PCAP file using Wireshark to investigate suspicious traffic targeting a server.
The analysis revealed **TCP SYN scanning followed by web probing activity**, which represents a real-world attack pattern.

---

# 🧠 Investigation Steps

---

## 🔹 Step 1: Identify Suspicious Activity

I started by checking network conversations to identify unusual traffic patterns.

📸 **Conversations View**
![Step 1](screenshots/01-conversations.png)

🔍 Observation:

* Multiple external IPs communicating with a single host
* High number of small packet exchanges

👉 This indicated potential **scanning activity**

---

## 🔹 Step 2: Filter Suspicious IP Activity

Applied filter:

```
ip.addr == 203.161.44.208
```

📸 **Filtered Traffic**
![Step 2](screenshots/02-syn-scan.png)

🔍 Observation:

* High volume of TCP packets
* Repeated connection attempts

👉 Identified **target server under attack**

---

## 🔹 Step 3: Detect SYN Scan Behavior

Applied filter:

```
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

📸 **SYN Scan Packets**
![Step 3](screenshots/03-syn-scan-filter.png)

🔍 Observation:

* Multiple SYN packets from different IPs
* Targeting various ports

👉 Confirmed **TCP SYN scanning**

---

## 🔹 Step 4: Analyze Port Responses

📸 **RST Responses (Closed Ports)**
![Step 4](screenshots/03-rst-response.png)

📸 **SYN-ACK Responses (Open Ports)**
![Step 4-2](screenshots/04-syn-ack.png)

🔍 Observation:

* RST, ACK → Closed ports
* SYN-ACK → Open ports

👉 Attackers identifying available services

---

## 🔹 Step 5: Identify Targeted Ports

📸 **TCP Port Activity**
![Step 5](screenshots/04-tcp.png)

🔍 Observation:

* Ports targeted:

  * 22 (SSH)
  * 25 (SMTP)
  * 80 (HTTP)
  * 443 (HTTPS)
  * 636 (LDAPS)
  * 8080 / 8443

👉 Indicates **service discovery attempt**

---

## 🔹 Step 6: Identify Victim and Attack Pattern

📸 **Multiple Sources → One Target**
![Step 6](screenshots/01-conversations.png)

🔍 Observation:

* Many IPs → One server

👉 This confirms:

* Server is **victim**
* External IPs are **attackers**

---

## 🔹 Step 7: Detect Web Probing Activity

Applied filter:

```
http
```

📸 **HTTP Requests**
![Step 7](screenshots/05-http-probing.png)

🔍 Observation:

* Requests to:

  * `/.env`
  * `/.git/config`
  * `/vendor/phpunit/...`
  * `/admin`, `/login`

* Responses:

  * 404 Not Found
  * 200 OK

👉 Indicates **web vulnerability probing**

---

# 🧭 Attack Timeline

1. External hosts initiated TCP SYN scan
2. Server responded with port status
3. Attackers identified open services
4. Web probing activity began
5. Attempts made to access sensitive files and vulnerabilities

---

# 🚨 Conclusion

The server **203.161.44.208** is under active attack involving:

* TCP SYN scanning (reconnaissance)
* Web probing (vulnerability discovery)

👉 This behavior matches **automated attacker tools used in real-world environments**

---

# 🛠 Tools Used

* Wireshark

---

# 💡 Skills Demonstrated

* Packet analysis
* TCP flag interpretation
* Port scanning detection
* Web attack identification
* Incident investigation

---
