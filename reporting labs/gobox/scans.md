PORT     STATE    SERVICE    VERSION
22/tcp   open     ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 d8:f5:ef:d2:d3:f9:8d:ad:c6:cf:24:85:94:26:ef:7a (RSA)
|   256 46:3d:6b:cb:a8:19:eb:6a:d0:68:86:94:86:73:e1:72 (ECDSA)
|_  256 70:32:d7:e3:77:c1:4a:cf:47:2a:de:e5:08:7a:f8:7a (ED25519)
80/tcp   open     http       nginx
|_http-title: Hacking eSports | {{.Title}}
4566/tcp open     http       nginx
|_http-title: 403 Forbidden
8080/tcp open     http       nginx
|_http-title: Hacking eSports | Home page
|_http-open-proxy: Proxy might be redirecting requests
9000/tcp filtered cslistener
9001/tcp filtered tor-orport
9002/tcp filtered dynamid
Service Info: OS: Linux;


Target: http://gobox.htb:8080/

[17:42:05] Starting:                                                                               
[17:42:36] 301 -   65B  - /axis2//axis2-web/HappyAxis.jsp  ->  /axis2/axis2-web/HappyAxis.jsp
[17:42:36] 301 -   54B  - /axis//happyaxis.jsp  ->  /axis/happyaxis.jsp     
[17:42:36] 301 -   59B  - /axis2-web//HappyAxis.jsp  ->  /axis2-web/HappyAxis.jsp
[17:42:40] 301 -   87B  - /Citrix//AccessPlatform/auth/clientscripts/cookies.js  ->  /Citrix/AccessPlatform/auth/clientscripts/cookies.js
[17:42:50] 301 -   74B  - /engine/classes/swfupload//swfupload.swf  ->  /engine/classes/swfupload/swfupload.swf
[17:42:50] 301 -   77B  - /engine/classes/swfupload//swfupload_f9.swf  ->  /engine/classes/swfupload/swfupload_f9.swf
[17:42:52] 301 -   62B  - /extjs/resources//charts.swf  ->  /extjs/resources/charts.swf
[17:42:54] 301 -   43B  - /forgot  ->  /forgot/                             
[17:42:57] 301 -   72B  - /html/js/misc/swfupload//swfupload.swf  ->  /html/js/misc/swfupload/swfupload.swf
