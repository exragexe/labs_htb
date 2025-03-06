### Network Reconnaissance

- **Nmap Scan:**  
    Discovered open ports and services on the target host:
    
    - **Host:** Linux 5.X
    - **Open Ports:**
        - **22/tcp:** SSH (OpenSSH 8.9p1 Ubuntu 3ubuntu0.10)
            
            - **SSH Host Keys:**
                - ECDSA: `48:b0:d2:c7:29:26:ae:3d:fb:b7:6b:0f:f5:4d:2a:ea`
                - ED25519: `cb:61:64:b8:1b:1b:b5:ba:b8:45:86:c5:16:bb:e2:a2`
            
        - **80/tcp:** HTTP (Apache httpd 2.4.52 (Ubuntu))
        - **161/udp:** SNMP
    
- **SNMP Enumeration:**
	Using msfconsole with moudule auxiliary(scanner/snmp/snmp_enum)
	Gathered system information via SNMP:
	- **Host IP:** 10.10.11.48
	- **Hostname:** UnDerPass.htb is the only ==daloradius== server in the basin!
	- **Description:** Linux underpass 5.15.0-126-generic #136-Ubuntu SMP Wed Nov 6 10:38:22 UTC 2024 x86_64
	- **Contact:** [steve@underpass.htb](mailto:steve@underpass.htb)
	- **Location:** Nevada, U.S.A. but not Vegas
	- **Uptime SNMP:** 01:43:54.75
	- **Uptime System:** 01:43:44.03
	- **System Date:** 2025-1-21 18:22:45.0
### Web Enumeration

- **Directory Discovery:**  
    Used `dirsearch` to enumerate directories http://underpass.htb/daloradius:
### Directory and File Enumeration Results

| **Time**       | **Status** | **Size** | **Path**                                   | **Redirect**                                  |
| -------------- | ---------- | -------- | ------------------------------------------ | --------------------------------------------- |
| [14:19:02]     | Starting   | -        | `/daloradius/`                             | -                                             |
| [14:19:05]     | 200        | 221B     | `/daloradius/.gitignore`                   | -                                             |
| [14:19:26]     | 301        | 323B     | `/daloradius/app`                          | `http://underpass.htb/daloradius/app/`        |
| [14:32:08]     | 301        | 330B     | `/daloradius/app/common`                   | `http://underpass.htb/daloradius/app/common/` |
| [14:45:02]     | 404        | 0B       | `/daloradius/app/common/includes/mail.php` | -                                             |
| [14:33:19]     | 301        | 329B     | `/daloradius/app/users`                    | `http://underpass.htb/daloradius/app/users/`  |
| [14:33:19]     | 200        | 2KB      | `/daloradius/app/users/login.php`          | -                                             |
| [14:33:19]     | 302        | 0B       | `/daloradius/app/users/`                   | `home-main.php`                               |
| [14:19:31]     | 200        | 24KB     | `/daloradius/ChangeLog`                    | -                                             |
| [14:19:39]     | 301        | 323B     | `/daloradius/doc`                          | `http://underpass.htb/daloradius/doc/`        |
| ==[15:39:51]== | ==200==    | ==8KB==  | ==/daloradius/doc/install/INSTALL==        | ==-==                                         |
| ==[14:19:39]== | ==200==    | ==2KB==  | ==/daloradius/docker-compose.yml==         | ==-==                                         |
| [14:19:39]     | 200        | 2KB      | `/daloradius/Dockerfile`                   | -                                             |
| [14:19:52]     | 301        | 327B     | `/daloradius/library`                      | `http://underpass.htb/daloradius/library/`    |
| [14:19:53]     | 200        | 18KB     | `/daloradius/LICENSE`                      | -                                             |
| [14:20:13]     | 200        | 10KB     | `/daloradius/README.md`                    | -                                             |
| [14:20:18]     | 301        | 325B     | `/daloradius/setup`                        | `http://underpass.htb/daloradius/setup/`      |
Second enumeration
Using wordlist: /usr/share/wordlists/gobuster/directory-list-2.3-medium.txt and found operators directory, then we use default wordlist and found file login.php and login there: http://underpass.htb/daloradius/app/operators/home-main.php

### Docker Configuration Details

- **Docker Compose File Analysis:**  
    Extracted sensitive configuration details from `docker-compose.yml`:
	services:
  radius-mysql:
    image: mariadb:10
    container_name: radius-mysql
    restart: unless-stopped
    environment:
	    ==- MYSQL_DATABASE=radius==
      ==- MYSQL_USER=radius==
      ==- MYSQL_PASSWORD=raxxxxxxx
      ==- MYSQL_ROOT_PASSWORD=raxxxxxxxxxx==
    volumes:
      - "./data/mysql:/var/lib/mysql"
	<SNIP>
	....
	<SNIP>
  

