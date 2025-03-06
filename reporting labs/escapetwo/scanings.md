login with rpcclient:
rpcclient -U rose --password KxEPkKe6R8su 10.10.11.51

![[Pasted image 20250117215339.png]]
![[Pasted image 20250117215448.png]]
![[Pasted image 20250117215504.png]]
have vulnerabilities priviligies ![[Pasted image 20250117215721.png]]
![[Pasted image 20250117215741.png]]
![[Pasted image 20250117215757.png]]

PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-01-17 19:00:27Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: sequel.htb0., Site: Default-First-Site-Name)
DNS:DC01.sequel.htb
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP 
1433/tcp open  ms-sql-s      Microsoft SQL Server 2019 15.00.2000.00; RTM
| ms-sql-info: 
|   10.10.11.51:1433: 
|     Version: 
|       name: Microsoft SQL Server 2019 RTM
| ms-sql-ntlm-info: 
|   10.10.11.51:1433: 
|     Target_Name: SEQUEL
|     NetBIOS_Domain_Name: SEQUEL
|     NetBIOS_Computer_Name: DC01
|     DNS_Domain_Name: sequel.htb
|     DNS_Computer_Name: DC01.sequel.htb
|     DNS_Tree_Name: sequel.htb
|_    Product_Version: 10.0.17763
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: sequel.htb0., Site: Default-First-Site-Name)
3269/tcp open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: sequel.htb0., Site: Default-First-Site-Name)



mssql users
![[Pasted image 20250118181253.png]]
sql_svc
memberOf: CN=SQLRUserGroupSQLEXPRESS,CN=Users,DC=sequel,DC=htb
memberOf: CN=SQLServer2005SQLBrowserUser$DC01,CN=Users,DC=sequel,DC=htb
![[Pasted image 20250118200744.png]]

bloodhound AD SCAN
![[Pasted image 20250119142938.png]]

Certify scan
![[Pasted image 20250119190924.png]]
ca_svc member of group Cert Publishers