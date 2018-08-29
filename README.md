# localdomain

1. Go to C:/Windows/System32/drivers/etc/host
  	add the following:
        127.0.0.1   [custom domain name]
        
2. Go to C:/xampp/apache/conf/extra/httpd-vhosts
    add the following:
        NameVirtualHost *
          <VirtualHost *>
              DocumentRoot "C:/Xampp/Htdocs"
              ServerName localhost
          </VirtualHost>
          <VirtualHost *>
              ServerName [custom domain name]
              ServerAlias [ custom alias ]
              DocumentRoot "[directory]"
          </VirtualHost>
