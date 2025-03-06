view-source:http://2million.htb/invite
it this directories when we saw on code page we found:
src="[/js/inviteapi.min.js](view-source:http://2million.htb/js/inviteapi.min.js)

when we unminify this we get 2 function
![[Pasted image 20250130165016.png]]
then we do req and get:
![[Pasted image 20250130165106.png]]
then we do req to /api/v1/invite/generate and get code
after gen code we do registy and login to account
then we found button in access, button is connection p...
this button give for as new dirictoris to research and we found /api/v1

after researching we found new directories and do req to /api/v1/admin/settings/update and add Content-Type: applications/json , then we get parameters that we need
![[Pasted image 20250130210237.png]]

then we found command injection (we need add # in the end)
![[Pasted image 20250130213757.png]]

and in terminal we found credentials for admin
![[Pasted image 20250130213837.png]]

DB_USERNAME=admin
DB_PASSWORD=SuperDuperPass123

then we found mail in /var/mail/admin
in this mail sender said that os is vulnerable becaus version of this os is linux 5.15.70

we use this exploit and get root
https://github.com/xkaneiki/CVE-2023-0386