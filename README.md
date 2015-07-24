# ec2-notes



DEBIAN/UBUNTU VM CREATION
-------------------------

1.  Log into aws.amazon.com.  Click EC2.

2.  Create key pair.  Save the .pem file for safekeeping--this is your private key.  Keep this secret.

3.  Go to EC2.  Launch Instance.  "Select" the Ubuntu server.

4.  Select "Free tier" option, use defaults and Launch.

5.  Select the key pair from Step 2.  Launch Instances.

6.  Note "Public DNS".  Log in to that DNS using username "ubuntu".

7.  On command line, "sudo apt-get update"

8.  "sudo apt install dselect"

For logging in from Windows:

9.  Install xrdp and lxdm (may require "Update Packages" beforehand)

10. "sudo start lxdm"

11. "sudo passwd ubuntu"

12. Log into public DNS from Windows Remote Desktop Connection.



Drupal7 (Refer to /usr/share/doc/drupal7/README.Debian.gz)
-------

1.  drupal7.conf in /etc/apache2/conf-available needs to be moved to /etc/apache2/conf-enabled

2.  "sudo apache2ctl restart"

3.  Open browser to http://localhost/drupal7/install.php

4.  Click on Standard install.  Save and continue.  Save and continue.

5.  Fill out "Configure site" form for admin account and email information.



DRUPAL FTP ACCESS (For modules installation page)
-------------------------------------------------

FROM https://www.drupal.org/node/1608658
Linux Instructions (UNSECURED):

Step 1: sudo  apt-get  install  vsftpd

Step 2: sudo nano /etc/vsftpd.conf
Uncomment these settings:
listen=YES
local_enable=YES
write_enable=YES
local_umask=022
anon_upload_enable=YES
anon_mkdir_write_enable=YES

Enter the following:
local_root=/home

Step 3: sudo service vsftpd restart

Now you should be able to install modules via ftp. For user/pass, anonymous and blank password.

This was written for n00bs who just want to test modules locally. To set this up on a live server, read the documentation thoroughly.

ADDITIONALLY:
cd /usr/share/drupal7
sudo chown www-data sites
sudo chown www-data /etc
sudo chown www-data /etc/drupal
sudo chown www-data /etc/drupal/7
sudo chown www-data /etc/drupal/7/sites
sudo chown www-data /etc/drupal/7/sites/default



Drupal7 subtheme import
-----------------------

1.  "sudo mkdir /usr/share/drupal7/sites/all" 

2.  "sudo mkdir /usr/share/drupal7/sites/all/themes"

3.  "mv subtheme_dir /usr/share/drupal7/sites/all/themes"

4.  Enable subtheme from admin Appearance menu.



References
----------

http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html
http://www.comtechies.com/2013/02/how-to-set-up-gui-on-amazon-ec2-ubuntu.html


Notes
-----

"sudo service restart /etc/init.d/apache2"

/etc/apache2 directory contains the .conf files used.  apache2.conf contains useful comments.

apache2ctl is a script/program.

/etc/apache2/{conf,mods,sites}-{available,enabled}

php5-curl (needed by Drupal testing module) requires Apache restart after installation.


DRUPAL7 ORGANIC GROUPS CONFIG
-----------------------------

Prereqs:  Follow setup from https://modulesunraveled.com/organic-groups-7x-2x

Navigate to admin/structure/pages/edit/node_view
Click on Variants >> Panels >> Content
Modify Layout as needed. (OG Menu is under Add Content >> Misc)

Suggested:
"Content create links" from either EntityReference [1] or OG "Content prepopulate links"
     (Note: Latter lists only those attached via "Group Content" Content Types.)
OG Menu : multiple (also enable from admin/config/group/og_menu)
Menu Breadcrumb (also enable it from admin/config/user-interface/menu-breadcrumb)
Variation of custom "Golden" View
Anything suggested by the above video series.

[1] Entity prepopulate:
     Go to “Structure => Content types => Article => Manage fields” (to make Article creatable) (admin/structure/types/manage/article/fields)
     Click “edit” next to “Groups audience”
     If we scroll down just a bit, we’ll see the “Additional Behaviors” section. In here, we need to enable the “Entity reference prepopulate” option for this content type to show up in our “Content create links” list.

When populating group with content, turn on menu links to ensure hierarchy is tracked for Menu Breadcrumb
Also need to "add link" to appropriate menu under admin/structure/og_menu
