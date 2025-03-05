# Network Security Auditing using Command Line Utilities

## **Description**
This lab will demonstrate how to perform **network security auditing** using command-line utilities. 

## **Lab Walk Through**

#### Verifying DNS Security and Identifying Risks**
#### **Steps:**
1. Open **Command Prompt** (`cmd`).
2. Type `nslookup` and press **Enter**.
3. Enter interactive mode and run:
   set type=a
   www.certifiedhacker.com
   ```
   - **Security Insight:** If the response is **non-authoritative**, check if an attacker could **spoof DNS responses**.
   <p align="center">
<br/>
<p align="center"><img src="https://i.imgur.com/xhT0mpO.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
4. Check for CNAME records:
   ```sh
   set type=cname
   certifiedhacker.com
   ```
5. Identify the authoritative DNS:
   ```sh
   set type=a
   ns1.bluehost.com
   ```
   - **Security Concern:** If an attacker discovers the **primary name server**, they might target it for **DNS hijacking**.

### **2. Tracing Network Path for Potential Exposure**
#### **Steps:**
1. Run traceroute to examine network hops:
   ```sh
   tracert www.certifiedhacker.com
   ```
   - **Audit Insight:** Identify if traffic passes through **unauthorized or insecure nodes**.
2. Limit hops for quick internal audits:
   ```sh
   tracert -h 5 www.certifiedhacker.com
   ```

### **3. Identifying ARP Cache Manipulation**
#### **Steps:**
1. Display the ARP cache:
   ```sh
   arp -a
   ```
   - **Security Focus:** Look for unexpected **IP-to-MAC mappings**, which could indicate **ARP spoofing**.

### **4. Analyzing Network Traffic for Potential Intrusions**
#### **Steps:**
1. Run `pathping` to detect packet loss:
   ```sh
   pathping -n www.certifiedhacker.com
   ```
   - **Audit Concern:** Consistent high latency may indicate a **DoS attack**.
2. Check network statistics:
   ```sh
   netstat -e
   ```
   - **Audit Focus:** Analyze for **unexpected spikes in sent/received bytes**.
3. List all active connections:
   ```sh
   netstat -an
   ```
   - **Security Consideration:** Identify **unknown foreign IP addresses**.

### **5. Checking for Exposed Services**
#### **Steps:**
1. Display open ports:
   ```sh
   netstat -ano
   ```
2. Find services linked to open ports:
   ```sh
   tasklist /fi "pid eq <PID>"
   ```
   - Replace `<PID>` with the actual process ID.
   - **Audit Concern:** Flag unexpected **processes communicating over the network**.

---

## **Attacker Machine-2: Simulating an External Audit**
#### **Steps:**
1. Open **Parrot Terminal**.
2. Run traceroute:
   ```sh
   traceroute www.certifiedhacker.com
   ```
3. Query DNS name servers:
   ```sh
   dig ns certifiedhacker.com
   ```
4. Test for DNS zone transfers:
   ```sh
   dig @ns1.bluehost.com certifiedhacker.com axfr
   ```
   - **Audit Concern:** If **zone transfer succeeds**, DNS misconfiguration allows **data leakage**.

---

## **Conclusion**
This lab enhances network auditing skills by:
- Identifying **DNS vulnerabilities** that could lead to **spoofing or hijacking**.
- Evaluating **network path security** and flagging **suspicious hops**.
- Detecting **ARP spoofing** that could allow attackers to intercept traffic.
- Auditing **open ports** and active connections for **potential security breaches**.
- Testing **zone transfer vulnerabilities** to prevent **unauthorized data leakage**.

**Final Step:**
- Document findings and **recommend fixes** for each identified issue.
- Ensure **proper network hardening measures** are in place.

---

## **Modified Lab Question:**
**Q:** In Admin Machine-1, use `netstat` to display both the incoming and outgoing TCP/IP traffic to www.certifiedhacker.com. What parameter displays the Ethernet statistics?

**A:**
```sh
netstat -e
```
- Displays **Ethernet statistics**, including **bytes and packets sent/received**.
- Helps auditors detect **suspicious traffic patterns**.

---

## **Why This Version is Better for Auditing?**
✅ **Shifts** from troubleshooting to **security auditing**  
✅ **Focuses** on detecting vulnerabilities and preventing attacks  
✅ **Enhances** compliance verification for **network security policies**  

---

### **📌 Upload this to GitHub & Share with Your Team!** 🚀
