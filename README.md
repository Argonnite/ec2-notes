# ec2-notes



DEBIAN/UBUNTU
-------------

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


Redmine
-------
1.  Install libapache2-mod-passenger

2.  Create softlink in /etc/apache2/conf-enabled to /usr/share/doc/redmine/examples/apache2-passenger-alias.conf, then apache2ctl or service restart

3.  "apache2ctl restart"

4.  http://localhost/redmine




Drupal7 (Refer to /usr/share/doc/drupal7/README.Debian.gz)
-------

1.  drupal7.conf in /etc/apache2/conf-available needs to be moved to /etc/apache2/conf-enabled

2.  "sudo apache2ctl restart"

3.  Open browser to http://localhost/drupal7/install.php

4.  Click on Standard install.  Save and continue.  Save and continue.

5.  Fill out "Configure site" form for admin account and email information.


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



DRUPAL FTP ACCESS
-----------------

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



FROM http://jarodms-drupal.blogspot.com/2011/09/updating-modules-and-themes-requires.html
Updating modules and themes requires FTP access to your server

http://drupal.org/documentation/install/modules-themes/modules-7#comment-4690140

The short of it, change the owner of the sites/default directory to whoever the Apache default user is (www-data, apache, etc.)

chown www-data sites/default


FROM https://www.drupal.org/node/1362318
Just run this on your terminal (linux/ubuntu)
sudo chown www-data:www-data -R /var/www/drupal717/




cd /usr/share/drupal7
sudo chown www-data sites
sudo chown www-data /etc/drupal/7/sites/default
