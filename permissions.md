1.1. Document the username utilized by the Apache Service.
   The username by default that the HTTP Apache Server uses the user group www-data by default, was able to uncover this by using the commands

   2. Determine and document a permissions structure for server admins and site developers
Usually, I would consider admins to have full access to the entire Apache HTTP server, this way, they can modify, create, edit and delete whatever changes they may need to make in the future.
Be it managing security, change user passwords, erase users which typically admins will be in charge of. When implementing the permissions structures for the users in the Apache HTTP server database,
I think that it will be of utmost importance to label the admins in the top of a hierarchy.

Site Developers, on the other hand will have limited access to being able to make changes, delete and modify objects
typically, site developers will be in charge of being able to maintain the HTTP Server, and will rarely be able to make
changes to files and or directories, in rare cases, they will be given permissions to such. For this task they will get
limited access. The root directory will be able to be editable by the site developers for example, but Apache will be able to view
Both groups will have users with Passwords

Below is a diagram of what a proposed layout may looklike 
![image](https://github.com/user-attachments/assets/b954391d-6313-4490-a370-4d5317267b31)

3. Implement the structure
When creating the structure and the groups I used the sudo groupadd (insert group name), when confirming
the groups were created I used cat /etc/group and it shows the two groups there
Proof of groups(https://github.com/user-attachments/assets/13f190ad-4a81-450d-bbb0-cb99e2692b3e)

Next step is to create the users, I used a simple command sudo useradd sullivan and then to set a password to 
the accounts I used sudo passwd sullivan and typed in a password, then I move sullivon to the site-developers group using sudo usermod -aG site-developers sullivon and sullivan 
using the same command but using admins and sullivan

Then, I will want to set the privileges towards the groups that I wish to have read and write access controls
using sudo superuser command and chown which changes the ownership of a specific entity I am able to type in, in this case sudo chown -R www-data:site-developers /var/www/html
Sullivan has been put into the admins section
![image](https://github.com/user-attachments/assets/25c870e8-e8fc-4d22-bbda-2bd9e0affa9a)

Sullivon into the site-developers

![image](https://github.com/user-attachments/assets/7cbf4bb6-c813-4ecc-8d9a-e9f6101b3301)

I gave the Apache server full access to be able to read and write in order to even be able to read and edit certain html files in order to edit
sudo chmod -R 770 ( which gives access to read and write privileges for apache ) then /var/www/html/

giving write permissions for now to site-developres group, in a real scenario, I personally would want them to have mainly read access, and sometimes if a certain file needs edited be able to write. In this case, I will also give it the 770 command
sudo chmod -R 770 

4. Write up for admins to add a new site developer
   when doing this, I will want to set the root directory as the owner of /var/www/html where the Apache server is housed at
in order to add a user to the site developer I used the sudo usermod -aG (this command adds a user to a group) site-develooper sullivon, running the groups sullivon, displays that this user is infact in the group
![image](https://github.com/user-attachments/assets/86290400-9b10-4df4-a495-291a1066cc0b)

5. Configure the site's root document directory to be editable by site developers and readable by the apache service. Document how you configured this and screenshot(s) proving your implementation worked

I performed this task using the commands 
the sudo chown -R root:site-developers /var/www/html and sudo chmod -R 775 /var/www/html/ commands 
to confirm, I performed both a sudo ls -l that lists all sorts of settings that exist in a directory or filesystem in return I got the bottom screenshots

![image](https://github.com/user-attachments/assets/6faf5a93-81f0-400c-8bea-1b2e702d8166)

for sudo ls -l /var/www/html/ (seems to have worked?????)
![image](https://github.com/user-attachments/assets/60be2a72-fa5e-4b4e-8d36-efd72a4b2238)

for Apache access in return I got
![image](https://github.com/user-attachments/assets/ccbe0e1e-9c53-4ace-a54b-efa0740dc36d)

Extra Credit Option:
Restrict site developers from using a shell session - they may only edit via SFTP. Document how you configured this and screenshot(s) proving your implementation worked
for this task I used the command sudo usermod -s /usr/sbin/nologin sullivon -s will specify the use of secure shell protocol
In order to add permissions to use sftp, $ sudo vim /etc/ssh/sshd_config I found from vultr.com
![image](https://github.com/user-attachments/assets/1ae7a9ff-3892-4674-a779-bd31f0cd6783)
Then I restarted the ssh which kicked me out of the command line the moment I entered the command

