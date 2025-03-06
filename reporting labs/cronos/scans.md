PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 18:b9:73:82:6f:26:c7:78:8f:1b:39:88:d8:02:ce:e8 (RSA)
|   256 1a:e6:06:a6:05:0b:bb:41:92:b0:28:bf:7f:e5:96:3b (ECDSA)
|_  256 1a:0e:e7:ba:00:cc:02:01:04:cd:a3:a9:3f:5e:22:20 (ED25519)
53/tcp open  domain  ISC BIND 9.10.3-P4 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.10.3-P4-Ubuntu
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Cronos
|_http-server-header: Apache/2.4.18 (Ubuntu)

subdomains:
www                     [Status: 200, Size: 2319, Words: 990, Lines: 86, Duration: 136ms]
admin                   [Status: 200, Size: 1547, Words: 525, Lines: 57, Duration: 132ms]

directories:
[15:45:14] 403 -  295B  - /.htpasswds                                       
[15:45:14] 403 -  297B  - /.htaccess_sc
[15:45:14] 403 -  299B  - /.htpasswd_test                                   
[15:45:14] 403 -  297B  - /.htaccessOLD                                     
[15:45:14] 403 -  296B  - /.httr-oauth
[15:45:14] 403 -  289B  - /.htm                                             
[15:45:14] 403 -  290B  - /.html                                            
[15:45:17] 403 -  290B  - /.php3                                            
[15:45:17] 403 -  289B  - /.php                                             
[15:45:58] 301 -  306B  - /css  ->  http://cronos.htb/css/                  
[15:46:07] 200 -    0B  - /favicon.ico                                      
[15:46:15] 404 -   11KB - /index.php/login/                                 
[15:46:18] 200 -  449B  - /js/                                              
[15:46:54] 200 -   24B  - /robots.txt                                       
[15:46:57] 403 -  298B  - /server-status                                    
[15:46:57] 403 -  299B  - /server-status/                                   
[15:47:24] 200 -  914B  - /web.config