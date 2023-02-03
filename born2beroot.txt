if im on root i dont need to use sudo
to go to root use "su -"

add a user
- adduser user

create a group
- groupadd <group>
- groupadd user42

change user group
- usermod -aG <group> <user>
- usermod -aG sudo dimarque

see the inside the group
- getent group <group>
- getent group sudo


download stuff
- apt-get install <package>
- apt-get install ssh

download ufw
- apt-get install <package>
- apt-get install ufw

then enable ufw
- ufw enable

check if everything is ok
- ufw status numbered

allow ssh and then the port you want to use
- ufw allow ssh
- ufw allow <port>
- ufw allow 4242

check if server is open to connect to the terminal
- systemctl status ssh

get the ip of the machine
- hostname -I

connect to your terminal using ssh
- ssh <user>@<ip_address> -p <port>
- ssh dimarque@10.12.249.236 -p 4242

# PassWord configs
## setup the password rules
- nano /etc/pam.d/common-password
the rules are: maxrepeat=3 (max of 3 repeated chars) minlen=10(minimun lenght) lcredit=1(lowercase) ucredit=1(uppercase) dcredit=2(decimal) ocredit=1(other) difok=7(number of diff letters from the last password) reject_username 

## setup the password expiring date
- nano /etc/login.defs
then scroll down until you find the 3 vars

# script
## create the script(monitoring.sh)
- its located at /usr/local/bin/
now open the file
- nano /usr/local/bin/monitoring.sh
## setup the timer(crontab)
edit the crontab using
- crontab -e
and then set it to 10 min
- `*/10 * * * * /usr/local/bin/monitoring.sh`

open crontab using user(not root)
- sudo crontab -u root -e
