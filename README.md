# 🔍 Wireshark Network Attack Analysis (TCP SYN Scan + Web Probing)

## 🎯 Objective

Analyze a real PCAP file to identify network scanning and web probing activity against a target server.

---

## 🧠 Scenario

A public-facing server is receiving abnormal traffic from multiple external sources. The objective is to determine whether this activity represents a security threat.

---

## 🔎 Key Findings

### 🔹 Target Identification

* **Victim Server:** 203.161.44.208
* Multiple external IPs initiated connections to this server

---

### 🔹 TCP SYN Scan Detection

* Observed a high volume of TCP SYN packets
* Behavior pattern:

  * SYN → RST, ACK → Closed port
  * SYN → SYN-ACK → Open port

👉 Indicates **TCP SYN scanning activity**

---

### 🔹 Ports Targeted

Attackers probed multiple services:

* 22 (SSH)
* 25 (SMTP)
* 80 (HTTP)
* 443 (HTTPS)
* 636 (LDAPS)
* 8080 / 8443

---

### 🔹 Web Probing Activity

Observed HTTP requests targeting sensitive and vulnerable paths:

* `/.env`
* `/.git/config`
* `/vendor/phpunit/...`
* `/admin`, `/login`

Responses:

* Mostly **404 Not Found**
* Some **200 OK**

👉 Indicates **web application probing**

---

## 🧭 Attack Timeline

1. External hosts initiated TCP SYN scan
2. Server responded with port status
3. Attackers identified open services
4. HTTP probing activity began
5. Attempts to access sensitive files and vulnerabilities observed

---

## 🚨 Conclusion

The server **203.161.44.208** is under active attack involving:

* TCP SYN scanning (reconnaissance phase)
* Web probing (vulnerability discovery phase)

This behavior is consistent with **automated attack tools attempting to identify exploitable services**.

---

## 🛠 Tools Used

* Wireshark

---

## 💡 Skills Demonstrated

* Network traffic analysis
* TCP flag interpretation
* Port scanning detection
* Web attack identification
* Incident response analysis

---

## 📸 Screenshots

Refer to the images in this repository for evidence of:

* SYN scanning
* Port responses
* Web probing activity
