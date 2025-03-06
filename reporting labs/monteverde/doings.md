we found domain MEGABANK.LOCAL
after check dns notes we found monteverde.MEGABANK.LOCAL
after enumerating we found whole users in system and try to find password
![[Pasted image 20250223143749.png]]
we found that one of the users uses his password as well as his username
![[Pasted image 20250223143905.png]]
we use users$ share and found azure.xml file in mhope dir
![[Pasted image 20250223144129.png]]
4n0therD4y@n0th3r$
this may be password for mhope
![[Pasted image 20250223144207.png]]
mhope member of azure admins

we found this cheat sheet https://blog.xpnsec.com/azuread-connect-for-redteam/
and use [azuread_decrypt_msol.ps1](https://gist.github.com/xpn/0dc393e944d8733e3c63023968583545#file-azuread_decrypt_msol-ps1)

but we change this parametr
$client = new-object System.Data.SqlClient.SqlConnection -ArgumentList "Server=MONTEVERDE;Database=ADSync;Trusted_Connection=true"
![[Pasted image 20250224131805.png]]
d0m@in4dminyeah!
