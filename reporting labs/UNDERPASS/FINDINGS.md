1. **Docker Compose Configuration:**
	- **Description:** Found sensitive database credentials in `docker-compose.yml`
		- - **Database:** radius
		- **User:** radius
		- **Password:** radxxxxxxx
		- **Root Password:** radxxxxxxxxxxx
2. **Default Credentials in Documentation:**
    - **Description:** Found default credentials in `/daloradius/doc/install/INSTALL`:
        - **Username:** administrator
        - **Password:** rxxxxx 
3. **Vulnerable Login Page:**
    - **Description:** Discovered a login page at `/daloradius/app/operators/home-main.php`. Logged in using the found credentials.
![[Pasted image 20250202233021.png]]

1. **User Credentials in User List:**
    - **Description:** Extracted user credentials from the user list:
        - **Username:** svcMosh
        - **Password Hash:** `412DD4759978ACFCC8XXXXXXXXXXXXX` MD5 (cracked as `underwatxxxxxxxxx`)
2. **Privilege Escalation via Mosh:**
    - **Description:** The `svcMosh` user had sudo privileges to run `/usr/bin/mosh-server`. This allowed privilege escalation to root.


