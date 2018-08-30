# localdomain

1. Go to C:/Windows/System32/drivers/etc/host
  	add the following:
        127.0.0.1   example.domain.test
        
2. Go to C:/xampp/apache/conf/extra/httpd-vhosts
    add the following:

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

3. Create SSL cert
go to C:\Xampp\Apache and run "makecert"
Enter a PEM passphrase and the other information you are asked for. For Common Name, you should enter the domain you want to use for the virtual host, so the certificate is signed for that domain.
After processing all steps, you maybe want to import the cert into your browser (it lives under C:/xampp/apache/conf/ssl.crt/server.crt). Nevertheless, you will get a warning about insecure self-signed certificate after loading your website – you need to add it as an exception.
