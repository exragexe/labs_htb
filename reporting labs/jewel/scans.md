PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 fd:80:8b:0c:73:93:d6:30:dc:ec:83:55:7c:9f:5d:12 (RSA)
|   256 61:99:05:76:54:07:92:ef:ee:34:cf:b7:3e:8a:05:c6 (ECDSA)
|_  256 7c:6d:39:ca:e7:e8:9c:53:65:f7:e2:7e:c7:17:2d:c3 (ED25519)
8000/tcp open  http    Apache httpd 2.4.38
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported:CONNECTION
|_http-generator: gitweb/2.20.1 git/2.20.1
| http-title: jewel.htb Git
|_Requested resource was http://jewel.htb:8000/gitweb/
|_http-server-header: Apache/2.4.38 (Debian)
8080/tcp open  http    nginx 1.14.2 (Phusion Passenger 6.0.6)
|_http-title: BL0G!
|_http-server-header: nginx/1.14.2 + Phusion Passenger 6.0.6
in git syte we found data in db.sql
![[Pasted image 20250222172703.png]]
bill    bill@mail.htb   2020-08-25 08:13:58.662464      2020-08-25 08:13:58.662464      $2a$12$uhUssB8.HFpT4XpbhclQU.Oizufehl9qqKtmdxTXetojn2FcNncJW
+2      jennifer        jennifer@mail.htb       2020-08-25 08:54:42.8483        2020-08-25 08:54:42.8483        $2a$12$ik.0o.TGRwMgUmyOR.Djzuyb/hjisgk2vws1xYC/hxw8M1nFk0MQy

we found this on host
![[Pasted image 20250222222438.png]]

