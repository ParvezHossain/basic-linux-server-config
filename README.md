# basic-linux-server-config

 # Practical Examples of Linux Find Command
 - https://www.tecmint.com/35-practical-examples-of-linux-find-command/#:~:text=The%20find%20command%20is%20used,size%2C%20and%20other%20possible%20criteria

# Login to linux server using public private key instead of password

sudo apt install openssh-server
sudo apt install openssh-clinet

Generate rsa public/private key to the client machine
- ssh-keygen -b 4096
copy the authorized key to the server
- ssh-copy-id -p 22 user@127.0.0.1
If ssh-copy-id does not work on windows machine, run this command
- Get-Content $env:USERPROFILE\\.ssh\id_rsa.pub | ssh -p 22 user@127.0.0.1 "cat >> .ssh/authorized_keys"

# Install Prometheus and Grafana

- Use Prometheus from Docker Hub
    -- docker pull prom/prometheus

- step-1: Create Prometheus system’s group 
    - First, create a user and Prometheus system’s group before installing the prometheus on Ubuntu 22.04. To create the prometheus system group, execute the given command in terminal:
    sudo groupadd --system prometheus
    
- Step-2: Add user to assign the group
    - When the group is created, add the Prometheus user and assign it the created group. To add a user and assign the created group, type and run the following command in Linux terminal: 
    sudo useradd -s /sbin/nologin --system -g prometheus prometheus

- Step 3: Create directory
    - The Prometheus has its own storing system. However, it stores the data using the directory. Therefore, to create the directory, run the following command:
    
- sudo mkdir /etc/prometheus
    - It is the primary directory of Prometheus. However, it will have some sub directory. To create sub directory, run the below mentioned command:
        sudo mkdir /var/lib/prometheus
    
- Step 4: Download, extract and move to the extracted folder
    - And move the binary files to the local folder to change the directory. To move the files to /usr/local/bin, use the following command:
    sudo mv prometheus promtool /usr/local/bin/
    
- Step 5: Move Prometheus configuration template
    - When the installation is completed successfully, move the configuration template to the /etc directory for Prometheus configuration. To move the template, run the following command:
    sudo mv prometheus.yml /etc/prometheus/prometheus.yml
    
- You should also move the console libraries to the /etc  directory to change back to the home directory. To move the console libraries, type and run the following command:

- sudo mv consoles/ console_libraries/ /etc/prometheus/

- How to configure Prometheus on Ubuntu:
- sudo nano /etc/prometheus/prometheus.yml

- How to Create Prometheus systemd service
    - If you want to start the prometheus automatically then you should create the prometheus systemd service file. Type and execute the command in terminal as given in following:
    sudo nano /etc/systemd/system/prometheus.service
        - And paste this

    [Unit]
    Description=Prometheus
    Documentation=https://prometheus.io/docs/introduction/overview/
    Wants=network-online.target
    After=network-online.target
    [Service]
    User=prometheus
    Group=prometheus
    Type=simple
    ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

    [Install]
    WantedBy=multi-user.target


    How to Reload and enable the Prometheus:
    sudo systemctl daemon-reload
    sudo systemctl enable --now prometheus
    sudo systemctl status prometheus
    sudo ufw allow 9090/tcp

    journalctl -t prometheus

    Reference: https://itslinuxfoss.com/how-to-install-prometheus-on-ubuntu-22-04-lts/

# Install Docker

- curl -fsSL https://get.docker.com -o get-docker.sh
- sudo sh get-docker.sh
- sudo systemctl restart docker
- sudo chmod 666 /var/run/docker.sock

# Install php, MySQL, phpMyAdmin and access phpMyAdmin from browser

- sudo apt install php-fpm php-mysql
    - change fpm version in /etc/nginx/sites-available/default

- sudo apt install mysql
- sudo systemctl status mysql.service
- check mysql status is avtive or inactive
- sudo systemctl start mysql.service
- to start mysql
- sudo mysql
- ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
    exit;
- mysql -u root -p
- ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;

- php-mbstring: A module for managing non-ASCII strings and convert strings to different encodings
- php-zip: This extension supports uploading .zip files to phpMyAdmin
- php-gd: Enables support for the GD Graphics Library
- php-json: Provides PHP with support for JSON serialization
- php-curl: Allows PHP to interact with different kinds of 
- servers using different protocols

- sudo ln -s /usr/share/phpmyadmin/ /var/www/html/
- to create symblink to access the phpMyAdmin

# install curl
    sudo apt install curl

# Install latest/specific nodejs and npm
    curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash - && sudo apt-get install -y nodejs

# Linux firewall activation
- sudo ufw status
    - show the firewall status active/inactive
- sudo ufw enable
- Firewall is active and enabled on system startup
    - sudo ufw allow 22/tcp
    - open the port #22 to listen tcp connection from anyhwere (from any ip around the world) (ip-v4/ip-v6)
    sudo ufw allow http
    - open 80 port to listen/establish http connection from any ip 
    - sudo ufw allow from 69.171.224.37/16 port 80,443 proto tcp
    - Allow HTTP and HTTPS through Subnet
    - sudo ufw allow from 10.0.2.15 port ssh
    - Allow SSH from Specific IP
    - sudo ufw allow "Apache Full"
    - Allow Apache through Firewall
    - sudo ufw allow "NGINX Full"
    - Allow NGINX through Firewall
    - sudo ufw status numbered
    - to get the number of the rules
    - sudo ufw delete 5
    - How to Delete UFW Rules in Ubuntu
    - sudo ufw reset
    - to reset the firewall rules
        

# Change ownership of directory(s) recursively
- sudo chown -R `$`{USER}:`$`{USER} /var/www/html/

# Change permission of a file/folder recursively
- sudo chmod -R 777 directory/file location

# install .deb file
- sudo dpkg -i <package-name>

# git configuration:
- sudo apt install git -y
- git config --global user.name "user-name"
- git config --global user.email "email"
- git config --list

# install and configure Nginx
- sudo apt install nginx -y 
    - this will create a directory /var/www/html and a file index.nginx-debian.html


# Install FTP server
- https://linuxize.com/post/how-to-setup-ftp-server-with-vsftpd-on-ubuntu-20-04/
