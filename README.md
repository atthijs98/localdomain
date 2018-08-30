# localdomain

1. To let Windows know, for example, that the domain example.domain.test should point to the IP address 127.0.0.1 (localhost), we have to insert an entry in the Windows hosts file. The file can be found in `C:\Windows\System32\drivers\etc`. To edit it, you need admin privileges (search for the editor in Windows, right-click on it and choose Run as administrator).<br>	
At the end of the hosts file, add an entry with the following pattern:<br>
	```
	127.0.0.1   example.domain.test
	```

2. The virtual hosts in Apache can be found in the `C:\xampp\apache\conf\extra\httpd-vhosts.conf` file. Open the file and insert an entry according to the following pattern:<br>
	``` 	
	<VirtualHost example.domain.test:80>
		DocumentRoot "C:\Xampp\Htdocs\example"
		ServerName localhost
      		<Directory "C:\Xampp\Htdocs\example">
			AllowOverride All
			Order allow,deny
			Allow from all
  		</Directory>
	</VirtualHost>
	<VirtualHost example.domain.test:443>
		DocumentRoot "C:\Xampp\Htdocs\example"
		ServerName "example.domain"
		SSLEngine On
		SSLCertificateFile "conf/ssl.crt/server.crt"
		SSLCertificateKeyFile "conf/ssl.key/server.key"
		<Directory "C:\Xampp\Htdocs\example">
  			AllowOverride All
  			Order allow,deny
  			Allow from all	
		</Directory>
	</VirtualHost>
	
	```
3. Go to the Apache directory `C:\xampp\apache`.<br>
Run `makecert`.<br>
Enter a PEM passphrase and the other information you are asked for. For Common Name, you should enter the domain you want to use for the virtual host, so the certificate is signed for that domain.<br>
After processing all steps, you maybe want to import the cert into your browser (it lives under C:/xampp/apache/conf/ssl.crt/server.crt). Nevertheless, you will get a warning about insecure self-signed certificate after loading your website – you need to add it as an exception.
	

