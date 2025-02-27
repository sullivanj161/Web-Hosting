1. Identify a site that will confirm whether or not a domain is available
   While researching and finding websites that will find domain websites that will determine wheter or not a domain is available or not, there are many sites that offer the possibility of being used for a domain search
   One site that I found / knew of is Squarespace. Squarespace allows for you to see the price per year of the domain you wish to purchase, and similar names to what you searched for that may be available.
https://domains.squarespace.com/domain-search?channel=pnb&subchannel=go&campaign=pnb-go-us-en-core_domains_general-e&subcampaign=(search_domain-name-search-availability_e)&gad_source=1&gclid=EAIaIQobChMImois5OHiiwMVnzEIBR2_PDUmEAMYASAAEgKCzfD_BwE&gclsrc=aw.ds

    2. Recommend two different domain names to purchase / lease. Defend your choices and which the business should buy
      Domain names that will be applicable for purchase are sullivanscookieshop.com which is available for $14 and sullivanscookieshoponline.com for $14 on Sqaurespace
      these could be good choices due to their relatively low price per year. They could also be good choices simply due to the fact that apparently .com is usually a more trust worthy and more recognizable domain
      According to Mailchimp, .com domains are "usually designed for commercial businesses." Not only that, but .com domains are usually according to Mailchimp ".com domains tend to be more reliable than .org domains" which gives a safe
      reasoning to select between two options for .com domains
      Affordable pricing at $14 a year
      .com domains that add more reliability and use for commercial businesses such as the cookie shop
      also more search engine optimization customizable according to ChatGPT which can allow for commpany exapansion accross the internet
https://mailchimp.com/resources/org-vs-com-vs-net-domain-extensions/

   3. Explain how the domain to point to the web server's public IP - in other words, how will the DNS record be created
      The DNS record can be created through using a Squarespace interface according to the Sqaurespace website at https://support.squarespace.com/hc/en-us/articles/215744668-Pointing-a-Squarespace-domain

The first step is to open the domains dashboard on Sqaurespace, then you will want to click the domain you wish to point in this case this could be sullivanscookies.com
Go to DNS, and DNS settings 
You will then want to create custom records and add a record from there
from the Type drop down menu and select CNAME
In the host field enter www
in the data field, enter the URL from provider
then we save

In order to complete the connection we essentially do the settings again
The first step is to open the domains dashboard on Sqaurespace, then you will want to click the domain you wish to point in this case this could be sullivanscookies.com
Go to DNS, and DNS settings 
You will then want to go to custom records
now we click add
this time from the drop down menu, we select A
in our host field we enter @
in the data field, we enter the IP address from our apache https server
then we click save, this could take up to 24 - 72 hours to effectively change
https://support.squarespace.com/hc/en-us/articles/215744668-Pointing-a-Squarespace-domain

   4. Identify a Certificate Authority and defend why the business should use them as their vendor
      From previous in class, we know that CA's are trusted entities that issue SSL certificates for websites
      The Sec Master designates that there are different types of Certificate authority such as a domain validated ca which is the most basic type of a CA, you do not need to verify identity and are the fastest and easiest to get a CA from
      then there are Organization Validated CA's which verify both domain ownership and organizations identity, usually longer to obtain because this CA has to verify organizations identity
      Extended Validation (EV) Certificate Authorities:
EV CAs offer the highest level of security and trust. In addition to verifying your domain ownership and organization’s identity, EV CAs also verify your physical address. Take weeks to assign, thourough verification process
Self Signed are uncredited annd usually untrusted through browsers.
https://thesecmaster.com/blog/what-are-the-different-types-of-certificate-authority
With these in mind, I would want to choose an DV Organization Validated CA for the reasons of

can be used for small businesses
adds bare minimum security with peace of mind especially for a small cookie business
low level of authetication
affordable, some are free such as from LetsEncrypt
Shows as valid domain

A CA of this can be obtained from LetsEncrypt, which offers a free zero-cost secure environment that uses TLS security as the best practices. 
It can be obtained through simply email by verifying the validity of a domain. Once confirmed, it can issue the CA within a few hours
https://letsencrypt.org/how-it-works/

   5. Identify and defend the type of certificate the business should pursue
      The business should be required to use TLS/SSL certificates,
      a SSL/TLS certificate benefits massively due to their dedication towrds keeping site data and users data secure
      This will help secure stuff like
      Login information
      Credit card information
      other forms of sensitve information that can be entered (it is important to note we are running a business that should
      have the capabilities to order off the site from.
   The business should pursure the DV because of
can be used for small businesses
adds bare minimum security with peace of mind especially for a small cookie business
low level of authetication
affordable, some are free such as from LetsEncrypt
Shows as valid domain
      
  6. Document the steps the business will need to take to receive a valid certificate for the domain recommended
     According to LetsEncrypt, how to receive the certificate
     this is all performed through domain validation which identifies the server administration key by public key
     this involves an agent software interacting with letsencrypt to generate the key and will need to validate the domain as a
     verified owned domain by the user, this is done via email. and will confirm the domain.

     In the mean time, the business will need to log in to the HTTPS Apache server and generate a CSR certificate signing request

     typing in openssl req -new -newkey rsa:2048 -nodes -keyout sullivanscookieshop.com.key -out sullivanscookieshop.com.csr
     then will want to enter the information that correctly correlates to business location and information

     the CSR is important because it will want to be submitted to the CA, this will prompt the email for confirmation to the CA of the valid domain

Once the CA is obtained, you will want to sudo nano into the conf locations
in this case using sudo nano /etc/apache2/sites-available/default-ss.conf 
after this, the business will want to change the line
SSLCertificateFile /cert/path/sullivanscookieshop.com.crt
SSLCertificateKeyFile /key/path/sullivanscookieshop.com.key
after receiving the key and the cert to enable the use of the DV certification

after this is performed, the apache server must be restarted in order for the changes to take place,

after restart, head to the website and it should populate that it is TLS/SSL encrypted through LastEncrypt.
This can be found by going to the padlock on Firefox, from here click connection secure, and in this case it should say secure through LastEncrypt,
if on chrome, the user will want to go to the sliders right next to the task bar
click on connection is secure then site is valid
from there it should say Organization (O) as LetsEncrypt.
