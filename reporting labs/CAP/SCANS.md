### Network Reconnaissance

- **Nmap Scan:**  
    Discovered open ports and services on the target host:
    - **Host:** Linux
    - **Open Ports:**
        - **21/tcp:** FTP (vsftpd 3.0.3)
        - **22/tcp:** SSH (OpenSSH 8.2p1 Ubuntu 4ubuntu0.2)
            
            - **SSH Host Keys:**
                - RSA: `fa:80:a9:b2:ca:3b:88:69:a4:28:9e:39:0d:27:d5:75`
                - ECDSA: `96:d8:f8:e3:e8:f7:71:36:c5:49:d5:9d:b6:a4:c9:0c`
                - ED25519: `3f:d0:ff:91:eb:3b:f6:e1:9f:2e:8d:de:b3:de:b2:18`
            
        - **80/tcp:** HTTP (gunicorn)

### Web Enumeration

- **Directories:**  
    Found interesting directories during enumeration:
    
    |TIME|STATUS|SIZE|PATH|
    |---|---|---|---|
    |[10:05:31]|302|208B|/data ->[http://cap.htb/](http://cap.htb/)|
    |[10:05:31]|302|208B|/data/adminer.php ->[http://cap.htb/](http://cap.htb/)|
    |[10:05:31]|302|208B|/data/autosuggest ->[http://cap.htb/](http://cap.htb/)|
    |[10:05:34]|302|208B|/download/users.csv ->[http://cap.htb/](http://cap.htb/)|
    |[10:05:34]|302|208B|/download/history.csv ->[http://cap.htb/](http://cap.htb/)|
    
- **Subdomains:**  
    Discovered subdomains with server errors:
    - **[www.smart.cap.htb](http://www.smart.cap.htb/) :** [Status: 500]
    - **web5938.cap.htb:** [Status: 500]
    - **micasa.cap.htb:** [Status: 500]
    - **[www.frm.cap.htb](http://www.frm.cap.htb/) :** [Status: 500]