Nmap scan report for chemistry.htb (10.10.11.38)
Host is up (0.050s latency).
Not shown: 997 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 b6:fc:20:ae:9d:1d:45:1d:0b:ce:d9:d0:20:f2:6f:dc (RSA)
|   256 f1:ae:1c:3e:1d:ea:55:44:6c:2f:f2:56:8d:62:3c:2b (ECDSA)
|_  256 94:42:1b:78:f2:51:87:07:3e:97:26:c9:a2:5c:0a:26 (ED25519)
5000/tcp open  upnp?
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Server: Werkzeug/3.0.3 Python/3.9.5
|     Date: Sat, 25 Jan 2025 12:47:09 GMT
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 719
|     Vary: Cookie
|     Connection: close
8000/tcp open  http    SimpleHTTPServer 0.6 (Python 3.8.10)


dirsearch 
[07:52:18] Starting: 
[07:53:02] 302 -  235B  - /dashboard  ->  /login?next=%2Fdashboard      
[07:53:23] 200 -    1KB - /login                                        
[07:53:24] 302 -  229B  - /logout  ->  /login?next=%2Flogout            
[07:53:48] 200 -    1KB - /register                                     
[07:54:12] 405 -  153B  - /upload