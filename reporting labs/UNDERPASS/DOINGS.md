1. **Extracting Default Credentials:**
	- Analyzed the file `/daloradius/doc/install/INSTALL` to find default credentials:
2. **Logging into the Application:**
	- Accessed the login page at `/daloradius/app/operators/home-main.php` and authenticated using the extracted credentials.
3. **Cracking User Passwords:**
	- Extracted the MD5 hash of the `svcMosh` user from the user list and cracked it using a password cracker
4. **Gaining Initial Access:**
	- Authenticated via SSH using the cracked credentials
	 `ssh svcMosh@10.10.11.48`
5. **Identifying Privilege Escalation Vectors:**
	- Checked sudo privileges for the `svcMosh` user:
		sudo -l
		Result:
		User svcMosh may run the following commands on localhost:
		(ALL) NOPASSWD: /usr/bin/mosh-server
6. **Exploiting Mosh for Privilege Escalation:**
	- Used the following command to escalate privileges to root:
		`mosh --server="sudo /usr/bin/mosh-server" localhost`
