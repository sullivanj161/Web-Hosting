1. Identify, install, and enable modules required for the apache service to use HTTPS. Document how this was done.
In order to identify install and enable the modules required for apache server to use HTTPS. I looked up what module would be required
According to an Ubuntu website, the module we need to install is mod-ssl, to install this we use sudo a2enmod ssl which enables the ssl module, then we will want to 
configure the HTTPS module using sudo a2ensite default-ssl. then restart apache using sudo systemctl restart apache2
  https://ubuntu.com/server/docs/how-to-use-apache2-modules

2. Firewall acknowledgments to allow access to server over configured port
Enabling firewall acknowledgements is crucial to ensure traffic is able to flow through to the HTTPS port that allows for a connection
using the commands sudo ufw allow 443 will turn on traffic flow to the HTTPS port allowing for HTTPS access, through the Apache server
I personally used sufo ufw allow 443 and 80 and 22 to allow for HTTPS HTTP and SSH 

3.Create a self-signed certificate with OpenSSL. Document how this task was complete and details on the location of associated files 
In order to create a self signed certificate with Open SSL, I went over to digital ocean and followed steps in order to create a 
After doing the main processes for installing the SSL module, our next task is to create a self signed key with open ssl, we use the command
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
this key will be generated in RSA with a length of about 2048 bits long set to last up to about 365 days then will need to be regenerated again after expiration
After this we will prompt our information, for example
Country Name (2 letter code) [XX]:US
State or Province Name (full name) []:OH
Locality Name (eg, city) [Default City]:Fairborn
Organization Name (eg, company) [Default Company Ltd]:Sullivans-Domain
Organizational Unit Name (eg, section) []:NA
Common Name (eg, your name or your server's hostname) []:SullivansSite
Email Address []:turner.494@wright.edu
The key and cert will be set in those directories after such is completed.
https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-20-04


4. Configure apache to utilize your certificate. Document the process such so that future you can replace the certificates as required
Also using the same site https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-20-04
In order to configure the key and certifiaction to be used, we will need to modify the default directory of the SSL 

5. Redirect HTTP request to utilize HTTPS 
for this step, I went into my default configuration and used the commands
<VirtualHost *:443>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        Redirect "/" "https://www.52.22.207.109/ 
after sudoing into said file I made the changes from here

6. Testing for HTTPS
sure enough, when I enter my IP, it comes back as HTTPS in the search bar which proves one way that there is infact a HTTPS connection to to the website
another way we can tell there is if there is a grey padlock next to the search bar this deciphers whether or not the website is a https or not, this site itself has a self signed certificate
which gives it a gray padlock. You can also use a curl -I https://52.22.207.109 since this is a self signed certificate it will not recognize this as a secure website

![today](https://github.com/user-attachments/assets/d3a72a81-aab8-4899-952b-b948ddfc2a97)
![proof of https 123](https://github.com/user-attachments/assets/ff050ca8-a0d8-418c-ad70-77dbf2671ec2)
![proof of https](https://github.com/user-attachments/assets/213d3c96-2fee-490a-8a97-74c0c3c2222d)
![image](https://github.com/user-attachments/assets/acff2459-ac7d-41e7-8e35-c14bf6b4eb6f)

![image](https://github.com/user-attachments/assets/dba6a485-e37e-4b38-b8bd-62153dafd1c1)





