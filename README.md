# basic-linux-server-config

# Install php, MySQL, phpMyAdmin and access phpMyAdmin from browser

    sudo apt install mysql
        sudo systemctl status mysql.service
            - check mysql status is avtive or inactive
        sudo systemctl start mysql.service
            - to start mysql
        sudo mysql
        ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
        exit;
        mysql -u root -p
        ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;

    php-mbstring: A module for managing non-ASCII strings and convert strings to different encodings
    php-zip: This extension supports uploading .zip files to phpMyAdmin
    php-gd: Enables support for the GD Graphics Library
    php-json: Provides PHP with support for JSON serialization
    php-curl: Allows PHP to interact with different kinds of servers using different protocols

    sudo ln -s /usr/share/phpmyadmin/ /var/www/html/
        - to create symblink to access the phpMyAdmin

# install curl
    sudo apt install curl

# Install latest/specific nodejs and npm
    curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash - && sudo apt-get install -y nodejs

# Linux firewall activation
    sudo ufw status
        - show the firewall status active/inactive
    sudo ufw enable
        - Firewall is active and enabled on system startup
    sudo ufw allow 22/tcp
        - open the port #22 to listen tcp connection from anyhwere (from any ip around the world) (ip-v4/ip-v6)
    sudo ufw allow http
        - open 80 port to listen/establish http connection from any ip 
    sudo ufw allow from 69.171.224.37/16 port 80,443 proto tcp
        - Allow HTTP and HTTPS through Subnet
    sudo ufw allow from 10.0.2.15 port ssh
        - Allow SSH from Specific IP
    sudo ufw allow "Apache Full"
        - Allow Apache through Firewall
    sudo ufw allow "NGINX Full"
        - Allow NGINX through Firewall
    sudo ufw status numbered
        - to get the number of the rules
    sudo ufw delete 5
        - How to Delete UFW Rules in Ubuntu
    sudo ufw reset
        - to reset the firewall rules
        

# Change ownership of directory(s) recursively
    sudo chown -R ${USER}:${USER} /var/www/html/

# Change permission of a file/folder recursively
    sudo chmod -R 777 directory/file location

# install .deb file
    sudo dpkg -i <package-name>


# git configuration:
    sudo apt install git -y
    git config --global user.name "user-name"
    git config --global user.email "email"
    git config --list

# install and configure Nginx
    sudo apt install nginx -y 
        - this will create a directory /var/www/html and a file index.nginx-debian.html



