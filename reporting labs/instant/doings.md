we found lfi vuln 
![[Pasted image 20250127140904.png]]

then we open id_ssh file in ~/.ssh/id_rsa, end get rsa key to login in ssh

after this we crack file sessions-backup with tool SolarPuttyDecryptor
and get credentials
"Credentials": [
        {
            "Id": "452ed919-530e-419b-b721-da76cbe8ed04",
            "CredentialsName": "instant-root",
            "Username": "root",
            "Password": "12**24nzC!r0c%q12",
            "PrivateKeyPath": "",
            "Passphrase": "",
            "PrivateKeyContent": null
        }
    ],