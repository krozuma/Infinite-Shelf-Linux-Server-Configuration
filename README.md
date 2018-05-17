# Infinite-Shelf-Linux-Server-Configuration

* __Public IP Address:__ http://ec2-13-58-229-23.us-east-2.compute.amazonaws.com
* __SSH port:__ 2200

### Server Configuration ###
__1. Create new user grader__
* Give grader sudo access by adding grader ALL=(ALL:ALL) ALL to /etc/sudoers.d/grader
* Added my host address to /etc/hosts host list

__2. Set up key-based authentication for grader__
* On my local machine using Git bash I ran ssh-keygen -t rsa to generate the key and saved it
* Logged in as grader I copied and pasted the key into /home/grader/.ssh/authorized_keys
* On my lighsail console, I uploaded my ssh key file from my local machiene

__3. Set up exclusive key-based authentication__
* I edited /etc/ssh/sshd_config by changing the PasswordAuthentication line to no
* Saving the file 
* Running service ssh restart

__4. Changed the SSH port from  22 to 2200__
* I edited /etc/ssh/sshd_config by changing the port line to 2200
* I saved the file
* I ran sudo service ssh restart

__5. Configure server timezone to UTC__
* Ran sudo timedatectl set-timezone UTC
* Ran sudo apt-get install ntp to synchronize time over the network connection

__6. Update all installed packages__
* Ran sudo apt-get update
* Ran sudo sudo apt-get upgrade

__7. Configure and enable the UFW firewall__
I ran:
sudo ufw default deny incoming
 * sudo ufw default allow outgoing
 * sudo ufw allow 2200/tcp
 * sudo ufw allow www
 * sudo ufw allow ntp
 * sudo ufw enable
 
__8. Set up automatic package updates__
* Ran sudo apt-get install unattended-upgrades
* And sudo dpkg-reconfigure --priority=low unattended-upgrades to enable it

__9. Installed and configured Apache2, mod-wsgi and Git__
* I ran sudo apt-get install apache2 libapache2-mod-wsgi git
* I enabled mod_wsgi by running sudo a2enmod wsgi

__10. Installed and configured PostgreSQL__
* I installed the PostgresSQl depencies by running sudo apt-get install libpq-dev python-dev
* I installed PostgreSQL by running sudo apt-get install postgresql postgresql-contrib
* I checked that remote connections are not allowed by running sudo cat /etc/postgresql/9.3/main/pg_hba.conf

__11. I installed Flask and other packages necessary or my project__
I ran:
* sudo apt-get install python-pip
* sudo pip install Flask
* sudo pip install httplib2 oauth2client sqlalchemy psycopg2 sqlalchemy_utils
* sudo pip install requests
