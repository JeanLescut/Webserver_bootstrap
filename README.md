# Webserver_bootstrap

After creating your VPS, go to your associated mailbox !
(Warning: you might have a filter / a rule / it could be in Spam/Junk folder)
You'll find there 2 IP addresses, 1 login, 1 password

Go to your VPS management page : https://manager.pulseheberg.com/clientarea.php
and reinstall using Debian 10. Choose a New root password.

Then login using **SSH**, not the Console (it does not work)


```bash
# Install basics
apt-get update && apt-get upgrade && apt-get install -y git vim tree telnet wget sudo

# Configure LOCALES :
# Source: https://www.thomas-krenn.com/en/wiki/Perl_warning_Setting_locale_failed_in_Debian
export LANGUAGE=en_US.UTF-8
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
locale-gen en_US.UTF-8
dpkg-reconfigure locales

# Adding colors, Alias, etc...
wget https://raw.githubusercontent.com/JeanLescut/DataScience_stack_server/master/01_unix_helpers/root/usr/bin/configurebashrc
mv configurebashrc /usr/bin/
wget https://raw.githubusercontent.com/JeanLescut/DataScience_stack_server/master/01_unix_helpers/root/usr/sbin/adduser2
mv adduser2 /usr/sbin/
chmod +x /usr/sbin/adduser2
chmod +x /usr/bin/configurebashrc
configurebashrc
```

Source: https://www.tecmint.com/install-wordpress-with-nginx-mariadb-php-on-debian-9/
```bash
# Also disable default site from nginx:
rm /etc/nginx/sites-enabled/default
systemctl reload nginx

# And Just replace :
# sudo systemctl start php7.0-fpm
# systemctl enable php7.0-fpm
# by :
sudo systemctl start php7.3-fpm
sudo systemctl enable php7.3-fpm

# Also in /etc/nginx/sites-available/wordpress.conf, replace :
fastcgi_pass             unix:/var/run/php/php7.0-fpm.sock;
# By :
fastcgi_pass             unix:/var/run/php/php7.3-fpm.sock;
# Then :
systemctl reload nginx
```
