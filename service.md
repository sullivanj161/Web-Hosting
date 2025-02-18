1. Firewall Acknowledgements
   The firewall is managed through a security group policy that is setup to communicate via HTTP protocol that is on port 80 of the TCP protocol. Through this security group policy, it is allowing any sort of traffic that is coming through the inbound route to gain access to the server through port 80, it is essentially accepting all forms of traffic that are flowing to this specific port on the server

2. Controlling Apache as a service
   Controlling Apache as a service is important to initially configure the process of setting up the Apache server,
   Using the sudo command which is a super user command that grants the ability to be able to run programs and use other security locked tools that would normally be limited to administrators.
   In this task, I used the following commands
   sudo apt update - this command updates packages that are availiable on a Linux environment, this is essential when installing the Apache to ensure that the device has the proper configurations and properties in order to run Apache

   sudo apt install apache2 -y - this command installs the Apache 2 HTTP Server program that is used for this task
   in order to launch the contents on the server, the y is the yes button.

   sudo systemctl start apache2 - this command is responsible for starting Apache 2 at the administrator level

   sudo systemctl enable Apache 2 - this command is responsible for enabling Apache 2 to start every time ad the administrator level

   sudo systemctl status apache2 - this command is responsible for ensuring the status at the administrator level

3. Root document directory definition
   The root documents are house in the following areas, which is where I went to go and configure these to display the code HTML and CSS generated codes
   /var/www/html/index.html
   /var/www/html/styles.css 
   /var/www/html/404.html
   these were managed using the nano application in Apache that helped edit and configure to read the codes as entered

4. Steps to adding content to defined content root directory
  First, make it to the ubuntu powershell page, from here, I typed in the command sudo systectl enable Apache 2 to enable the proce]ss of Apache running. Second, to ensure that Apache was running
  I went to the IP Address I assigned the EC2 Instance and Apache popped up as active. Third, I issued the commands sudo nano /var/www/html/index.html /var/www/html/styles.css 
   /var/www/html/404.html all using the sudo nano command to edit and modify the code. Lastly after making the changes, I write the save using CTRL+O and CTRL+X to exit

5. Two ways to determine server is issuing content via Apache
   There are two methods that I know of that helped determine the status of the Apache server,

   Method 1: Simply going to the IP address of the server itself and getting a reply by accessing the page itself proves that the Apache server is currently up and running at its core

   Method 2: issuing a sudo command at sudo systemctl status apache2 checks the status of the Apache server as either up or running

   6. Photographs of documentation
  
   ![404 example on website](https://github.com/user-attachments/assets/e86b2555-e7fd-4c43-83f0-ef0445e8c2fb)
![screen shot of website](https://github.com/user-attachments/assets/809b8d8e-3f3e-4d18-bc1e-730640eb6a45)
![screenshot of index html](https://github.com/user-attachments/assets/89df84de-abd9-4db4-a2c1-920ea4ad3c05)
![screenshot of css code](https://github.com/user-attachments/assets/698d1718-b683-4041-9755-9e52ae527430)
![screenshot of 404](https://github.com/user-attachments/assets/d5d8dd2a-b89a-4931-aa6b-633f76d72bff)

