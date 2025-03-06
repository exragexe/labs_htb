1. **FTP Credentials Leak:**
    
    - **Description:** A pcap file in `/data/0` contained FTP login credentials (`nathan:<REDACTED>).
    - **Impact:** An attacker could authenticate via FTP to gain access to the system.
    
2. **Privilege Escalation via Python3 Capabilities:**
    
    - **Description:** The file `/usr/bin/python3.8` had elevated capabilities (`cap_setuid,cap_net_bind_service+eip`).
    - **Impact:** An attacker could exploit this to escalate privileges to root.