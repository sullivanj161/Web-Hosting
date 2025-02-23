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




